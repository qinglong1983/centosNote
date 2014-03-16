一、查看是否安装 VNC

6.0 以后VNC名字 由 vnc 改成  tigervnc

	rpm -qa|grep tigervnc
	如果有的话会出现类似下面的内容
	tigervnc-1.0.90-0.17.20110314svn4359.el6.x86_64
	tigervnc-server-1.0.90-0.17.20110314svn4359.el6.x86_64

如果没有就安装下了 

	sudo yum install tigervnc tigervnc-server

添加启动项

	sudo chkconfig --add vncserver
	sudo chkconfig vncserver on

二、设置 VNC 密码 

	vncserver
	显示下面的内容
	Creating default startup script /root/.vnc/xstartup
	Starting applications specified in /root/.vnc/xstartup
	Log file is /root/.vnc/xen:1.log

	会在当前用户主目录下 生成 .vnc  目录和配置文件

	vncpasswd 
	Password:
	Verify:

设置的密码保存在  /root/.vnc/passwd 

三、VNC 配置 

修改 xstartup 文件 把最后的 twm & 删掉 加上 gnome-session & 

	cd /root/.vnc/
	tail -n 3 xstartup 
	xsetroot -solid grey
	xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
	gnome-session &

如果直接 启动

	/etc/init.d/vncserver start

正在启动 VNC 服务器：
no displays configured                [失败]

所以要修改  /etc/sysconfig/vncservers 文件添加以下内容

VNCSERVERS="2:root"

# 桌面号:用户    监听 590* 端口

VNCSERVERARGS[2]="-geometry 800x600"

这样修改后，就算 /etc/inittab 启动模式为 3  也可以正常进入图形界面

启动 vncserver
[root@xen ~]# /etc/init.d/vncserver start
正在启动 VNC 服务器：2:root xauth: (stdin):1:  bad display name "xen:2" in "add" command

New 'xen:2 (root)' desktop is xen:2

Starting applications specified in /root/.vnc/xstartup
Log file is /root/.vnc/xen:2.log