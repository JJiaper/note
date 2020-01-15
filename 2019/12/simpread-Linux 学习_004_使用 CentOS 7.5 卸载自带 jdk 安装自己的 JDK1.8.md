> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 https://www.cnblogs.com/chenmingjun/p/9931593.html

**文章目录**

*   [一、安装环境](#_label0)
*   [二、安装步骤](#_label1)

> 本文主要介绍的是如何是 Linux 环境下安装 JDK 的，因为 Linux 环境下，很多时候也离不开 Java 的，下面笔者就和大家一起分享如何 jdk1.8 的过程吧。

[回到顶部](#_labelTop)

**一、安装环境**
----------

*   本机系统：Win 10
*   虚拟机软件：VMware PRO 14
*   虚拟机 Linux 系统：CentOS 7.5
*   JDK 版本：1.8.0_191
*   工具：SecureCRT
*   说明：本文是通过 SecureCRT 工具远程连接 Linux 操作，如果是直接在 Linux 可视化界面操作那就更方便了，原理一样。

[回到顶部](#_labelTop)

**二、安装步骤**
----------

*   下载安装包  
      下载 Linux 环境下的 jdk1.8，请去（官网）中下载 jdk 的安装文件。  
      由于我的 Linux 是 64 位的，[jdk-8u191-linux-x64.tar.gz 下载链接](http://download.oracle.com/otn-pub/java/jdk/8u191-b12/2787e4a523244c269598db4e85c51e0c/jdk-8u191-linux-x64.tar.gz)

**0、我们先有一个干净的 Linux 的环境**  
　　进行如下操作：

```
[root@itheima ~]# cat /etc/redhat-release
CentOS Linux release 7.5.1804 (Core) 
[root@itheima ~]# ll
总用量 0


```

**1、检查一下 linux 系统中的 jdk 版本**

```
[root@itheima ~]# java -version


```

　　显示如下：

```
openjdk version "1.8.0_161"
OpenJDK Runtime Environment (build 1.8.0_161-b14)
OpenJDK 64-Bit Server VM (build 25.161-b14, mixed mode)


```

**2、检测 linux 下的 jdk 安装包**

```
[root@itheima ~]# rpm -qa | grep java
或者
[root@itheima ~]# rpm -qa | grep jdk


```

　　显示如下：

```
python-javapackages-3.4.1-11.el7.noarch
java-1.8.0-openjdk-headless-1.8.0.161-2.b14.el7.x86_64
tzdata-java-2018c-1.el7.noarch
java-1.7.0-openjdk-1.7.0.171-2.6.13.2.el7.x86_64
java-1.8.0-openjdk-1.8.0.161-2.b14.el7.x86_64
javapackages-tools-3.4.1-11.el7.noarch
java-1.7.0-openjdk-headless-1.7.0.171-2.6.13.2.el7.x86_64
或者
copy-jdk-configs-3.3-2.el7.noarch
java-1.8.0-openjdk-headless-1.8.0.161-2.b14.el7.x86_64
java-1.7.0-openjdk-1.7.0.171-2.6.13.2.el7.x86_64
java-1.8.0-openjdk-1.8.0.161-2.b14.el7.x86_64
java-1.7.0-openjdk-headless-1.7.0.171-2.6.13.2.el7.x86_64


```

**3、先卸载 openjdk（共 4 个文件）**

```
[root@itheima ~]# rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.161-2.b14.el7.x86_64
[root@itheima ~]# rpm -e --nodeps java-1.7.0-openjdk-1.7.0.171-2.6.13.2.el7.x86_64
[root@itheima ~]# rpm -e --nodeps java-1.8.0-openjdk-1.8.0.161-2.b14.el7.x86_64
[root@itheima ~]# rpm -e --nodeps java-1.7.0-openjdk-headless-1.7.0.171-2.6.13.2.el7.x86_64


```

　　删完之后可以再通过：rpm -qa | grep java 或 rpm -qa | grep jdk 命令来查询出是否删除掉

```
[root@itheima ~]# rpm -qa | grep java
python-javapackages-3.4.1-11.el7.noarch
tzdata-java-2018c-1.el7.noarch
javapackages-tools-3.4.1-11.el7.noarch
[root@itheima ~]# rpm -qa | grep jdk
copy-jdk-configs-3.3-2.el7.noarch
[root@itheima ~]# 


```

**4、安装新的 Oracle JDK1.8**  
　　通过命令：`cd /usr/local/` 进入 local 目录，并通过`ll（两个小写的L）`命令或者`ls命令（ll 本身不是命令，只是 ls -l 命令的一个别名）`列出当前目录下得所有非隐含的文件，如果想要看到隐含（以. 开头的，如：.test.txt）文件信息可通过`ll -a`来查看，如下：

```
[root@itheima ~]# cd /usr/local/
[root@itheima local]# ll
总用量 0
drwxr-xr-x. 2 root root  6 4月  11 2018 bin
drwxr-xr-x. 2 root root  6 4月  11 2018 etc
drwxr-xr-x. 2 root root  6 4月  11 2018 games
drwxr-xr-x. 2 root root  6 4月  11 2018 include
drwxr-xr-x. 2 root root  6 4月  11 2018 lib
drwxr-xr-x. 2 root root  6 4月  11 2018 lib64
drwxr-xr-x. 2 root root  6 4月  11 2018 libexec
drwxr-xr-x. 2 root root  6 4月  11 2018 sbin
drwxr-xr-x. 5 root root 49 11月  2 00:50 share
drwxr-xr-x. 2 root root  6 4月  11 2018 src


```

　　进入 local 目录之后通过`mkdir java`命令来创建 java 目录存放自己的 jdk。  
**　　扩展**：如果你想一次性在同一级目录下创建多个平级的目录可以通过`mkdir brother1 brother2`（如要创建更多就在后面加上去就可以了，中间用空格隔开）这样的命令来创建，如果要一次创建父子目录（parent/child）可以通过`mkdir -p parent/child/grandson`来创建，如下：

```
[root@itheima local]# mkdir java
[root@itheima local]# ll
总用量 0
drwxr-xr-x. 2 root root  6 4月  11 2018 bin
drwxr-xr-x. 2 root root  6 4月  11 2018 etc
drwxr-xr-x. 2 root root  6 4月  11 2018 games
drwxr-xr-x. 2 root root  6 4月  11 2018 include
drwxr-xr-x. 2 root root  6 11月  8 19:01 java
drwxr-xr-x. 2 root root  6 4月  11 2018 lib
drwxr-xr-x. 2 root root  6 4月  11 2018 lib64
drwxr-xr-x. 2 root root  6 4月  11 2018 libexec
drwxr-xr-x. 2 root root  6 4月  11 2018 sbin
drwxr-xr-x. 5 root root 49 11月  2 00:50 share
drwxr-xr-x. 2 root root  6 4月  11 2018 src


```

**5、使用 SSH 链接工具 SecureCRT 链接 Linux 系统，打开 SFTP 会话**  
　　将下载好的 jdk 安装包 jdk-8u191-linux-x64.tar.gz 上传至 Linux 系统的 / usr/local/java 目录下

```
sftp> pwd
/root
sftp> cd /usr/local/java/
sftp> pwd
/usr/local/java
sftp> put -r "C:\Users\Bruce\Desktop\jdk-8u191-linux-x64.tar.gz"
Uploading jdk-8u191-linux-x64.tar.gz to /usr/local/java/jdk-8u191-linux-x64.tar.gz
  100% 187259KB  46814KB/s 00:00:04     
C:\Users\Bruce\Desktop\jdk-8u191-linux-x64.tar.gz: 191753373 bytes transferred in 4 seconds (46814 KB/s)
sftp> put -r "C:\Users\Bruce\Desktop\jdk-8u191-linux-x64.tar.gz"
Uploading jdk-8u191-linux-x64.tar.gz to /usr/local/java/jdk-8u191-linux-x64.tar.gz
  100% 187259KB  62419KB/s 00:00:03     
C:\Users\Bruce\Desktop\jdk-8u191-linux-x64.tar.gz: 191753373 bytes transferred in 3 seconds (62419 KB/s)
sftp> 


```

　　传输完成之后 ll 命令查看

```
[root@itheima java]# ll
总用量 187260
-rw-r--r--. 1 root root 191753373 11月  8 17:07 jdk-8u191-linux-x64.tar.gz
[root@itheima java]# 


```

**6、解压 jdk-8u191-linux-x64.tar.gz 安装包**

```
[root@itheima java]# tar -zxvf jdk-8u191-linux-x64.tar.gz


```

　　解压过后出现如下：

```
......
......
jdk1.8.0_191/jre/lib/fontconfig.SuSE.10.properties.src
jdk1.8.0_191/jre/lib/fontconfig.SuSE.11.bfc
jdk1.8.0_191/jre/COPYRIGHT
jdk1.8.0_191/jre/THIRDPARTYLICENSEREADME-JAVAFX.txt
jdk1.8.0_191/jre/Welcome.html
jdk1.8.0_191/jre/README
jdk1.8.0_191/README.html
[root@itheima java]# ll
总用量 187260
drwxr-xr-x. 7   10  143       245 10月  6 20:55 jdk1.8.0_191
-rw-r--r--. 1 root root 191753373 11月  8 17:07 jdk-8u191-linux-x64.tar.gz


```

　　这时安装包已经没用了，我一般都会删掉安装包，通过`rm -f jdk-8u191-linux-x64.tar.gz`删除安装包。  
　　这里`-f`的意思就是不询问删除，如果你不加`-f`在删除时它会询问你一下是否要删除该安装包，`是确定要删除就加-f`。  
　　如果你要删除一个目录，而这个目录下还有目录或者有文件，比如在 parent/child/grandson，这样的目录下你要删除 parent 下得所有目录和文件（包括 parent）就可以用到`rm -rf parent`命令就可以删除掉了。`rm -rf parent`表示递归删除不询问。

```
[root@itheima java]# rm -rf jdk-8u191-linux-x64.tar.gz 
[root@itheima java]# ll
总用量 0
drwxr-xr-x. 7 10 143 245 10月  6 20:55 jdk1.8.0_191
[root@itheima java]# 


```

**7、设置环境变量**  
　　通过`vim /etc/profile`命令打开 profile 文件盘配置环境变量

```
[root@itheima java]# vim /etc/profile


```

　　打开之后按`i`进入`insert（插入）模式`，在文件末尾添加上环境变量，内容如下：

```
JAVA_HOME=/usr/local/java/jdk1.8.0_191
JRE_HOME=/usr/local/java/jdk1.8.0_191/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH


```

　　添加完之后保存并退出，保存并退出的命令有两种 第一种是：`按住shift键然后连按两次z`（这是我常用的，因为它方便快速），第二种是`:wq`命令，有一种是不保存退出的命令`:q!` 注意：以上三种命令都是在`非插入模式`（插入模式下按键盘左上角的`Esc键退出插入模式`就是非插入模式了）下操作。

**8、保存完之后输入：source /etc/profile 命令使刚才配置的环境变量生效**

```
[root@itheima java]# source /etc/profile
[root@itheima java]# 


```

**9、测试 jdk 是否安装成功**  
　　输入`javac`命令如果出现以下的文字就说明编译成功了（如果你之前安装 centos7 时使用的语言是英文，那出现的就是类似这样排版的英文）

```
[root@itheima java]# javac
用法: javac <options> <source files>
其中, 可能的选项包括:
  -g                         生成所有调试信息
  -g:none                    不生成任何调试信息
  -g:{lines,vars,source}     只生成某些调试信息
  -nowarn                    不生成任何警告
  -verbose                   输出有关编译器正在执行的操作的消息
  -deprecation               输出使用已过时的 API 的源位置
  -classpath <路径>            指定查找用户类文件和注释处理程序的位置
  -cp <路径>                   指定查找用户类文件和注释处理程序的位置
  -sourcepath <路径>           指定查找输入源文件的位置
  -bootclasspath <路径>        覆盖引导类文件的位置
  -extdirs <目录>              覆盖所安装扩展的位置
  -endorseddirs <目录>         覆盖签名的标准路径的位置
  -proc:{none,only}          控制是否执行注释处理和/或编译。
  -processor <class1>[,<class2>,<class3>...] 要运行的注释处理程序的名称; 绕过默认的搜索进程
  -processorpath <路径>        指定查找注释处理程序的位置
  -parameters                生成元数据以用于方法参数的反射
  -d <目录>                    指定放置生成的类文件的位置
  -s <目录>                    指定放置生成的源文件的位置
  -h <目录>                    指定放置生成的本机标头文件的位置
  -implicit:{none,class}     指定是否为隐式引用文件生成类文件
  -encoding <编码>             指定源文件使用的字符编码
  -source <发行版>              提供与指定发行版的源兼容性
  -target <发行版>              生成特定 VM 版本的类文件
  -profile <配置文件>            请确保使用的 API 在指定的配置文件中可用
  -version                   版本信息
  -help                      输出标准选项的提要
  -A关键字[=值]                  传递给注释处理程序的选项
  -X                         输出非标准选项的提要
  -J<标记>                     直接将 <标记> 传递给运行时系统
  -Werror                    出现警告时终止编译
  @<文件名>                     从文件读取选项和文件名

[root@itheima java]# 


```

　　或者输入`java -version`

```
[root@itheima java]# java -version
java version "1.8.0_191"
Java(TM) SE Runtime Environment (build 1.8.0_191-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.191-b12, mixed mode)
[root@itheima java]# 


```

　　如果出现以上信息就说明你自己的 jdk 就完全安装成功了！！！

参考链接：  
  https://blog.csdn.net/hui_2016/article/details/69941850  
  https://www.cnblogs.com/Dylansuns/p/6974272.html