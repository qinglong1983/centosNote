#云服务器安装#

##用户设置##

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

##安装查找软件##

		yum install mlocate  
		updatedb
		locate mysql.h




##安装apache##

		yum install apache

##安装php##
		
	yum install php

##安装rz##

	yum install lrzsz

##安装java##

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

##安装mysql##

	rpm -qa | grep -i mysql
	如果找到有mysql相关的库，先进行删除
	rpm -e --nodeps mysql-libs-5.1.61-4.el6.x86_64
	


##安装pocolib##

##安装wowza流媒体##

##支持C1000K##

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


####gcc安装####

	yum install gcc

####g++安装####
g++的名字叫做 gcc-c++

	yum install gcc-c++
 


