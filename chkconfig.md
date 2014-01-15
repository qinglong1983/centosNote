## CentOS 学习笔记 ##

###chkconfig 命令###

用来更新和查询不同运行级上的系统服务

简单地说，比如你安装了mysql，并且你把启动的脚本放在了/etc/rc.d/init.d目录下，有时候你需要开机自动启动它，而有时候则不需要。

我们就可以使用chkconfig命令来进行控制，这个命令就相当于一个开关。

不过这个开关有6个档，表示在不同级别下的运行状态是on还是off。

语法解释 ：

- chkconfig --list [name]  列表服务
- chkconfig --add  [name]   添加服务
- chkconfig --del  [name]   删除服务
- chkconfig [--level levels] name <on|off|reset>  改变启动信息以及检查特定服务的启动状态。
on 和 off 分别指服务在改变运行级时的启动和停止，reset 指初始化服务信息。
对于 on 和 off 开关，系统默认只对运行级 3，4， 5有效，但是 reset 可以对所有运行级有效。

选项介绍 ： 
--level levels 指定运行级，由数字 0 到 7 构成的字符串，如：
--level 35 表示指定运行级3 和5。 
--add name 增加一项新的服务。

chkconfig 确保每个运行级有一项 启动(S) 或者 杀死(K) 入口。如有缺少，则会从缺省的init脚本自动建立。 

--del name  删除服务，并把相关符号连接从 /etc/rc[0-6].d 删除。 

--list name 查看列表，如果指定了name 那么只是显示指定的服务名，否则，列出全部服务在不同运行级的状态。 

运行级文件 ：
每个被chkconfig 管理的服务需要在对应的/etc/rc.d/init.d 下的脚本加上两行或者更多行的注释。
第一行告诉 chkconfig 缺省启动的运行级以及启动和停止的优先级。如果某服务缺省不在任何运行级启动，那么使用 - 代替运行级。
      第二行对服务进行描述，可以用\ 跨行注释。 

例如，random.init 包含三行：
	
	chkconfig: 2345 20 80 
	description: Saves and restores system entropy pool for 
	higher quality random number generation.
 
表明 random 脚本应该在运行级 2, 3, 4, 5 启动，启动优先权为20，停止优先权为 80。

###关闭Linux系统下不必要的服务###

chkconfig --list 显示。 

chkconfig [service] off 关闭其中一个服务。 

守候进程名字功能对照表。 

amd：自动安装NFS（网络文件系统）守侯进程。 

apmd:高级电源管理。 

Arpwatch：记录日志并构建一个在LAN接口上看到的以太网地址和IP地址对数据库。 

Autofs：自动安装管理进程automount，与NFS相关，依赖于NIS。 

Bootparamd：引导参数服务器，为LAN上的无盘工作站提供引导所需的相关信息。 

crond：Linux下的计划任务。 

Dhcpd：启动一个DHCP（动态IP地址分配）服务器。 

Gated：网关路由守候进程，使用动态的OSPF路由选择协议。 

Httpd：WEB服务器。 

Inetd：支持多种网络服务的核心守候程序。 

Innd：Usenet新闻服务器。 

Linuxconf：允许使用本地WEB服务器作为用户接口来配置机器。 

Lpd：打印服务器。 

Mars-nwe：mars-nwe文件和用于Novell的打印服务器。 

Mcserv：Midnight命令文件服务器。 

named：DNS服务器。 

netfs：安装NFS、Samba和NetWare网络文件系统。

network：激活已配置网络接口的脚本程序。 

nfs：打开NFS服务。 

nscd：nscd(Name

Switch Cache daemon)服务器，用于NIS一个支持服务，它高速缓存用户口令和组成成员关系。 

portmap：RPC

portmap管理器，与inetd类似，它管理基于RPC服务的连接。 

postgresql：一种SQL数据库服务器。 

routed：路由守候进程，使用动态RIP路由选择协议。 

rstatd：一个为LAN上的其它机器收集和提供系统信息的守候程序。 

ruserd：远程用户定位服务，这是一个基于RPC的服务，它提供关于当前记录到LAN上一个机器日志中的用
户信息。 

rwalld：激活rpc.rwall服务进程，这是一项基于RPC的服务，允许用户给每个注册到LAN机器的其他终端写消息。 

rwhod：激活rwhod服务进程，它支持LAN的rwho和ruptime服务。 

sendmail：邮件服务器sendmail。 

smb：Samba文件共享/打印服务。 

snmpd：本地简单网络管理候进程。 

squid：激活代理服务器squid。 

syslog：一个让系统引导时起动syslog和klogd系统日志守候进程的脚本。 

xfs：X

Window字型服务器，为本地和远程X服务器提供字型集。 

xntpd：网络时间服务器。 

ypbind：为NIS（网络信息系统）客户机激活ypbind服务进程。 

yppasswdd：NIS口令服务器。 

ypserv：NIS主服务器。 

gpm：管鼠标的。 

identd：AUTH服务，在提供用户信息方面与finger类似。
 
###Linux chkconfig命令使用范例###

列出所有的系统服务
	
	chkconfig --list      

增加httpd服务

	chkconfig --add httpd 

删除httpd服务

	chkconfig --del httpd 

设置httpd在运行级别为2、3、4、5的情况下都是on（开启）的状态

	chkconfig --level httpd 2345 on 

列出系统所有的服务启动情况

	chkconfig --list 

列出mysqld服务设置情况
	
	chkconfig --list mysqld

设定mysqld在等级3和5为开机运行服务，--level35表示操作只在等级3和5执行，on表示启动，off表示关闭

	chkconfig --level 35 mysqld on

设定mysqld在各等级为on，“各等级”包括2、3、4、5等级
	
	chkconfig mysqld on

###Linux chkconfig命令如何增加一个服务###

1. 服务脚本必须存放在/etc/ini.d/目录下;
2. 在chkconfig工具服务列表中增加此服务，(使用chkconfig--add servicename),此时服务会被在/etc/rc.d/rcN.d中赋予K/S入口了;
3. chkconfig --level 35 mysqld on 修改服务的默认启动等级。