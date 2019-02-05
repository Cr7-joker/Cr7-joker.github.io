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

* V~i~-第i个句子

* d-阻尼系数，保证每个句子由一定的权重值，一般取0.85

* In(V~i~),Out(V~i~):对于句子来说没有推荐和被推荐的区分，即每个句子都相邻

* ω~ji~-句子j和句子i之间的相似度
  $$
  Similarity(S_i,S_j)=\frac{}{}
  $$
  