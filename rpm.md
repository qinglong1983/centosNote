## CentOS 学习笔记 ##
==========
###RPM包下载###
1. [http://rpm.pbone.net](http://rpm.pbone.net)
2. [http://pkgs.org](http://pkgs.org)   
这个网站要好一些，操作系统做了归类,可以通过选择操作系统对应的RPM包下载。

###RPM包工具常用命令###

1. 查找当前是否安装了xxxx.rpm包程序及程序的版本  

		rpm –qa | grep xxxx

2. 全新安装程序
		
		rpm –ivh xxxxx.rpm

3. 升级程序

		rpm –Uvh xxxx.rpm

4. 删除程序

		rpm –e xxxxx

###RPM包安装常见问题###
安装rpm包软件常见的问题是安装时会遇到需要依赖包，从而导致没有办法安装当前的软件，只能把包有的依赖包都安装上才能完成安装。   
特别是一个新装的系统，因为系统太干净，没有安装一些基本的小工具。