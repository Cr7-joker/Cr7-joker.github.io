---
title: Automatic news abstract extraction
tags: Python MMR TextRank
edit: 2019-02-05
categories: Python
status: Writing
description: Automatic Extraction of News Digest Using TextRank Algorithm and MMR Algorithm
---

# 利用TextRank算法实现新闻摘要的自动提取（Python）

TextRank算法的由来：PageRank算法

## PageRank

PageRank 是根据网页之间相互的超链接计算网页重要性的技术，是Google的创始人拉里·佩奇和谢尔盖·布林于1998年在斯坦福大学发明了这项技术。
提到重要性我们就会联想到我们上一个实验也计算了每一个单词的重要性 ，但是在PageRank算法中是为每个页面计算重要性，而TextRank对PageRank算法做了改进，使其可以计算每一个**句子**的重要性 。

## TextRank

机器可以模拟人的理解，给新闻中的每个句子打分，给出分数排名靠前的句子，形成文章的摘要。

### TextRank公式：

$$
WS(V_i)=(1-d)+d\cdot\sum_{V_j\in In(V_i)}{\frac{W_{ji}}{\sum_{V_k\in Out(V_j)}w_{jk}}WS(V_j)}
$$

* V<sub>i</sub>-第i个句子

* d-阻尼系数，保证每个句子由一定的权重值，一般取0.85

* In(V<sub>i</sub>),Out(V<sub>i</sub>):对于句子来说没有推荐和被推荐的区分，即每个句子都相邻

* ω<sub>ji</sub>-句子j和句子i之间的相似度 <\br>
  $$
  Similarity(S_i,S_j)=\frac{|\{w_k|w_k\in S_i\&w_k\in S_j\}|}{\log(|S_i|)+\log(|S_j|)}
  $$
  <\br>
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



#### 遇到的问题

1.分词时对停用词的处理，有些时候去掉停用词会导致两个句子之间的权值为0，进而在运用TextRank公式时会导
致分母为零
2.有些句子去掉停用词会只剩一个单词，在计算句子权重时分母会变成零
3.在对句子关联不太紧密的新闻的效果不是很好

#### 解决方法

1.在停用词设置的时候可以手动设置
2.对于单个单词的句子进行删除

