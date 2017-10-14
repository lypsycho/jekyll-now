---
layout: post
title: 零基础自学Python 3开发网络爬虫学习（一）
tags: Python3  
---

#### 由于最近在开发一个的在线学习系统需要用到很多数据，个人觉得手工加入太过繁琐，太过耽误时间，太过脑残等等原因，所以决定学习Python3爬虫把别人的数据直接爬过来用，正好又可以借此多了解一门语言，这岂不是美滋滋嘛~~~

## 一、爬虫是什么?

![爬虫](/images/p101.png)

#### 我觉得可以用一句话来概括，爬虫就是一个可以抓取网页数据的程序。那么这个程序可以由什么语言编写呢？<code>java、C#、Python</code>等等都可以写爬虫程序，那为什么选择Python3来写呢？原因很简单，看下图：

![爬虫](/images/p102.png)

#### 百度关键字是爬虫入门，搜索出来的内容大多都与Python有关，那就说明网上大把的关于Python开发爬虫的资料等着我们去探索，另外说一点，为什么强调一下是使用Python3。Python2 和 Python 3 语法，模块等等都有很大的变动。作为刚入门Python的我肯定选择最新的版本，况且现在Python3也很稳定很成熟了。


## 二、爬虫可以做什么?

![爬虫](/images/p103.png)

## 看到第三个是不是有点小激动？？？？？



## 三、Hello爬虫

#### (1)、直接上代码

	# encoding:UTF-8	
	import urllib.request #导入库
	url = "http://www.imooc.com" #定义要爬取的网站

	reponse = urllib.request.urlopen(url) 
	#调用urllib.request.urlopen()方法传入url，事实上该方法可以传入很多参数，目前我们只传一个url，其他用到时候在说吧
	
	#目前要说的是，urllib.request.urlopen()方法的返回值类型：http.client.HTTPResponse
	#然后这个对象又有各种方法，下面先列举一些

	#1、read()读取并返回响应正文，我觉得跟浏览器右击查看网页源代码的内容差不多
	data = reponse.read()	
	#2、geturl()这个就很好理解了，返回检索资源的URL
	url= reponse.geturl()
	#3、返回响应的HTTP状态代码
	status=reponse.getcode()	
	data = data.decode('UTF-8')
	print
	print(data)
	print(url)

#### (2)、如上已经说了urllib.request.urlopen()的返回值，下面我们来看一下该方法的参数列表包含哪些

	urllib.request.urlopen(url, data=None, [timeout, ]*,
	cafile=None, capath=None, cadefault=False)

* url 可以是一个字符串形式或者Request对象
* data 该参数如果有值就是呀post方式响应，默认为GET方式
* timeout 该参数指定阻塞操作的超时，未指定使用全局默认超时设置
* cafile和capath 参数指定一组HTTPS请求的可信CA证书 

<strong>备：</strong>官方说明文档：<a href="https://docs.python.org/3/library/urllib.request.html#module-urllib.request">https://docs.python.org/3/library/urllib.request.html#module-urllib.request</a>

## 本章结束

