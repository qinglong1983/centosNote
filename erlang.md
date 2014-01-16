## CentOS 学习笔记 ##
==========
安装Erlang
Erlang版本是R16B02。 

在安装之前，需要先要安装一些其他的软件，否则在安装中间会出现一些由于没有其依赖的软件模块而失败。 
###安装依赖###
####1. 首先要先安装GCC GCC-C++ Openssl等以来模块####
	
	yum -y install make gcc gcc-c++ kernel-devel m4 ncurses-devel openssl-devel  
 
####2. 再安装ncurses模块####
	
	yum -y install ncurses-devel  
	yum install ncurses-devel  

####3.下载和解压####
   
- 下载Erang源代码文件文件，并对其付权限和解压文件：

		wget http://www.erlang.org/download/otp_src_R16B02.tar.gz
		chmod +x otp_src_R16B02.tar.gz  
		tar -xzvf otp_src_R16B02.tar.gz  
		mv otp_src_R16B02  erlang_R16B #重命名解压厚的文件  
 
- 编译和安装

		cd erlang_R16B/
		进入erlang_R16B目录
  
		./configure --prefix=/usr/local/erlang --with-ssl --enable-threads --enable-smp-support --enable-kernel-poll --enable-hipe --without-javac  
		//不用java编译，故去掉java避免错误  
		
		make && make install 
		//编译和安装  