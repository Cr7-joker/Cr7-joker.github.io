---
title: Automatic news abstract extraction
tags: Python MMR TextRank TF-IDF
edit: 2019-02-06
categories: Python
status: Completed
description: Automatic Extraction of News Digest Using TextRank Algorithm and MMR Algorithm
---

# 利用TextRank算法实现新闻摘要的自动提取（Python）

TextRank算法的由来：PageRank算法

## PageRank

PageRank 是根据网页之间相互的超链接计算网页重要性的技术，是Google的创始人拉里·佩奇和谢尔盖·布林于1998年在斯坦福大学发明了这项技术。
提到重要性我们就会联想到我们上一个实验也计算了每一个单词的重要性 ，但是在PageRank算法中是为每个页面计算重要性，而TextRank对PageRank算法做了改进，使其可以计算每一个**句子**的重要性 。

## TextRank

TextRank 算法是一种**用于文本的基于图**的排序算法。其基本思想来源于谷歌的PageRank算法（其原理在本文在下面）, 通过把文本分割成若干组成单元(单词、句子)并建立图模型, 利用**投票机制**对文本中的重要成分进行排序, 仅利用单篇文档本身的信息即可实现关键词提取、文摘。

机器可以模拟人的理解，给新闻中的每个句子打分，给出分数排名靠前的句子，形成文章的摘要。

### TextRank公式：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-06-News%20abstract%20extraction/assert/T1.png" width="75%" alt="TextRank公式" >

* V<sub>i</sub>-第i个句子

* d-阻尼系数，保证每个句子由一定的权重值，一般取0.85

* In(V<sub>i</sub>),Out(V<sub>i</sub>):对于句子来说没有推荐和被推荐的区分，即每个句子都相邻

* ω<sub>ji</sub>-句子j和句子i之间的相似度

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-06-News%20abstract%20extraction/assert/T2.png" width="65%" alt="相似度计算公式" margin-left="30px"><br/>

 <br/>
 <br/>
 分子为两个句子中共同出现的词数, S<sub>i</sub>S<sub>j</sub>分别为两个句子中的单词总数

* WS(V<sub>i</sub>)(WeightSum)-每个句子的分数，初始值为一个常数，从第一句开始计算，不断迭代，直到最终每一个句子的分数不再变化为止(即小于一个极小值)

### 英文

#### 实现步骤

1. 读取新闻并将新闻分为i个句子
2. 计算每个句子之间的相似度并建立相似度矩阵(进行分词和去停用词处理)
3. 迭代计算每个句子的“分数”
4. 对每个句子依据分数从大到小排序并根据摘要要求选出合适的句子

#### 代码实现

**源代码**

```python
import math
import heapq
from itertools import product
import string
import nltk
from nltk.tokenize import WordPunctTokenizer #nltk中的句子分割器
from nltk.corpus import stopwords #nltk中的停用词库


class TextRank(object):
	def __init__(self,filename,d,min,n):   #后两个参数为可变参数，可调参优化算法
            self.filename = filename #初始化需要读取的文本的Path
            self.d = d #初始化阻尼系数
            self.min = min #初始化判断是否继续迭代的误差最小值
            self.n = n #摘要所需要的句子数
        
#读取文本内容
	def FileRead(self):
            f = open(self.filename,encoding='UTF-8')
            text = f.read()
            return text
    
#进行句子分割
	def SentenceToken(self,text):
            sent_tokenizer = nltk.data.load('tokenizers/punkt/english.pickle') # 句子分割器
            sentences = sent_tokenizer.tokenize(text)
            return sentences
    
#去除标点符号和非字母字符
	def CleanSent(self,sentences):
            delEstr = string.punctuation + string.digits
            identify = str.maketrans('', '', delEstr) # 转换字符
            Cleansentences = []
            for sentence in sentences:
                sentence = sentence.lower()
                Cleansentence = sentence.translate(identify) # 删除非字母字符和标点符号
                Cleansentences.append(Cleansentence)
    		return Cleansentences
    
#进行分词并去停用词
	def WordTokenpro(self,sentence):
            #stopwordlist = set(stopwords.words('english'))
            # 在很多新闻中去掉了nltk停用词则公式中分母可能会为0
            #如果在专业性的英文中则可以选用
            stopwordlist = ['is', 'am', 'are', 'a', 'an', 'the']
            Words = nltk.word_tokenize(sentence)
            Words = [i for i in Words if i not in stopwordlist]
            return Words
    
#计算两个句子的相似度
    	def Sentsimilarity(self,sent1,sent2):
            count = 0
            for word in sent1:
            	if word in sent2:
            		count = count + 1
            return (count/math.log(len(sent1)) * math.log(len(sent2)))

#创建相似度矩阵
	def SimilarMatrix(self,sentences):
            N = len(sentences)
            Matrix = [[0.0 for _ in range(N)]for _ in range(N)] #创建N X N的浮点数列表
            for i,j in product(range(N),repeat=2):
                if(i != j):
    			Matrix[i][j] = self.Sentsimilarity(sentences[i],sentences[j])
            return Matrix
    
#TextRank公式计算
	def Culculate(self,Matrix,scores,i):
            Sump = 0.0
            for j in range(len(Matrix)):
                fraction = 0.0
                denominator = 0.0
                # 先计算分子
                fraction = Matrix[j][i] * scores[j]
                # 计算分母
                for k in range(len(Matrix)):
                    denominator += Matrix[j][k]
                Sump += fraction / denominator
            Sum = (1-self.d) + self.d * Sump
            return Sum
    
#判断是否需要继续迭代
	def Different(self,scores,prevent_scores):
            flag = False
	    for i in range(len(scores)):
                if(math.fabs(scores[i]-prevent_scores[i]) >= self.min):
                    flag = True
                    break	
	    return flag
    
#迭代计算每个句子的分数
	def Sentscore(self,Matrix):
            scores = [1.0 for _ in range(len(Matrix))]
            prevent_scores = [0.0 for _ in range(len(Matrix))]
            while self.Different(scores,prevent_scores):
    		for i in range(len(scores)):
    				prevent_scores[i] = scores[i]
                for j in range(len(scores)):
    				scores[j] = self.Culculate(Matrix,scores,j)
    	    return scores
    
#主函数
def main():
    Test = TextRank('News.txt',0.85,0.0001,2)
    text = Test.FileRead()
    sentences = Test.SentenceToken(text) #句子分割
    cleansentences = Test.CleanSent(sentences)
    wordSets = []
    for sentence in cleansentences:
	sentence = Test.WordTokenpro(sentence)
	wordSets.append(sentence)
    Matrix = Test.SimilarMatrix(wordSets)
    scores = Test.Sentscore(Matrix)
    print(scores)
    max_index = map(scores.index, heapq.nlargest(Test.n, scores)) #找出分数最大的n个句子的索引
    for index in list(max_index): #输出分数最大的n个句子
        print(sentences[index])
        
if __name__ == '__main__':
    main()
```



**输出结果**

> 原文：
>
> ```
> James Harden misses his third straight game with a hamstring injury.
> NEW YORK (AP) -- James Harden is missing his third straight game with a strained
> left hamstring and Rockets coach Mike D'Antoni says he will probably return
> Saturday.
> Harden has worked out without discomfort but the Rockets are playing on back-toback nights, starting Friday at Brooklyn.
> Because he wouldn't use Harden in both games after returning from injury, D'Antoni
> is opting to wait the extra day and bring Harden back Saturday at Chicago. He says
> if the Rockets were just playing Friday and then been off, Harden likely would
> have played against the Nets.
> The league MVP was hurt near the end of a loss to Utah on Oct. 24 and Houston has
> been routed in both games since.
> 翻译：
> 詹姆斯哈登因腿筋受伤缺席了他连续第三场比赛。
> 纽约（美联社） - 詹姆斯哈登缺席了他的第三场比赛，左腿筋受伤，火箭队教练迈克德安东尼说他可能会在周
> 六回归。
> 哈登在没有任何不适的情况下表现得很好，但火箭队正在背靠背的比赛中进行比赛，从周五开始在布鲁克林举
> 行。
> 因为在伤病归来后他不会在两场比赛中使用哈登，所以D'Antoni选择等待额外的一天并让哈登在周六回到芝加
> 哥。他说如果火箭队在周五刚刚上场比赛，那么哈登很可能会对阵网队。
> 联盟MVP在10月24日输给犹他的比赛结束时受伤，休斯顿自从两场比赛都被淘汰出局。
> ```



> 句子的分数
>
> ```
> [0.7491461814709529, 1.4317342944926308, 0.7890567971519759, 1.2420957531473755,
> 1.0677846943912852, 0.7210011046284952]
> ```



> 摘要：
>
> ```
> NEW YORK (AP) -- James Harden is missing his third straight game with a strained left hamstring
> and Rockets coach Mike D'Antoni says he will probably return Saturday. Because he wouldn't use
> Harden in both games after returning from injury, D'Antoni is opting to wait the extra day and bring
> Harden back Saturday at Chicago.
> 翻译：
> 纽约（美联社） - 詹姆斯哈登缺席了他的第三场比赛，左腿筋受伤，火箭队教练迈克德安东尼说他可能会在
> 周六回归。
> 因为在伤病归来后他不会在两场比赛中使用哈登，所以D'Antoni选择等待额外的一天并让哈登在周六回到芝
> 加哥。
> ```



### 中文

通过import导入**textrnak4ZH**关键词和生成摘要的类，进行关键词和关键短语的提取，关键句子的摘要

#### 代码实现

**源代码**

```python
#导入textrnak4ZH关键词和生成摘要的类
from textrank4zh import TextRank4Keyword,TextRank4Sentence
from tkinter import *
import tkinter.filedialog

#定义窗口
win = Tk()
win.geometry("1600x1200")
win.title("请选择一个文本文件")

#创建分类词实例
tw = TextRank4Keyword()


#输出关键词
def Keyword(file):
    tw.analyze(file, lower=True, window=2)  # 分析文本
    lb = Label(win,text = '关键词为:')
    lb.pack()
    for words in tw.get_keywords(num=10,word_min_len=1):
        disp = Label(win,text = words.word)
        disp.pack()



#输出关键短语
def Kephrase(file):
    tw.analyze(file, lower=True, window=2)  # 分析文本
    lb = Label(win, text='关键短语为:')
    lb.pack()
    for phrase in tw.get_keyphrases(keywords_num=10,min_occur_num=2):
        disp = Label(win,text = phrase)
        disp.pack()


#创建分类句实例
ts = TextRank4Sentence()

#输出关键句
def Keysentence(file):
    ts.analyze(file,lower=True,source='all_filters')
    lb = Label(win,text = '摘要为:')
    lb.pack()
    for sentences in ts.get_key_sentences(num=3):
        disp = Label(win, text = sentences.sentence)
        disp.pack()


#创建GUI界面
def file_choose():
    filename = tkinter.filedialog.askopenfilename()
    if filename != '':
        lb.config(text = "您选择的文件是："+filename);
    else:
        lb.config(text = "您没有选择任何文件");
    file = open(filename,'r')
    news = file.read()
    Keyword(news)
    Kephrase(news)
    Keysentence(news)
    file.close()

lb = Label(win,text = '')
lb.pack()
btn = Button(win,text="选择文件",command=file_choose)
btn.pack()
win.mainloop()

```



### 遇到的问题

1. 分词时对停用词的处理，有些时候去掉停用词会导致两个句子之间的权值为0，进而在运用TextRank公式时会导
致分母为零
2. 有些句子去掉停用词会只剩一个单词，在计算句子权重时分母会变成零
3. 在对句子关联不太紧密的新闻的效果不是很好

### 解决方法

1. 在停用词设置的时候可以手动设置
2. 对于单个单词的句子进行删除



# 利用MMR算法实现新闻摘要的自动提取（Python）

## MMR原理

MMR是Maximal Marginal Releuance的缩写，中文为最大边界相关算法或最大边缘相关算法。

设计之初是用来计算Query语句与被搜索文档之间的相似度，从而对文档进行rank排序的算法。

**公式：**

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-06-News%20abstract%20extraction/assert/MMR1.png" width="75%" alt="MMR公式">

## MMR用于新闻提取

•当我们将MMR用于新闻摘要提取时，可以将Query看做是整篇文档，对公式稍作修改，变成下面这个样子：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-06-News%20abstract%20extraction/assert/MMR2.jpg" width="75%" alt="MMR用于新闻提取公式">

•左边的score计算的是句子的重要性分值，右边的计算的是句子与所有已经被选择成为摘要的句子之间的相似度最大值，注意这里的是负号，说明成为摘要的句子间的相似度越小越好。此处体现了MMR的算法原理，即均衡考虑了文章摘要的重要性和多样性。这种摘要提取方式与textrank不同，textrank只取全文的重要句子进行排序形成摘要，忽略了其多样性。

## MMR新闻提取的特点

从公式中可以看到得到的摘要的句子需要遵循两个原则：“句子重要性更高”以及“与摘要中其他句子相似程度更低”，分别对应公式中score(Di)和max[Sim(Di,Dj)]两部分，并依靠λλ进行权衡。**简单来讲，MMR得到的摘要，句句重要，且句句不同。**

其中，相似度是将句子转换为有tfidf权重的词袋模型后计算余弦相似度。对Di句子重要性的衡量采用Di与整个文档的相似度。

## 代码实现

### 英文

```python
import nltk
from nltk.tokenize import sent_tokenize,word_tokenize
from nltk.corpus import  stopwords
from collections import defaultdict
from string import punctuation
from heapq import nlargest

stopwords = set(stopwords.words('english')+list(punctuation))
max_cut = 0.9
min_cut = 0.1

def compute_frequencies(word_sent):
    freq = defaultdict(int)
    for s in word_sent:
        for word in s:
            if word not in stopwords:
                freq[word] += 1
    m = float(max(freq.values()))
    for w in list(freq.keys()):
        freq[w] = freq[w]/m
        if freq[w] >= max_cut or freq[w] <= min_cut:
            del freq[w]
    return freq

def summarize(text,n):
    sents = sent_tokenize(text)
    assert  n <= len(sents)
    word_sent = [word_tokenize(s.lower()) for s in sents]
    freq = compute_frequencies(word_sent)
    ranking = defaultdict(int)
    for i,word in enumerate(word_sent):
        for w in word:
            if w in freq:
                ranking[i] += freq[w]
    sents_idx = rank(ranking,n)
    return [sents[j] for j in sents_idx]

def rank(ranking,n):
    return  nlargest(n,ranking,key = ranking.get)

def main():
    file = open("C:\\Users\\Mr.L\\Desktop\\Python\\1.txt",'r')
    text = file.read().replace('\n','')
    res = summarize(text,2)
    for i in range(len(res)):
        print(res[i])

if __name__ == '__main__':
    main()

```

### 中文

```python
import jieba
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics.pairwise import cosine_similarity
import operator

def cleanData(name):    #句子切分
    setlast = jieba.cut(name, cut_all=False)
    seg_list = [i.lower() for i in setlast]
    return " ".join(seg_list)


def calculateSimilarity(sentence, doc):  # 根据句子和句子，句子和文档的余弦相似度
    if doc == []:
        return 0
    vocab = {}
    for word in sentence.split():
        vocab[word] = 0  # 生成所在句子的单词字典，值为0

    docInOneSentence = '';
    for t in doc:
        docInOneSentence += (t + ' ')  # 所有剩余句子合并
        for word in t.split():
            vocab[word] = 0  # 所有剩余句子的单词字典，值为0

    cv = CountVectorizer(vocabulary=vocab.keys())

    docVector = cv.fit_transform([docInOneSentence])
    sentenceVector = cv.fit_transform([sentence])
    return cosine_similarity(docVector, sentenceVector)[0][0]


data = open(r"C:\Users\Joker\Desktop\课程设计\项目\第十周\chinesenews.txt")  # 测试文件
texts = data.readlines()  # 读行
texts = [i[:-1] if i[-1] == '\n' else i for i in texts]

sentences = []
clean = []
originalSentenceOf = {}

# Data cleansing
for line in texts:
    parts = line.split('。')[:-1]  # 句子拆分
    #   print (parts)
    for part in parts:
        cl = cleanData(part)  # 句子切分
        #       print (cl)
        sentences.append(part)  # 原本的句子
        clean.append(cl)  # 干净有重复的句子
        originalSentenceOf[cl] = part  # 字典格式
setClean = set(clean)  # 干净无重复的句子

# calculate Similarity score each sentence with whole documents
scores = {}
for data in clean:
    temp_doc = setClean - set([data])  # 在除了当前句子的剩余所有句子
    score = calculateSimilarity(data, list(temp_doc))  # 计算当前句子与剩余所有句子的相似度
    scores[data] = score  # 得到相似度的列表
    # print score

# calculate MMR
n = 25 * len(sentences) / 100  # 摘要的比例大小
alpha = 0.7
summarySet = []
while n > 0:
    mmr = {}
    # kurangkan dengan set summary
    for sentence in scores.keys():
        if not sentence in summarySet:
            mmr[sentence] = alpha * scores[sentence] - (1 - alpha) * calculateSimilarity(sentence,
                                                                                         summarySet)  # 公式
    selected = max(mmr.items(), key=operator.itemgetter(1))[0]
    summarySet.append(selected)
    #   print (summarySet)
    n -= 1

print('\nSummary:\n')
for sentence in summarySet:
    print(originalSentenceOf[sentence].lstrip(' '))
print('=============================================================')

```

# 利用 TF-IDF 算法实现新闻关键词的提取(Python)

TF-IDF是一种统计方法，用以评估一字词对于一个文件集或一个语料库中的其中一份文件的重要程度。字词的重要性随着它在文件中出现的次数成正比增加，但同时会随着它在语料库中出现的频率成反比下降。TF-IDF加权的各种形式常被搜索引擎应用，作为文件与用户查询之间相关程度的度量或评级。除了TF-IDF以外，因特网上的搜索引擎还会使用基于链接分析的评级方法，以确定文件在搜寻结果中出现的顺序。

TFIDF主要思想：如果某个词或短语在一篇文章中出现的频率TF高，并且在其他文章中很少出现，则认为此词或者短语具有很好的类别区分能力，适合用来分类。TFIDF实际上是：TF * IDF，TF词频(Term Frequency)，IDF逆向文件频率(Inverse Document Frequency)。TF表示词条在文档d中出现的频率。IDF的主要思想是：如果包含词条t的文档越少，也就是n越小，IDF越大，则说明词条t具有很好的类别区分能力。如果某一类文档C中包含词条t的文档数为m，而其它类包含t的文档总数为k，显然所有包含t的文档数n=m+k，当m大的时候，n也大，按照IDF公式得到的IDF的值会小，就说明该词条t类别区分能力不强。但是实际上，如果一个词条在一个类的文档中频繁出现，则说明该词条能够很好代表这个类的文本的特征，这样的词条应该给它们赋予较高的权重，并选来作为该类文本的特征词以区别与其它类文档。这就是IDF的不足之处. 在一份给定的文件里，词频（term frequency，TF）指的是某一个给定的词语在该文件中出现的频率。这个数字是对词数(term count)的归一化，以防止它偏向长的文件。（同一个词语在长文件里可能会比短文件有更高的词数，而不管该词语重要与否。）对于在某一特定文件里的词语来说，它的重要性可表示为：
$$
tf_{i,j}=\frac{n_{i,j}}{\sum_kn_{k,j}}
$$


以上式子中分子是该词在文件中的出现次数，而分母则是在文件中所有字词的出现次数之和。

逆向文件频率（inverse document frequency，IDF）是一个词语普遍重要性的度量。某一特定词语的IDF，可以由总文件数目除以包含该词语之文件的数目，再将得到的商取对数得到：
$$
idf_i=\log\frac{|D|}{\{j:t_i\in d_j\}}
$$


其中

\|D\|：语料库中的文件总数

{j：t<sub>i</sub>∈d<sub>j</sub>}：包含词语的文件数目（即的文件数目）如果该词语不在语料库中，就会导致分母为零，因此一般情况下使用**1+\|{d∈D:t∈d}\|**作为分母。

然后再计算TF与IDF的乘积: 
$$
tf_idf_{i,j}=tf_{i,j}\times idf_i
$$


某一特定文件内的高词语频率，以及该词语在整个文件集合中的低文件频率，可以产生出高权重的TF-IDF。因此，TF-IDF倾向于过滤掉常见的词语，保留重要的词语。 

## 代码实现

```python
import math
from itertools import product
import string
import nltk
from nltk.tokenize import WordPunctTokenizer #nltk中的句子分割器
from nltk.corpus import stopwords #nltk中的停用词库
from collections import Counter
from nltk.stem.porter import *

#读取文本
def FileRead(filename):
    f = open(filename, encoding='UTF-8')
    text = f.read()
    return text

#进行分词并去除
def get_tokens(text):
    lowers = text.lower()
    # remove the punctuation using the character deletion step of translate
    delEstr = string.punctuation + string.digits
    remove_punctuation_map = dict((ord(char), None) for char in delEstr)
    no_punctuation = lowers.translate(remove_punctuation_map)
    tokens = nltk.word_tokenize(no_punctuation)
    return tokens

#像 films, film, filmed 其实都可以看出是 film，而不应该把每个词型都分别进行统计。
    #这时就需要要用 Stemming 方法。
def stem_tokens(tokens, stemmer):
    stemmed = []
    for item in tokens:
        stemmed.append(stemmer.stem(item))
    return stemmed


def def_Preprocessing(text):
    # 测试上述分词结果 Counter() 函数用于统计每个单词出现的次数。
    # 去除“词袋”中的“停词”（stop words）,因为像the, a, and 这些词出现次数很多，但与文档所表述的主题是无关的，
    tokens = get_tokens(text)
    filtered = [w for w in tokens if not w in stopwords.words('english')]
    stemmer = PorterStemmer()
    stemmed = stem_tokens(filtered, stemmer)

    count = Counter(stemmed)
    print(count)
    return count

#计算某一个单词的TF值
def TF(word,count):
    return count[word] / sum(count.values())

def n_countaining(word,count_list):
    return sum(1 for count in count_list if word in count)

#计算IDF值
def IDF(word,conut_list):
    return math.log(len(conut_list)/1+n_countaining(word,conut_list))

#计算TF-IDF值
def TF_IDF(word,count,count_list):
    return TF(word,count) * IDF (word,count_list)


#主函数
count1 = def_Preprocessing(FileRead("News1.txt"))
count2 = def_Preprocessing(FileRead("News2.txt"))
count3 = def_Preprocessing(FileRead("News3.txt"))
countlist = [count1, count2, count3]
for i, count in enumerate(countlist):
    print("Top words in document {}".format(i + 1))
    scores = {word: TF_IDF(word, count, countlist) for word in count}
    sorted_words = sorted(scores.items(), key=lambda x: x[1], reverse=True)
    for word, score in sorted_words[:3]:
        print("\tWord: {}, TF-IDF: {}".format(word, round(score, 5)))

```



# 场景比较分析

|          |                           科技新闻                           |                           体育新闻                           |                           娱乐新闻                           |                           军事新闻                           |
| :------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   特点   |                    新闻性，科学性，通俗性                    |                    娱乐性，国际性，情感性                    |                        故事性，情节性                        |                    思想性，新鲜性，显著性                    |
|   MMR    | 摘要相对全面，不仅对于反复提及科技产品或成果本身有足够的摘要，也对重要的有概括意义的相关结论有一定的摘要。 | 摘要更偏重对体育赛事的数据和过程进行描述，特别是在重要位置的比赛信息，能比较全面的概括新闻中对比赛过程的描写。 | 摘要比较简洁能够抓住核心语句，特别是新闻热点和矛盾点所在，不过摘要没法展示整个新闻中情节的发展。 | 摘要非常全面，围绕着关键事件和事物有足够多的摘要，当然会有一些与核心事件无关紧要的摘要出现。 |
| TextRank | 摘要更偏重对科技产品或成果本身描述，能够较完整的描述新闻中提及的科技产品或成果的特点，特性，参数等信息，但对一些结论不会做描述。 | 摘要更加简洁，更加有针对性，特别是新闻中反复出现的名词，会有更多与之相关的摘要，摘要能够对某一方面有充分的概括。 | 摘要更加全面，对于涉及主要事件和主要人物的片段，都会有摘要，使得摘要能够大致反映新闻中情节的发展，而且对于核心的地方也有足够的描述。 | 摘要比较简洁，对于核心事件或事物能够有相对全面的描述，但是新闻中围绕核心事件或事物的一些附加片段不会有太多的描述。 |