# 云服务器安装 #

## 用户设置 ##

1. 查看系统里所有用户
 
    	cat /etc/passwd

	
	如果第三个参数为:500以上的,就是新建用户.  
    其它则为系统的用户.
	
	列出所有用户  
			
		cat /etc/passwd |cut -f 1 -d :

	列出新建的用户

		cat /etc/passwd | grep 500 |cut -f 1 -d :

2. 添加用户，修改用户密码

		passwd 用户名 (修改密码)
		useradd 用户名 (添加用户)

3. ssh禁止root直接登录和修改端口号

		vi /etc/ssh/sshd_config
		修改 PermitRootLogin yes 为no
		修改Port 22 为 8888
		修改完成后需要重新启动
		/etc/init.d/sshd restart

## 安装查找软件 ##

		yum install mlocate  
		updatedb
		locate mysql.h

## 安装apache ##

		yum install apache

## 安装php ##
		
	yum install php

## 安装rz ##

	yum install lrzsz

## 安装java ##

	下载绿色版本jdk的tar包
	拷贝并解压缩到 /usr/local中
	/usr/local/jdk1.7.0_51

	配置环境变量
	vi /etc/profile
	在profile文件下面追加写入下面信息：
	export JAVA_HOME=/usr/local/jdk1.7.0_51
	export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
	export PATH=$PATH:$JAVA_HOME/bin
	
	保存退出，执行

	source /etc/profile
	
	创建符号链接
	因为wowza流媒体需要这个链接，所以我们需要创建一个
	ln -sf /usr/local/jdk1.7.0_51/bin/java /usr/bin/java

## 安装mysql ##
首先，为了保证安装成功，我们需要删除以前的mysql

	rpm -qa | grep -i mysql
	如果找到有mysql相关的库，先进行删除
	rpm -e --nodeps mysql-libs-5.1.61-4.el6.x86_64

然后，我们使用repo方式进行安装，先必须安装repo
	
	打开http://dev.mysql.com/downloads/repo/  
从这里下载对应的版本,我们目前下载的是

	mysql-community-release-el6-5.noarch.rpm
	CentOS 6 对应的是 Redhat6的
	sudo yum localinstall mysql-community-release-el6-5.noarch.rpm

使用yum安装mysql

		sudo yum install mysql-server

开始和停止mysql服务

		开始mysql服务
		sudo service mysqld start

		检查mysql状态
		sudo service mysqld status

		停止mysql服务
		sudo service mysqld stop
	
## 安装odbc ##
因为pocolib依赖这个，所以我们需要先安装odbc  

	sudo yum install unixODBC unixODBC-devel libtool-ltdl libtool-ltdl-devel
	sudo yum install mysql-connector-odbc

## 安装pocolib ##

	yum --enablerepo=base install openssl-devel
	wget http://pocoproject.org/releases/poco-1.4.6/poco-1.4.6p4-all.tar.gz
	tar -zxvf poco-1.4.6p4-all.tar.gz
	./configure --omit=Data/ODBC,Data/MySQL
	make
	make install

## 安装wowza流媒体 ##

	

## 支持百万用户（C1000K） ##

1. 修改当前系统的全局最大打开文件数

		修改 /etc/sysctl.conf 文件:

		如果已经存在下面这些信息，则修改，没有则添加
		fs.file-max = 1020000
		net.ipv4.ip_conntrack_max = 1020000
		net.ipv4.netfilter.ip_conntrack_max = 1020000

		执行sysctl -p，使其生效

		查看大小改变
		cat /proc/sys/fs/file-nr
		5100	0	101747
		第三个数字就是当前系统的全局最大打开文件数,这里只有10万

2. 进程限制

		ulimit -n
		ulimit -n 1020000

		永久修改

		编辑 /etc/security/limits.conf 文件, 加入如下行:

		# /etc/security/limits.conf
		work         hard    nofile      1020000
		work         soft    nofile      1020000
		第一列的 work 表示 work 用户, 你可以填 *, 或者 root. 
		保存退出, 重新登录服务器.


### gcc安装 ###

	yum install gcc

### g++安装 ###
g++的名字叫做 gcc-c++

	yum install gcc-c++
 
##解压bz2文件##

	tar jxvf XX.tar.bz2
	如果tar不支持j选项，就用下面方式解压
	bzip2 -d  XX.tar.bz2
	tar -xvf  XX.tar.bz2
	
	
	
## mac连接linux ##
mac通过终端ssh远程连接centos服务器  
在终端下输入
  
	连接22端口
	ssh -l root ip地址      
	连接其他端口
	ssh -p 端口 -l 用户名 ip地址 
 
ssh 连接的时候 Host key verification failed. 
解决方法:
	
	vi ~/.ssh/known_hosts

进入此目录，删除与你相关rsa的信息即可.

或者删除这个文件
cd ~/.ssh/
rm known_hosts