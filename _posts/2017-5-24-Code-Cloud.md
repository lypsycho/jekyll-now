---
layout: post
title: 软件安装及使用系列教程之码云
tags: git 教程
---
>下文将介绍关于码云以及git命令的使用（基础）

## 前言
1. [码云](https://git.oschina.net/)是开源中国社区团队推出的基于Git的快速的、免费的、稳定的在线代码托管平台,不限制私有库和公有库数量.
![mayun01](/images/mayun01.png)

2. [GIT](http://baike.baidu.com/link?url=UQs_Fc-h_NRQCrg0365ZbpYiG720l2QKM6GWg8zk9l1CWUBe5GT1gxmLgkFdxgne8qmaHl_PEdHMHaRdv-aUxK)是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
## 正文
2013年中国最大的开源技术社区开源中国上线"码云"平台代码托管服务，被称为"中国本土的GitHub"。那么显而易见码云相对于国内用户而言它的速度更快，并且在码云上我们可以建立公有或者私有项目，而GitHub上要建立私有项目必须付费。本文内容主要为新手简单介绍一下如何使用码云

## 第一步

+ 注册码云[http://git.oschina.net/](http://git.oschina.net/)

## 第二步
+ 下载安装git[http://git.oschina.net/](http://git.oschina.net/),可以根据自己的操作系统的下载

![mayun02](/images/mayun02.png)

+ 安装成功后打开命令行输入：git version 检查是否成功安装,如图所示即为安装成功

![mayun03](/images/mayun03.png)

## 第三步

+ 将远程仓库<em>git clone</em> 到本地

打开命令行，首先进入你想要clone到本地的路径（例如：e:xxxx）,然后执行`git clone "远端的仓库地址"`

![mayun05](/images/mayun05.png)

获取远端地址如下图

![mayun04](/images/mayun04.png)

之后会提示你输入用户名和密码(注册码云时候的账号和密码)，如图提示`Unpacking objects:100%,done`时即clone成功

![mayun06](/images/mayun06.png)

## 第四步
+ 完成以上三步之后我们就可以在本地更改文件，然后在通过以下命令来提交到远程仓库。
在使用前我们可以先配置一下个人的用户名称和电子邮件地址，如下图

![mayun07](/images/mayun07.png)

![mayun08](/images/mayun08.png)

然后依次输入如下命令：

	1、git pull origin master
	2、git add .
	3、git commit -m "更改文件的说明"
	4、git push  

然后如果提示输入账号密码的话就输入账号密码，这样就完成了一次提交。 


## 附录 
1、码云平台帮助文档 V1.2 [http://git.mydoc.io/](http://git.mydoc.io/)

2、Git常用命令总结 [http://www.cnblogs.com/cspku/articles/Git_cmds.html](http://www.cnblogs.com/cspku/articles/Git_cmds.html)


` 有任何问题可以给我留言哦，也可以发送邮件到rookieit@aliyun.com `