---
layout: post
title: MySQL
tags: sql语句 
---


>  下文总结一下mysql的各种语句

## 前言
 MySQL是目前流行的关系型数据库管理系统，mysql所使用的SQL语言也是最常用的标准化语言。
学习mysq最基础的肯定要会使用sql，下面总结一下sql的语句。

### 查询sql
1、查询X表所有内容
	
	select * from X 

2、从X表中查询Y字段

	select YYY from XXX 

3、当N=M时从X表查询内容（查询Y字段）
	
	select * from X where N=M
	select Y from X where N=M

4、IN操作符，IN操作符允许我们在WHERE子句中规定多个值
	
	select * from X where N in(value1,value2,value3,……)

5、LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式，通俗来讲就是模糊匹配

	从X表中查询内容，当N字段以M开头（反之在like前加not）
	select * from X where N like '%M'

![mysql](/images/mysql01.png)

	从X表中查询内容，当N字段中包含M（反之在like前加not）
	select * from X where N like '%M%'

![mysql](/images/mysql02.png)

上面几条查询语句中涉及到通配符，其中<code>%</code>替代一个或多个字符，<code>_</code>仅替代一个字符，<code>[charlist]</code>字符列中的任何单一字符，<code>[^charlist]</code>不在字符列中的任何单一字符

6、between操作符在WHERE子句中使用，作用是选取介于两个值之间的数据范围

操作符 BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是数值、文本或者日期。

<strong style="color:red">注意：</strong>不同的数据库对 BETWEEN...AND 操作符的处理方式是有差异的。某些数据库会列出介于 "Adams" 和 "Carter" 之间的人，但不包括 "Adams" 和 "Carter" ；某些数据库会列出介于 "Adams" 和 "Carter" 之间并包括 "Adams" 和 "Carter" 的人；而另一些数据库会列出介于 "Adams" 和 "Carter" 之间的人，包括 "Adams" ，但不包括 "Carter" 。

	从X表中查询内容，当N字段介于M,N之间，反之加NOT
	select * from X where N between M AND N

![mysql](/images/mysql03.png)

