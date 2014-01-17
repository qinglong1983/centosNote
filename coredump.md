###打开core dump文件开关###

####1. 什么是dump####
dump文件可以在程序crash时，方便我们查看程序crash的地方和上下文信息。   
在window下，要能生成dump文件，需要自己编写相应的代码。   
 
在linux下面就简单的许多。只要打开相应的开关，linux会自动在程序crash时生成相应的core文件。   
这个文件和window下的dump文件类似。
 
####2.操作步骤####
#####1.查看当前是否已经打开了此开关#####
通过命令：ulimit -c 如果输出为 0 ，则代表没有打开。  
如果为unlimited则已经打开了,就没必要在做打开。  

#####2.通过命令打开#####

	ulimit -c unlimited 

然后通过步骤1，可以监测是否打开成功。

#####3.取消coredump#####
	
	ulimit -c 0 

#####4.永久生效####
通过上面的命令修改后，一般都只是对当前会话起作用，当你下次重新登录后，还是要重新输入上面的命令，所以很麻烦。

我们可以把通过修改 /etc/profile文件 来使系统每次自动打开。

步骤如下：
1.首先打开/etc/profile文件   
一般都可以在文件中找到这句语句：
ulimit -S -c 0 > /dev/null 2>&

根据上面的例子，我们只要把那个0 改为 unlimited 就ok了。然后保存退出。

2.通过source /etc/profile 使当期设置生效。

3.通过ulimit -c 查看下是否已经打开。

其实不光这个命令可以加入到/etc/profile文件中，一些其他我们需要每次登录都生效的都可以加入到此文件中，因为登录时linux都会加载此文件。比如一些环境变量的设置。
还有一种方法可以通过修改/etc/security/limits.conf文件来设置，这个方法没有试过，也是网上看到。不过上面两种就可以了！



> 最后说一下生成core dump文件的位置，默认位置与可执行程序在同一目录下，文件名是core.***，其中***是一个数字。  
> core dump文件名的模式保存在/proc/sys/kernel/core_pattern中，缺省值是core。   
> 通过以下命令可以更改core dump文件的位置(如希望生成到/tmp/cores目录下)   
echo “/tmp/cores/core” > /proc/sys/kernel/core_pattern

设置完以后我们可以做个测试，写个程序，产生一个异常。  
我们会看到当前目录会有个core*的文件。  
输入gdb core。***程序进行调试。



###小程序产生 core dump###

	#include <stdio.h>
	
	int main()
	{
	    int *null_ptr = NULL;
	    *null_ptr = 10;            //对空指针指向的内存区域写,会发生段错误
	    return 0;
	}