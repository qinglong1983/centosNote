## CentOS 学习笔记 ##

**Apache** 的管理。

**Apache** 是一个非常优秀的web服务器。

### 检查Apache的安装情况 ###

查看是否有编译安装。Apache服务器的进程名称为httpd。

    find / -name httpd

如果找不到的话，可是试着使用下面的命令。

    whereis httpd

查看是否有RPM包安装

    rpm -qa | grep httpd

### 安装Apache ###
使用yum安装

    yum install httpd

###配置Apache###

系统在引导时启动Apache

	chkconfig --levels 235 httpd on

启动Apache

	/etc/init.d/httpd start

打开您的浏览器到http：//127.0.0.1，你应该看到Apache2的测试页

Apache的默认文档根目录是在CentOS上的/var/www/html目录。

配置文件是/etc/httpd/conf/httpd.conf。

配置存储在的/etc/httpd/conf.d/目录。

###测试环境###
	centos 