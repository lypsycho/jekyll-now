---
layout: post
title: 零基础自学Python 3 链接MySQL数据库
tags: 教程 Python3 
---

> 下文将介绍PyCharm 2017链接MySQL数据库

## 扯个谈

##### 应该不会有人问PyCharm是什么吧？有的话就看下图

![pymysql](/images/pymysql03.png)

<a href="https://www.jetbrains.com/pycharm/">https://www.jetbrains.com/pycharm/</a>

##### 在我写这篇博文的时候，我发现还有个<code>PyCharm Edu</code>版本的,好像是免费的，瞬间让我对JetBrains有了点好感。不过已经是一名专业开发人员的我，就等专业版到期了在去下载看看吧

![pymysql](/images/pymysql06.png)

![pymysql](/images/pymysql04.png)

<a href="https://www.jetbrains.com/pycharm-edu/">https://www.jetbrains.com/pycharm-edu/</a>

## 重点

### 第一步

##### 打开PyCharm，然后选择File->settings->Project Interpreter-pip

![pymysql](/images/pymysql05.png)

![pymysql](/images/pymysql07.png)

### 第二步

##### 在弹出的窗口搜索<code>pymysql3</code>,然后选中<code>Install Package</code>(见下图)

##### 解释一下<code>pymysql3</code>，这个就是Python3用来链接MySQL的驱动，跟<code>mysql-connector-java-5.0.4-bin.jar</code>跟这种东西类似，如果这个你还不知道的话那么请你走！！！

![pymysql](/images/pymysql08.png)

### 第三步

##### 测试一下，在PyCharm中新建.py文件（前提你建个个Python project），接着看下面代码

	import pymysql
	conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='123456', db='mysql') #这里写上面设置的密码
	cursor = conn.cursor()
	cursor.execute("SELECT VERSION()")
	row = cursor.fetchone()
	print("MySQL server version:", row[0])
	cursor.close()
	conn.close()

##### 程序运行结果

![pymysql](/images/pymysql09.png)

##### 运行上面的程序，打印出MySQL的版本号说明你已经成功了。

## 结语

本篇文章先扯这么多！

![pymysql](/images/pymysql11.png)

