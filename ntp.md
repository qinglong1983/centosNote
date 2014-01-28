我们在安装完Centos Linux操作系统之后，点击系统的时间发现与现在所使用的时间不一致，相差有8小时。

而在安装系统的时候我们选择的时区是上海，但是CentOS Linux默认的bios时间是utc时间(UTC是协调世界时(Universal Time Coordinated)英文缩写，是由国际无线电咨询委员会规定和推荐,并由国际时间局(BIH)负责保持的以秒为基础的时间标度。

UTC相当于本初子午线(即经度0度)上的平均太阳时，过去曾用格林威治平均时(GMT)来表示.北京时间比UTC时间早8小时，以1999年1月1日0000UTC为例，UTC时间是零点，北京时间为1999年1月1日早上8点整。)，所以我们在时间上面相隔了8个小时。这个时候bios的时间和系统的时间当然是不一致，一个代表 utc 时间，一个代表cst（＋8时区），即上海的时间。

让我们动手将操作系统的时间进行同步吧!

在CentOS Linux中终端命令中执行以下命令：

1、vi /etc/sysconfig/clock   #编辑时间配置文件

     ZONE="Asia/Shanghai"
     UTC=false          #设置为false，硬件时钟不于utc时间一致
2、linux的时区设置为上海时区

	ln -sf /usr/share/zoneinfo/Asia/Shanghai    /etc/localtime	

3、对准时间

	ntpdate  cn.pool.ntp.org    

如果没有安装ntp服务器，刚需要先执行以下命令：

	yum install ntp #安装ntp服务器

4、#设置硬件时间和系统时间一致并校准

	/sbin/hwclock --systohc   