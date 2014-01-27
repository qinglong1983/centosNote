在安装lua到make linux的时候出现以下错误：  
在包含自 lua.h：16 的文件中，  
从 lua.c：15:  
luaconf.h:275:31: 错误：readline/readline.h：没有那个文件或目录  
luaconf.h:276:30: 错误：readline/history.h：没有那个文件或目录  
lua.c: In function ‘pushline’:  
lua.c:182: 警告：隐式声明函数 ‘readline’  
lua.c:182: 警告：赋值时将整数赋给指针，未作类型转换  
lua.c: In function ‘loadline’:  
lua.c:210: 警告：隐式声明函数 ‘add_history’  
make[2]: *** [lua.o] 错误 1  
make[2]: Leaving directory `/data0/software/lua-5.1.4/src’  
make[1]: *** [linux] 错误 2  
make[1]: Leaving directory `/data0/software/lua-5.1.4/src’     
make: *** [linux] 错误 2  
解决方法：  

yum install libtermcap-devel ncurses-devel libevent-devel readline-devel