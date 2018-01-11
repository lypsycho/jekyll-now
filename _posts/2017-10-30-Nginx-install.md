---
layout: post

title: Nginx服务器入门及Linux环境安装
tags: Nginx 教程
---

## Nginx是一款轻量级Web服务器，轻量就是占用系统资源少。具体为什么这里不做深入探讨，同时Nginx也是一款反向代理服务器，如果你想知道什么是反向代理，去百度吧！！！


## 一、安装环境 

### 1、linux：<span style="color:green">CenOS 6.8 64</span>

### 2、Ngix：<span style="color:green">1.10.2版本</span>

## 二、安装步骤

### 1、安装Nginx需要的依赖

#### (1)、安装<span style="color:red">gcc</span>，使用命令<code style="color:red">yum install gcc</code>。
	备注：安装前需要检查系统是否已经安装gcc，gcc -v查询

#### (2)、安装<span style="color:red">pcre</span>，使用命令<code style="color:red">yum install pcre-devel</code>，下图为百度百科对pcre的说明：

![nginx](/images/nginx01.jpg)

#### (3)、安装<span style="color:red">zlib</span>，使用命令<code style="color:red">yum install zlib zlib-devel</code>，下图为百度百科对zlib的说明：

![nginx](/images/nginx02.jpg)

#### (4)、安装<span style="color:red">openssl</span>，使用命令<code style="color:red">yum install openssl openssl-devel</code>，openssl就是一个密码工具，Apache用它加密https，SSL用来保证数据在Internet上传输的安全的一种安全协议。ps：但是目前这个openssl好像有很大的安全漏洞！！！

	备注以上可以综合成一条命令：yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel

### 2、安装nginx

#### (1)、下载nginx，<code style="color:red">wget http://nginx.org/download/nginx-1.10.2.tar.gz</code>

#### (2)、解压缩，<code style="color:red">tar -zxvf nginx-1.10.2.tar.gz</code>

#### (3)、解压完成进入<code style="color:red">nginx-1.10.2</code>目录，依次执行<code style="color:red">./configure</code>、<code style="color:red">make</code>、<code style="color:red">make install</code>

![nginx](/images/nginx04.jpg)

#### (4)、默认<code style="color:red">nginx</code>安装在<code style="color:red">/usr/local/nginx</code>,可以使用命令<code style="color:red">whereis nginx</code>查看<code style="color:red">nginx</code>安装路径。接着进入nginx的sbin目录，<code style="color:red">cd /usr/local/nginx/sbin</code>,执行<code style="color:red">./nginx</code>启动服务器

### 如上述过程中没有出现问题，那么打开浏览器输入本机的IP地址你将看到的如下图，另外nginx默认端口号是80，所以IP地址后不需要跟端口号

![nginx](/images/nginx05.jpg)

### 三、Nginx常用命令

	1、/usr/local/nginx/sbin/nginx 启动
	2、/usr/local/nginx/sbin/nginx -s stop 关闭
	3、/usr/local/nginx/sbin/nginx -s reload 重启
	4、ps -ef | grep nginx 查看nginx进程命令


### 四、结语

#### 本篇文章到此结束，有时间在写一下关于nginx的虚拟域名配置，文章内容比较基础，要深入学习nginx的可以到网上找找其他资料。