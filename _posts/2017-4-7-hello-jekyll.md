---
layout: post
title: 关于在Github上搭建个人博客
tags: jekyll Github
---
>下文将介绍在github搭建个人博客所使用到的技术、工具以及具体步骤

## 前言
1. [Github](https://github.com/)是一个面向开源及私有软件项目的托管平台，Github提供了一种功能*Github Pages*，使用此功能可以快速的在该平台上搭建属于自己的博客。
2. [Jekyll](http://jekyll.com.cn/)可以将纯文本转化为静态网站和博客，具体细节请参考jekyll开发文档[http://jekyll.com.cn/](http://jekyll.com.cn/)

## 正文
首先请允许我随便BB几句，我在不了解Github以及jekyll之前是在新浪博客上写博客，但偶然一天看到了 <a href="http://binux.cn">彬哥</a> 的博客，顿时觉得very高大上啊！所以必须要搞起来，以我的智商是折腾了好几天。为了让大家少走弯路，下面我会尽可能的给大家介绍一下具体操作步骤。

## 环境搭建

` |Windows 7 ` 

# Github
+ 注册Github[https://github.com/](https://github.com/)，这里不做过多解释了。
+ 下载安装github for windows，[https://desktop.github.com/](https://desktop.github.com/)
+ 克隆jekyll到自己的仓库，[https://github.com/barryclark/jekyll-now](https://github.com/barryclark/jekyll-now)

参照下图：

![jekyll01](/images/hello-jekyll01.png)

接下来参照[https://github.com/barryclark/jekyll-now](https://github.com/barryclark/jekyll-now)网址下方提供的使用说明来构建自己的博客,首先要更改仓库的名字，规则在上方链接中有介绍，更改完成后就可以用：yourusername.github.io来访问你的博客了

![jekyll02](/images/hello-jekyll02.png)

# ruby、jekyll

+ ruby和jeykll安装可以参考该链接[http://www.jianshu.com/p/310d796cf5f3](http://www.jianshu.com/p/310d796cf5f3)
+ 在安装ruby和jekyll的过程中可能会遇到一些问题，下面的链接是一些错误的解决办法
	+ [https://github.com/jekyll/jekyll/issues/3909](https://github.com/jekyll/jekyll/issues/3909)
	+ [https://github.com/juthilo/run-jekyll-on-windows/issues/34](https://github.com/juthilo/run-jekyll-on-windows/issues/34)
	+ [http://stackoverflow.com/questions/33389632/jekyll-serve-error](http://stackoverflow.com/questions/33389632/jekyll-serve-error)

## 结语
以上就是在github上使用jekyll工具搭建属于自己的博客，当然jekyll还有很多功能本文没有提到，其中包括：博客主题、评论插件、分类和归档插件等，请大家自行参考jekyll介绍文档[http://jekyll.com.cn/](http://jekyll.com.cn/)。

` 另外你有任何问题可以给我留言哦，也可以发送邮件到18351991765@163.com `