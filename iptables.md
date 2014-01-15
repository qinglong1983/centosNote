## CentOS 学习笔记 ##

###打开iptables的配置文件###
 
	vi /etc/sysconfig/iptables  

如果我们用来做网站服务器，那么需要打开80端口。 

我们在控制台敲入

	/etc/init.d/iptables status

命令查询是否有打开80端口。

如果没有可通过两种方式处理：

1.修改vi /etc/sysconfig/iptables命令添加使防火墙开放80端口

	-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT  
 
2.关闭防火墙
	
	/etc/init.d/iptables stop  
 
3.永久性关闭防火墙
	
	chkconfig --level 35 iptables off  
 
	/etc/init.d/iptables stop  
 
	iptables -P INPUT DROP  
 
4.打开主动模式21端口
	
	iptables -A INPUT -p tcp --dport 21 -j ACCEPT  
 
5.打开被动模式49152~65534之间的端口
	
	iptables -A INPUT -p tcp --dport 49152:65534 -j ACCEPT  
 
	iptables -A INPUT -i lo -j ACCEPT  
 
	iptables -A INPUT -m state --state ESTABLISHED -j ACCEPT  
 

注意：

一定要给自己留好后路,留VNC一个管理端口和SSh的管理端口

需要注意的是，你必须根据自己服务器的情况来修改这个文件。

全部修改完之后重启iptables:

	service iptables restart

你可以验证一下是否规则都已经生效：

iptables -L
