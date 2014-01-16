## CentOS 学习笔记 ##
==========
###安装Tomcat###
下载安装文件并上传到服务器，公司的系统都是用的tomcat 5.x的版本。  
将apache-tomcat-5.5.33.tar.gz放到自己想安装的目录下，再解压出来。  

	[root@localhost tomcat]# gunzip apache-tomcat-5.5.33.tar.gz
	[root@localhost tomcat]# tar xvf apache-tomcat-5.5.33.tar

解压出来的文件就可以用了，到apache-tomcat-5.5.33/bin/目录里面执行startup.sh文件进行测试。  

	[root@localhost bin]# ./ startup.sh

如果没有问题的话会打印出一些环境变量的值来，有问题刚需要去配置相关的环境变量，主要是java的环境变量