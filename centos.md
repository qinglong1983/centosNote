## CentOS 学习笔记 ##
CentOS（Community Enterprise Operating System）是Linux发布版之一，它是来自于Red Hat Enterprise Linux依照开放源代码规定发布的源代码所编译而成。  
CentOS的官方网站是[http://www.centos.org](http://www.centos.org)

1. CentOS 6.3系统镜像有两个，安装系统只用到第一个镜像即CentOS-6.3-i386-bin-DVD1.iso(32位)或者CentOS-6.3-x86_64-bin-DVD1.iso(64位),第二个镜像是系统自带软件安装包
2. 安装CentOS 6.3系统的计算机内存必须等于或者大于628M(最小内存628M)，才能启用图形安装模式
3. CentOS 6.3文本安装模式不支持自定义分区，建议使用图形安装模式安装
4. CentOS 6.3的系统安装方式分为：图形安装模式和文本安装模式
5. CentOS 6.3的系统运行方式分为：带图形界面、可以用鼠标操作的图形化方式和不带图形界面、直接用命令行操作的文本方式(具体的系统运行方式，可以在系统安装的过程中自定义选择)

###界面说明###
  
- Install or upgrade an existing system **安装或升级现有的系统**  
- install system with basic video driver **安装过程中采用 基本的显卡驱动**  
- Rescue installed system **进入系统修复模式**  
- Boot from local drive **退出安装从硬盘启动**  
- Memory test **内存检测**  


这里选择第一项，安装或升级现有的系统，回车。  
出现是否对CD媒体进行测试的提问，这里选择“Skip”跳过测试。

取消“系统时钟使用UTC时间”前面的勾

架设硬盘总共5G  
/ 4G,/就是根目录，这里表示为根目录分配4G的空间。    
Swap 1G(内存小于2G时，设置为内存的2倍;内存大于或等于2G时，设置为2G)  
swap是交换分区  
特别说明：  
> 用于正式生产的服务器，切记必须把数据盘单独分区，防止系统出问题时，保证数据的完整性。    
> 比如可以再划分一个/data专门用来存放数据。

   