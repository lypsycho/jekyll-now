---
layout: post
title: 零基础自学Python 3开发网络爬虫学习（二）
tags: 教程 Python3 
---

> 继续Python 3 爬虫


##### 上篇文章很粗略的了解了一下什么是爬虫，同时也写了一个Hello 爬虫小程序。本篇文章继续对爬虫的学习，Are your ready？-嗯~~~Maybe,you will say:

![p201](/images/p201.jpg)

##### 首先，学习爬虫前得先学习一下`正则表达式`,关于正则表达式下面放一些链接供大家参考：

* <a href="https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/00143193331387014ccd1040c814dee8b2164bb4f064cff000">廖雪峰-正则表达式</a>
* <a href="http://www.runoob.com/regexp/regexp-syntax.html">菜鸟教程-正则表达式</a>


##### okey，了解一下正则，让我们直接来写程序吧，虽然我不太愿意这么做，但是我认为把程序写出来是最快的学习方法。（仅个人认为）

### 先说一下要做的事情，如果所示，http://www.imooc.com/course/list?c=fe这个链接包含慕课网的一些课程信息，现在我们要通过爬虫把慕课网的课程分类信息爬取下来


![p202](/images/p202.jpg)

### 代码

	import urllib #引入库
	import urllib.request #引入库
	import re #这是Python3 用来编译正则表达式所用到的库
	url = 'http://www.imooc.com/course/list?c=fe' # 指定要爬取的链接
	response = urllib.request.urlopen(url) # 请求并获取http.client.HTTPResponse对象
	data = response.read().decode('utf-8') # 读取数据，并设置中文编码
	linkre  = re.compile('data-ct=fe>(.+?)</a>') #定义正则
	for x in linkre.findall(data): # 抽取数据并输出
	    print(x)

### 输出结果

![p203](/images/p203.jpg)

##### 下面讲一下正则是如何提取到我们要的数据的，首先我们看一下response.read().decode('utf-8')这个方法返回的data数据是什么样子的

![p204](/images/p204.jpg)

##### 图片中仅截取了一小部分，可以看出要截取的数据包含在< a >标签中,因此需要定义一条正则表达式去匹配我们需要的数据，即：linkre  = re.compile('data-ct=fe>(.+?)</a>')，`(.+?)`里面的内容将是我们要拿到的数据，正则表达式中‘（）’括号里的内容将被提取出来。我觉得我表达的可能不太清楚，那么，可以看下图：括号里的内容将被匹配提取出来

![p206](/images/p206.jpg)

## 结语

##### 好了，以上就是简单的爬取一些文本数据。并且只爬取了`前端开发`分类下面的二级分类，程序还可以扩展一下，爬取所有一级分类一级和二级分类的数据。

## You can hava a try and see. 

![p206](/images/p207.jpg)