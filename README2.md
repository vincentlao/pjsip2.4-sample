#### （1） ./configure-android 出错
> ./configure-android:/bin/sh^M:bad interpreter:No such file or directory  

原因：这是不同系统编码格式引起的：在windows系统中编辑的。sh文件可能有不可见字符，所以在Linux系统下执行会报以上异常。

```hell
# 查看文件格式
set ff 或者 set fileformat
# 可以看到如下信息：
fileformat=dos或fileformat=unix

# 更改
set ff=unix 或 set fileformat=unix
# ok，解决。
```

#### （2） ./configure 出错

> ./configure-android: 168: ./configure-android: ./configure: Permission denied  

./configure-android最后一步就是./configure
那是因为configure没有执行权限

#### （3） ./aconfigure 出错

>  ./aconfigure: Permission denied  

./configure 内部就是执行./aconfigure 脚本
也是没有执行权限 `chmod a+x` 解决

#### （4）修改目录先全部文件的格式
```shell
find . -type f -exec dos2unix {} \;
# 注意 ==> {没有空格}空格\;
```

#### （5）\*** missing separator. stop.
```shell
make clean && make distclean 
find . -type f -name '.*.depend*' -exec rm {} \;
```
清空所有，重新编译（官网FAQ这么说的）

#### （6）portaudio.h: No such file or directory
> portaudio.h: No such file or directory
> \# include  portaudio.h  

```shell
# 创建pjlib/include/pj/config_site.h，并添加以下内容
#define PJ_CONFIG_ANDROID 1
#include <pj/config_site_sample.h>
```

#### （7）运行示例工程出错==>UnsatisfiedLinkError exception with "cannot locate 'rand'" message
> Exception Ljava/lang/UnsatisfiedLinkError; thrown while initializing Lorg/pjsip/pjsua2/app/MyApp;
...
java.lang.UnsatisfiedLinkError: Cannot load library: reloc_library[1285]:    37 cannot locate 'rand'...  

原因： [http://stackoverflow.com/a/27338365/3355097](http://stackoverflow.com/a/27338365/3355097)
方案：[http://stackoverflow.com/a/27346821/3355097](http://stackoverflow.com/a/27346821/3355097)

