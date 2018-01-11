---
layout: post

title: Mysql在linux环境下的安装及配置
tags: Mysql 教程
---

<div style="border-left:3px solid red;padding-left:5px">

<span style="font-size:16px">版权声明：知识共享 尽情转载</span> 
<span style="font-size:16px;color:#999">Rookie Li</span> 

</div>

## 本文将简单介绍一下MySQL在linux环境下的安装以及一些基本的权限配置

## 一、安装


#### (1)、执行<code style="color:red">yum -y install mysql-server</code>命令，默认安装版本是5.1.73

#### (2)、修改字符集，执行<code style="color:red">vim /etc/my.cnf</code>命令，在配置文件中添加utf-8字符集，如下图：

![mysql](/images/mysql001.jpg)

#### (3)、设置mysql开机启动，执行<code style="color:red">chkconfig mysqld on</code>命令，设置好后可以使用<code style="color:red">chkconfig --list mysqld</code>查看是否生效，2-5项为打开状态即可，如图所示：

![mysql](/images/mysql002.jpg)

#### (4)、启动mysql<code style="color:red">service mysqld start</code>

#### (5)、目前登陆mysql不需要密码<code style="color:red">mysql -u root</code>

#### (6)、依次输入以下命令修改root用户密码

	1、 use mysql
	2、 UPDATE user SET password=password("Your Password") WHERE user='root'; 
	3、 flush privileges;
	4、 exit; 退出，重新登陆MySQL
	备注：还可以使用set password for root@127.0.0.1=password('your password');

#### (7)、该命令可以查看是否有匿名用户<code style="color:red">select user,host from mysql.user;</code>，如图

![mysql](/images/mysql003.jpg)

####删除匿名登陆mysql的用户<code style="color:red">delete from mysql.user where user="";</code>

![mysql](/images/mysql004.jpg)

#### (8)、配置防火墙，开放3306端口。打开防火墙配置文件：<code style="color:red">vim /etc/sysconfig/iptables</code>，加入<code style="color:red">-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT</code>，保存退出wq。然后重启防火墙<code style="color:red">service iptables restart</code>

#### (9)、添加用户,该命令表明了用户名密码以及该只能用户从本地登录MySQL

	1、insert into mysql.user(Host,User,Password) values("localhost","rookie",password("rookie"));
	2、flush privileges;
	3、exit;

#### (10)、导入sql文件
	
	1、创建数据库
	2、切换到该数据库，use xxx
	3、使用source /developer/xxx.sql;命令

#### (11)、关于web项目乱码问题

	1、检查Tomcat的server.xml文件，修改如下配置

![mysql](/images/mysql04.jpg)

	2、检查数据库编码格式，使用命令：show variables like "%char%";然后修改/etc/my.cnf。然后重启mysql服务器：service mysqld restart。如果数据是没有做修改之前导入的，这个时候应该进入数据库，检查一下数据表里面的中文字符是否能正常显示，如还是乱码，应该重新导入一下数据


![mysql](/images/mysql04.jpg)

	备注：此方法针对mysql5.1.17，其他版本尚未测试