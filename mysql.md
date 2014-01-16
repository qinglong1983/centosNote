## CentOS 学习笔记 ##
==========
### 安装Mysql###
Mysql安装的时候可能会麻烦一些，因为其中会遇到系统中缺少包的问题，这样就需要不停的到网上去找相关的包来安装完成之后才能完成Mysql的安装。  
需要准备的包  
这一次用到如下的安装包：  

- MySQL-server-5.6.2_m5-1.rhel4.x86_64.rpm  
- MySQL-client-5.5.15-1.rhel4.x86_64.rpm（MySQL-client-5.6.2_m5-1.rhel4.x86_64.rpm）  
- MySQL-devel-5.5.15-1.rhel4.x86_64.rpm  
- MySQL-shared-5.5.15-1.rhel4.x86_64.rpm  
- libaio-0.3.105-2.x86_64.rpm

####1. 检查软件是否存在####
在安装之前，应该先检查系统里面是不是在安装系统时就安装了mysql。  

	[root@localhost ~]# rpm –qa | grep mysql

####2. 卸载老版本####
如果有的话，不是你想要我版本，那就只能强行卸载。

	[root@localhost ~]# rpm -e --nodeps mysql-*(相关的软件包)

卸载完相关软件之后，再进行安装。

####3.安装####
安装的时候可能会报错，缺少包，我安装的时候就缺少了libaio-0.3.105-2.x86_64.rpm，这样就只能安装了libaio-0.3.105-2.x86_64.rpm包再装mysql。

	[root@localhost ~]# rpm –i MySQL-server-5.6.2_m5-1.rhel4.x86_64.rpm

测试
安装完成后，需要测试是否可用了。

	[root@localhost ~]# mysql

如果能够成功登录，则说明安装成功了，安装成功后，root是密码为空的，为了安全，需要改密码。 

	[root@localhost ~]# /usr/bin/mysqladmin -u root password 'xxxxxx';

服务相关命令

检查服务状态

	[root@localhost ~]# /etc/rc.d/init.d/mysql status

启动服务

	[root@localhost ~]# /etc/rc.d/init.d/mysql start

停止服务

	[root@localhost ~]# /etc/rc.d/init.d/mysql stop

添加到系统自动启动服务列表中

	[root@localhost ~]# chkconfig –add mysql