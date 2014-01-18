## CentOS 学习笔记 ##
==========
###常用工具###
####1.文件传输工具lrzsz####  
下载rpm包，然后安装    

	rpm –ivh lrzsz-xxx.rpm

####2.zip包工具####
下载zip和unzip的rpm

	rpm –ivh zip-xxx.rpm
	rpm –ivh unzip-xxx.rpm

####3.gcc编译器####
gcc 需要安装gcc、libgcc、gcc-c++三个rpm包

	rpm –ivh gcc-xxx.rpm
	rpm –ivh libgcc -xxx.rpm
	rpm –ivh gcc-c++-xxx.rpm

####4.安装中文支持####

	yum groupinstall chinese-support

####5.用文本方式启动####
	
	编辑/etc/inittab
	找到 id:initdefault
	将该句的5改为3
	重启之后，CentOS就会自动进入字符界面

####6.设置语言显示####

	CentOS 默认的语言编码是zh_CN.UTF-8
	在x-windows上是正常的，但是用SSH或者Telnet连接的时候
	所有的汉字会变成乱码
	解决方法是
	编辑文件 /etc/sysconfig/i18n
	将第一句
	LANG="zh_CN.UTF-8"
	修改为
	LANG="zh_CN.GB18030"


	
