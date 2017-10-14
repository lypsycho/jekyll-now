---
layout: post
title: vsftpd
tags: 教程 vsftpd 
---

> 下文将介绍vsftpd在linux环境的安装与使用,Linux系统为CentOs 6.8，7.0以上系统请绕道

## 简介
vsftpd是“very secure FTP daemon”的缩写，是一个完全免费的，开源的ftp服务器软件。vsftpd是一款在linux发行版中最受推崇的FTP服务器程序，小巧轻快，安全易用，支持虚拟用户，支持带宽限制等功能


### 安装步骤
<strong style="color:black">1、安装</strong>

（1）执行<code>yum -y install vsftpd</code>命令

<strong style="color:red">注：</strong>1、可以通过<code>rpm -qa | grep vsftpd</code>命令检查系统是否已经安装<strong style="color:black">vsftpd</strong>

2、默认配置文件在:<code>/etc/vsftpd/vsftpd.conf</code>


<strong style="color:black">2、创建虚拟用户</strong>

（1）选择在根或者用户目录下创建ftp文件夹：<code>mkdir ftpfile</code>,如：/ftpfile

![vsftpd](/images/vsftpd01.png)

（2）添加匿名用户：<code>useradd rookie -d /ftpfile -s /sbin/nologin</code>,添加rookie用户，但该用户没有登录该linux的权限

![vsftpd](/images/vsftpd02.png)

（3）修改ftpfile权限：<code>chown -R rookie.rookie /ftpfile</code>

![vsftpd](/images/vsftpd03.png)

（4）重设rookie密码：<code>passwd rookie</code>

<strong style="color:black">3、vsftpd配置</strong>

（1）<code>cd /etc/vsftpd</code>

（2）新建文件<code>vim chroot_list</code>	

（3）把刚才新增的虚拟用户添加到此配置文件中，后续要引用，保存退出

![vsftpd](/images/vsftpd07.png)

（4）<code>vim /etc/selinux/config</code>,修改为:<strong style="color:black">SELINUX=disabled</strong>

备注：如果验证是碰到550拒绝访问请执行：<code>setsebool -P ftp_home_dir 1</code>，然后重启linux服务器。

（5）配置vsftpd.conf:<code>vim /etc/vsftpd/vsftpd.conf</code>

	anonymous_enable=NO
	anon_root=/ftpfile
	use_localtime=YES
	chrootlistenable=YES
	chrootlistfile=/etc/vsftpd/chroot_list
	pasv_ min_port=61001
	pasv_ max_port=62000

下面列举一些常用的配置项

*  	<code>local_root=/ftpfile</code>(当本地用户登入时，将被更换到定义的目录下，默认值为各用户的家目录) 

* <code>anon_root=/ftpfile</code>(使用匿名登入时，所登入的目录)
* <code>use_localtime=YES</code>(默认是GMT时间，改成使用本机系统时间)
* <code>anonymous_enable=NO</code>(不允许匿名用户登录)
* <code>local_enable=YES</code>(允许本地用户登录)
* <code>write_enable=YES</code> (本地用户可以在自己家目录中进行读写操作)
* <code>local_umask=022</code> (本地用户新增档案时的umask值)
* <code>dirmessage_enable=YES</code> (如果启动这个选项，那么使用者第一次进入一个目录时，会检查该目录下是否有.message这个档案，如果有，则会出现此档案的内容，通常这个档案会放置欢迎话语，或是对该目录的说明。默认值为开启)
* <code>xferlog_enable=YES</code> (是否启用上传/下载日志记录。如果启用，则上传与下载的信息将被完整纪录在xferlog_file 所定义的档案中。预设为开启。)
* <code>connect_from_port_20=YES</code> (指定FTP使用20端口进行数据传输，默认值为YES)
* <code>xferlog_std_format=YES</code> (如果启用，则日志文件将会写成xferlog的标准格式)
* <code>ftpd_banner=Welcome to rookie FTP Server</code> (这里用来定义欢迎话语的字符串)
* <code>chroot_local_user=NO</code>(用于指定用户列表文件中的用户是否允许切换到上级目录) 
* <code>chroot_list_enable=YES</code> (设置是否启用chroot_list_file配置项指定的用户列表文件)
* <code>chroot_list_file=/etc/vsftpd/chroot_list</code> (用于指定用户列表文件)
* <code>listen=YES</code> (设置vsftpd服务器是否以standalone模式运行，以standalone模式运行是一种较好的方式，此时listen必须设置为YES，此为默认值。建议不要更改，有很多与服务器运行相关的配置命令，需要在此模式下才有效，若设置为NO，则vsftpd不是以独立的服务运行，要受到xinetd服务的管控，功能上会受到限制)
* <code>pam_service_name=vsftpd</code> (虚拟用户使用PAM认证方式，这里是设置PAM使用的名称，默认即可，与/etc/pam.d/vsftpd对应) userlist_enable=YES(是否启用vsftpd.user_list文件，黑名单,白名单都可以
* <code>pasv_ min_port=61001</code> (被动模式使用端口范围最小值)
* <code>pasv_ max_port=62000</code>(被动模式使用端口范围最大值)
* <code>pasv_enable=YES</code>  (pasv_enable=YES/NO（YES）
若设置为YES，则使用PASV工作模式；若设置为NO，则使用PORT模式。默认值为YES，即使用PASV工作模式。
   FTP协议有两种工作方式：PORT方式和PASV方式，中文意思为主动式和被动式。
   一、PORT（主动）方式的连接过程是：客户端向服务器的FTP端口（默认是21）发送连接请求，服务器接受连接，建立一条命令链路。 
  当需要传送数据时，客户端在命令链路上用 PORT命令告诉服务器：“我打开了* 端口，你过来连接我”。于是服务器从20端口向客户端的* 端口发送连接请求，建立一条数据链路来传送数据。
   二、PASV（被动）方式的连接过程是：客户端向服务器的FTP端口（默认是21）发送连接请求，服务器接受连接，建立一条命令链路。 
  当需要传送数据时，服务器在命令链路上用 PASV命令告诉客户端：“我打开了* 端口，你过来连接我”。于是客户端向服务器的* 端口发送连接请求，建立一条数据链路来传送数据。 
  从上面可以看出，两种方式的命令链路连接方法是一样的，而数据链路的建立方法就完全不同。而FTP的复杂性就在于此。


<strong style="color:black">4、防火墙配置</strong>

（1）打开linux防火墙配置文件 <code>vim /etc/sysconfig/iptables</code>

（2）将一下配置添加到防火墙配置中
	
	-A INPUT -p TCP --dport 61001:62000 -j ACCEPT
	-A OUTPUT -p TCP --sport 61001:62000 -j ACCEPT
	-A INPUT -p TCP --dport 20 -j ACCEPT
	-A OUTPUT -p TCP --sport 20 -j ACCEPT
	-A INPUT -p TCP --dport 21 -j ACCEPT
	-A OUTPUT -p TCP --sport 21 -j ACCEPT

备注：/etc/sysconfig/下没有iptables的问题,请参考下面链接

<a href="http://blog.csdn.net/csdn_lqr/article/details/53885808">http://blog.csdn.net/csdn_lqr/article/details/53885808</a>

（3）重启防火墙:<code>service iptables restart</code>


<strong style="color:black">5、验证vsftpd</strong>

1、执行<code>service vsftpd restart</code> 少截图

2、打开浏览器访问：<code>ftp://ip地址</code>



## 常用命令 

*	启动：<code>service vsftpd start</code>
*	关闭：<code>service vsftpd stop</code>
*	重启：<code>service vsftpd restart</code>

## 结语
以上是在linux环境下简单搭建vsftpd服务器，仅供学习和参考。另外如使用的是阿里云服务器，请配置相应的安全组规则，开放使用到的端口号

![vsftpd](/images/vsftpd10.png)