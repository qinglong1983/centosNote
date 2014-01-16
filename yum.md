###yum 命令工具使用举例###
####1、升级系统####

	[root@localhost ~]#yum update

####2、安装指定的软件包

	[root@localhost ~]# yum -y install mysql-server

####3、升级指定的软件包

	[root@localhost ~]# yum -y update mysql

####4、卸载指定的软件包

	[root@localhost ~]# yum -y remore mysql

####5、查看系统中已经安装的和可用的软件组，对于可用的软件组，你可以选择安装
	
	[root@localhost ~]# yum grouplist

####6、安装上一个命令中显示的可用的软件组中的一个软件组
	
	[root@localhost ~]# yum -y groupinstall Emacs

####7、更新指定软件组中的软件包

	[root@localhost ~]# yum -y groupupdate Emacs

####8、卸载指定软件组中的软件包

	[root@localhost ~]# yum -y groupremove Emacs

####9、清除缓存中的rpm 头文件和包文件
	
	[root@localhost ~]# yum clean all

####10、搜索相关的软件包
	
	[root@localhost ~]# yum -y search Emacs

####11、显示指定软件包的信息
	
	[root@localhost ~]# yum info Emacs

####12、查询指定软件包的依赖包####

	[root@localhost ~]# yum deplist emacs

####13、列出所有以 yum 开头的软件包####
	
	[root@localhost ~]# yum list yum\*

####14、列出已经安装的但是不包含在资源库中的rpm 包####

	[root@localhost ~]# # yum list extras


####15、更换网易的yum源####
CentOS-6.4-x86_64-minimal
下载地址：http://mirrors.163.com/centos/6.4/isos/x86_64/CentOS-6.4-x86_64-minimal.iso
	
此系统为CD版本，所以基本是属于最小化安装版本。现将系统默认源更换成网易源。步骤如下：

1、下载新源及将本地源备份

	[root@localhost ~]# cd /etc/yum.repos.d/
	[root@localhost ~]# wget http://mirrors.163.com/.help/CentOS6-Base-163.repo
	[root@localhost ~]# mv CentOS-Base.repo CentOS-Base.repo.bak
	[root@localhost ~]# mv CentOS6-Base-163.repo CentOS-Base.repo

2、yum源更新

	[root@localhost ~]# yum clean all && yum makecache && yum update -y

3、完成。
