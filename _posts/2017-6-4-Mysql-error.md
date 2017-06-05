---
layout: post
title: Mysql报错系列之ERROR 1045 (28000)
tags: mysql error 
---
## 前言
本文主要讲一下在登录mysql时报ERROR 1045 (28000)这个错误的原因，仅供参考

## 错误提示 

	ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

## 分析
从错误提示上来看，大概的意思就是说用户访问被拒绝了。首先想到可以先查看一下mysql数据库当中的user表是否是因为没有设置root密码

在非正常状态登录mysql步骤如下：

### 1、修改mysql配置参数，在[mysqlld]下面加上skip-grant-tables，如下图

	[root@iZxxj29crt0wjkZ ~]# vi /etc/my.cnf 

![mysqlerror2](/images/mysqlerror2.png)

### 2、重启mysql
	
	[root@iZxxj29crt0wjkZ ~]# /etc/init.d/mysqld restart

以上配置是指在启动mysql的时候不启动grant-tables（授权表），简单来说就是不需要密码即可登录操作mysql.

### 3、登录MySQL并进入mysql库,查询user表

	mysql> use mysql;
	Database changed
	mysql> select user,host,password from user;
	+------+-----------------+-------------------------------------------+
	| user | host            | password                                  |
	+------+-----------------+-------------------------------------------+
	| root | %               | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	| root | izxxj29crt0wjkz | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	| root | 127.0.0.1       | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	|      | localhost       |                                           |
	|      | izxxj29crt0wjkz |                                           |
	+------+-----------------+-------------------------------------------+
	5 rows in set (0.00 sec)

发现系统中存在两个空的用户，想了一下可能是由于这个原因造成的，于是就将user表中的空用户删除


	mysql> delete from user where user='';
	Query OK, 2 rows affected (0.00 sec)
	mysql> select user,host,password from user;
	+------+-----------------+-------------------------------------------+
	| user | host            | password                                  |
	+------+-----------------+-------------------------------------------+
	| root | %               | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	| root | izxxj29crt0wjkz | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	| root | 127.0.0.1       | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
	+------+-----------------+-------------------------------------------+
	3 rows in set (0.00 sec)

如上user表中的空用户已成功删除，然后将第1步修改的文件还原，即删除skip-grant-tables属性，重启MySQL测试。

### 4、于是问题解决了
	
	[root@iZxxj29crt0wjkZ ~]# /etc/rc.d/init.d/mysqld restart
	170605 13:22:11 mysqld_safe mysqld from pid file /var/run/mysqld/mysqld.pid ended
	Stopping mysqld:                                           [  OK  ]
	Starting mysqld:                                           [  OK  ]
	[1]+  Done                    mysqld_safe --user=mysql --skip-grant-tables --skip-networking
	[root@iZxxj29crt0wjkZ ~]# mysql -u root -p
	Enter password: 
	Welcome to the MySQL monitor.  Commands end with ; or \g.
	Your MySQL connection id is 2
	Server version: 5.5.54 MySQL Community Server (GPL) by Atomicorp
	
	Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
	
	Oracle is a registered trademark of Oracle Corporation and/or its
	affiliates. Other names may be trademarks of their respective
	owners.
	
	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
	
	mysql> use mysql;
	Reading table information for completion of table and column names
	You can turn off this feature to get a quicker startup with -A
	
	Database changed

如上可以看出成功登陆mysql，并且可以操作。

## 总结
以上原因可能只是mysql报ERROR 1045 (28000)的原因之一，也还可能会因为其他原因报错，这个有待发现。或者如果你知道，请联系我，Thank you！

# 邮箱：rookieit@aliyun.com