﻿# 数据驱动的酒店品牌形象量化

## 1.代码环境
- ananconda3
- python 3.8.8
- sklearn-crfsuite==0.3.6
- openpyxl==3.0.9
- torch==1.0.1.post2
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda install sklearn-crfsuite-0.3.6 
conda install openpyxl-3.0.9
```
## 2.数据集介绍
### 2.1 数据集来源
基于python技术，自行编写代码爬取网络上有关酒店的信息
### 2.2 数据组成
收集了2017 年 8 月 25 日到 2020 年 11 月 3 日来自北京6193 家酒店的 2481931 条评论，部分酒店统计数据如下：
|等级 |酒店品牌 | 酒店数量|评论总数 |含图片评论数 |
|--|--|--|--|--|
|高档|皇冠假日|6|15480|779|
|低档|全季|53|36744|2118|
|中档|假日|6|8090|391|
|.....|.....|.....|.....|.....|


## 3.项目背景

在当今竞争日益激烈的旅游行业，了解**酒店品牌形象**成为旅游管理和酒店营销中至关重要的环节。越来越多的游客通过在线的方式发布旅游居住酒店环境的照片、对酒店服务进行评论和意见等。这些以在线方式生成的内容已经成为从消费者角度反映酒店品牌形象的媒介，为酒店品牌推广和酒店品牌形象的塑造提供了重要的参考价值。


## 4.代码使用
1. 首先安装依赖项`pip install -r requirements.txt`
2. 将得到的数据集放在代码根目录`HBI/`下
3. `named_entity_recognition/test.py`可以中文命名实体识别
4. `three_tuple.ipynb`得到评论的三元组
5. `clustering.ipynb`实现三元组的聚类
6. `senti_scores.ipynb`实现情感值的计算

示例
```
git clone https://github.com/Sunzhizheng/HBI.git
cd HBI
python ./named_entity_recognition/test.py
```
中文命名实体识别的源代码来自[这里](https://github.com/luopeixiang/named_entity_recognition)

## 5.FrameWork
![输入图片说明](/image/cacf9267bfd37832e5de8ed2cb355cb.png)


### 5.1 数据爬取

- 通过自行开发的 **Python**网络爬虫程序收集数据
- 收集了从 2017 年 8 月 25 日到 2020 年 11 月 3 日来自北京**6193家酒店的2481931条评论**

### 5.2 主题分类
- 一条评论拆分为多个三元组，每个三元组由名词，动词，形容词组成
- **K-Means**对所有评论的三元组进行聚类，分为7类主题
- 7类主题分别为：**Bath** ；**Surrounding** ；**Room** ；**Price** ；**Public Area** ；**Service** ；**Food**

### 5.3 情感与频率的计算
- **BiLSTM-CRF**计算三元组的情感值
- 三元组中元素在数据集出现的频数计算频率
- 频率与情感值的加和作为该主题得分

## 6.结果展示
### 三家酒店品牌在七个方面的表现对比图如下


![图片1](/image/f3dfc05a48c77ed5da3e1f407a70211.png)


### 酒店品牌形象的七个方面的值随时间的变化图


![图片2](/image/759703b6ac7094f58429e0293faf077.png)
