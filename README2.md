#### ��1�� ./configure-android ����
> ./configure-android:/bin/sh^M:bad interpreter:No such file or directory  

ԭ�����ǲ�ͬϵͳ�����ʽ����ģ���windowsϵͳ�б༭�ġ�sh�ļ������в��ɼ��ַ���������Linuxϵͳ��ִ�лᱨ�����쳣��

```hell
# �鿴�ļ���ʽ
set ff ���� set fileformat
# ���Կ���������Ϣ��
fileformat=dos��fileformat=unix

# ����
set ff=unix �� set fileformat=unix
# ok�������
```

#### ��2�� ./configure ����

> ./configure-android: 168: ./configure-android: ./configure: Permission denied  

./configure-android���һ������./configure
������Ϊconfigureû��ִ��Ȩ��

#### ��3�� ./aconfigure ����

>  ./aconfigure: Permission denied  

./configure �ڲ�����ִ��./aconfigure �ű�
Ҳ��û��ִ��Ȩ�� `chmod a+x` ���

#### ��4���޸�Ŀ¼��ȫ���ļ��ĸ�ʽ
```shell
find . -type f -exec dos2unix {} \;
# ע�� ==> {û�пո�}�ո�\;
```

#### ��5��\*** missing separator. stop.
```shell
make clean && make distclean 
find . -type f -name '.*.depend*' -exec rm {} \;
```
������У����±��루����FAQ��ô˵�ģ�

#### ��6��portaudio.h: No such file or directory
> portaudio.h: No such file or directory
> \# include  portaudio.h  

```shell
# ����pjlib/include/pj/config_site.h���������������
#define PJ_CONFIG_ANDROID 1
#include <pj/config_site_sample.h>
```

#### ��7������ʾ�����̳���==>UnsatisfiedLinkError exception with "cannot locate 'rand'" message
> Exception Ljava/lang/UnsatisfiedLinkError; thrown while initializing Lorg/pjsip/pjsua2/app/MyApp;
...
java.lang.UnsatisfiedLinkError: Cannot load library: reloc_library[1285]:    37 cannot locate 'rand'...  

ԭ�� [http://stackoverflow.com/a/27338365/3355097](http://stackoverflow.com/a/27338365/3355097)
������[http://stackoverflow.com/a/27346821/3355097](http://stackoverflow.com/a/27346821/3355097)

