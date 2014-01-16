## CentOS 学习笔记 ##
==========
###1. 安装JDK###
Linux下的JDK安装文件，一般都是.bin的文件，如我们公司的环境用的JDK是1.5的，我下载的是java_ee_sdk-5_01-linux.bin文件。

将文件上传到服务器上，通./java_ee_sdk-5_01-linux.bin就可以进行安装了，安装过程中需要接受安装协议才能进行。

	[root@localhost ~]# ./java_ee_sdk-5_01-linux.bin



> 注：java_ee_sdk-5_01-linux.bin文件需要有可执行权限，chmod 700 java_ee_sdk-5_01-linux.bin

###2. 配置环境变量###
安装完成后，还需要配置环境变量，在/etc/profile.d/下添加java.sh文件，这样所有用户都可以共享这个配置。这样配置的坏处是，如果后期添加了其它版本的JDK，就不方便配置了。

	[root@localhost ~]# vi /etc/profile.d/java.sh

Java.sh文件内容：

	#set java environment 
	export JAVA_HOME=/usr/java/jdk1.5/jdk
	export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib 
	export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH

###3. 测试###
然后写一个java文件测试一下，看看是否能运行，这个就不再多啰嗦了。