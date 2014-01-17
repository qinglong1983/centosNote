###rebootCause###

####系统如果存在重启的现象，可以通过下面的命令来进行查看####

  

####1.查看最后重启的时间####

	last reboot

可以看到正常命令重启显示为down，而电源强制重启为crash。

####2.查看最近用户登录情况####

	last

####3.查看操作系统的历史命令####
	
	history |more

####4.查看日志信息####

	cat /var/log/messages |more
