## CentOS 学习笔记 ##
CentOS（Community Enterprise Operating System）是Linux发布版之一，它是来自于Red Hat Enterprise Linux依照开放源代码规定发布的源代码所编译而成。  
CentOS的官方网站是[http://www.centos.org](http://www.centos.org)。  
下载地址为[http://www.centos.org/download/](http://www.centos.org/download/)。
我们点击download now按钮，进入CentOS下载列表。   
然后我们从其中一个下载点下载CentOS-6.5-x86_64-bin-DVD1.iso   
一般来说，DVD1包含了大部分的CentOS软件，安装系统一般用第一张就可以了。 
如果不确定自己用哪些软件，就下载两张DVD。   

注意点  
1. 安装CentOS 系统的计算机内存必须等于或者大于628M(最小内存628M)，才能启用图形安装模式   
3. CentOS文本安装模式不支持自定义分区，建议使用图形安装模式安装  
4. CentOS的系统安装方式分为：图形安装模式和文本安装模式  
5. CentOS的系统运行方式分为：带图形界面、可以用鼠标操作的图形化方式和不带图形界面、直接用命令行操作的文本方式(具体的系统运行方式，可以在系统安装的过程中自定义选择)   

下载完iso文件后，我们可以安装一个虚拟机，然后在虚拟机上安装CentOS来做练习。   


开机，在Bios设置为从光盘启动以后，我们可以看到下面的界面。

  ![Centos安装](/img/CentOSInstall001.jpg)

###界面说明###
- Install or upgrade an existing system **安装或升级现有的系统**  
- install system with basic video driver **安装过程中采用 基本的显卡驱动**  
- Rescue installed system **进入系统修复模式**  
- Boot from local drive **退出安装从硬盘启动**  
- Memory test **内存检测**  

这里我们选择第一项就好了，安装或升级现有的系统，回车。  

![Centos安装](/img/CentOSInstall002.jpg)


随后画面跳出是否对光盘进行检测的提问框，这里用键盘左右键选择“Skip”，然后回车跳过测试。   
一般来说不会有问题，除非你下载的光盘出现了问题。


![Centos安装](/img/CentOSInstall003.jpg)

出现安装界面，这里直接点击下一步

![Centos安装](/img/CentOSInstall004.jpg)

这个画面询问你在安装过程中喜欢使用哪种语言，我们当然选择中文(简体)

![Centos安装](/img/CentOSInstall005.jpg)

这个画面选择键盘，我们一般使用的是美式键盘，选择美国英语就可以了

![Centos安装](/img/CentOSInstall006.jpg)

下面是选择存储设备的界面，我们选择基本存储设备

![Centos安装](/img/CentOSInstall007.jpg)

为我们的计算机取一个名字，这里我选择了camus

![Centos安装](/img/CentOSInstall008.jpg)

时钟选择画面，我们选择亚洲上海，并取消“系统时钟使用UTC时间”前面的勾

![Centos安装](/img/CentOSInstall009.jpg)

这里我们需要输入root用户的密码,root在英文中是根的意思，所以这里叫做根用户。    
密码最好复杂点，可以用一句你喜欢的歌词首字母，加上你的幸运数字代表的符号等等。  
当然，你得记住了，不然就是悲剧。  

![Centos安装](/img/CentOSInstall010.jpg)

下一步是分区，我们选择自定义布局

![Centos安装](/img/CentOSInstall011.jpg)
这里出现了已经有了系统和分区，我选择全部删除。

![Centos安装](/img/CentOSInstall012.jpg)
我们看到这里总共有40G空间，我们点击创建，创建一个标准分区。

![Centos安装](/img/CentOSInstall013.jpg)

这里我们创建一个/分区，大小为20G，并强制为主分区。
/分区的作用我们后续再介绍。

然后我们再创建一个swap分区，大小为4096M，也就是4G

![Centos安装](/img/CentOSInstall014.jpg)
然后我们创建一个/hd分区，大小为

![Centos安装](/img/CentOSInstall015.jpg)
最后我们的分区情况如上。

对于分区的创建，这里我们解释一下。   

- / 分区为 20G,用来存放系统的安装文件。 

 
- swap分区为4G，用作CentOS的交换文件。     
当内存不够的时候，CentOS会选择把一部分内存内容存放到这个交换分区中。  
这里很多人都说需要设置为内存的两倍，当内存较少的时候，的确是这样。     
不过内存到了48G这样，这里实际上可以设置得少一点。    

- /hd分区为我自己定义的名字，存放我的数据文件，程序文件，等等杂七杂八的资料。     
		hd的意思取名为hardDisk，硬盘的意思。      
		因为其实系统盘存放系统文件，虽然他是硬盘的一部分，但是并不能为我所使用，所以我这里单独分一个区，用来存放我自己的文件。     
		注意，/XXX中的XXX有些名字系统已经用了，所以最好不要重名。   
		关于CentOS默认的目录结构，我们后续介绍。   

 
> 用于正式生产的服务器，切记必须把数据盘单独分区，防止系统出问题时，保证数据的完整性。    
> 比如可以再划分一个/data专门用来存放数据。  
> 我这里就是单独划分一个/hd用来存放自己的东西。


![Centos安装](/img/CentOSInstall016.jpg)

这个界面点击下一步就好

![Centos安装](/img/CentOSInstall017.jpg)

然后到了我们选择CentOS安装类型的时候。
这里的选项有

- Desktop 桌面
- Minimal Desktop 最小桌面
- Minimal 最小
- Basic Server 基础服务器
- Database Server 数据库服务器
- Web Server web服务器
- Virtual Host 虚拟主机
- Software Development Workstation 软件开发工作站

这里我们选哪个呢，如果你不是程序员，选桌面。  
是程序员，选择软件开发工作站。  
其它的先不要管，后续如果正的是开发环境，我想你学完了这本书，也知道该如何选择了。  

![Centos安装](/img/CentOSInstall018.jpg)

点击下一步，开始启动安装了  
安装完成之后，重新启动  
我们会看到下面的界面  

![Centos安装](/img/CentOSInstall019.jpg)

我们按下回车键，系统就会启动了

![Centos安装](/img/CentOSInstall020.jpg)
最后输入我们的用户名和密码进行登录。