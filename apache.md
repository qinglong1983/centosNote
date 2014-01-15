## CentOS 学习笔记 ##

###1.1 Apache服务器简介###

**Apache服务器** 是一个非常优秀的web服务器,目前是世界使用排名第一的Web服务器软件。  
**Apache服务器**的官方网站是[http://httpd.apache.org](http://httpd.apache.org)。  
**Apache服务器**名字比较长，以下文章默认使用**Apache**代替**Apache服务器**这个名字。

###1.2 检查Apache的安装情况 ###

查看是否有编译安装。Apache服务器的进程名称为httpd。

    find / -name httpd

如果找不到的话，可是试着使用下面的命令。

    whereis httpd

查看是否有RPM包安装

    rpm -qa | grep httpd

###1.3 卸载已有的安装 ###



###1.4 安装Apache ###
1. 使用yum安装

		yum install httpd

2. 编译安装

		TODO:

###1.5 Apache基本操作###

1. 系统在引导时启动**Apache**

		chkconfig --levels 235 httpd on

2. 启动**Apache**

		/etc/init.d/httpd start
	
	或者

		service httpd start 

3. 重新启动**Apache**

		/etc/init.d/httpd restart

	或者
	
		service httpd restart


4. 停止**Apache**
	
		/etc/init.d/httpd stop

	或者
	
		service httpd stop

5. 查看**Apache**进程

		ps aux | grep httpd

6. 首次验证**Apache**已经启动

		打开您的浏览器到http：//127.0.0.1，你应该看到Apache2的测试页

7. **Apache**文档存放位置

		Apache的默认文档根目录是在 /var/www/html
		配置文件是   /etc/httpd/conf/httpd.conf
		配置存储在的 /etc/httpd/conf.d/目录
		Apache默认监听在80端口
