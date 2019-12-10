基本命令记录 --linux

centos 包管理器 yum
ubuntu debian kali 包管理器 apt-get


查看系统的信息：

uname -a
cat /etc/issue        # 查看操作系统版本——Os版本
cat /proc/version      #包含GCC的版本信息
cat /proc/cpuinfo     # 查看CPU相关信息(型号,缓存大小等)
cat /proc/stat         #查看所有CPU的活动信息
cat /sys/class/thermal/thermal_zone0/temp
查看cpu温度（/ 1000就是温度）
hostname             # 查看计算机名
lspci -tv             # 列出所有PCI设备
lsusb -tv             # 列出所有USB设备
lsmod                 # 列出加载的内核模块
env                   # 查看环境变量


资源信息：

free -m # 查看内存使用量和交换区使用量
df -h # 查看各分区使用情况
du -sh <目录名> # 查看指定目录的大小
grep MemTotal /proc/meminfo # 查看内存总量
grep MemFree /proc/meminfo # 查看空闲内存量
uptime # 查看系统运行时间、用户数、负载
cat /proc/loadavg # 查看系统负载

磁盘信息：

mount | column -t # 查看挂接的分区状态
fdisk -l # 查看所有分区
swapon -s # 查看所有交换分区
hdparm -i /dev/hda # 查看磁盘参数(仅适用于IDE设备)
dmesg | grep IDE # 查看启动时IDE设备检测状况
 下载网络工具net-tools

  sudo apt-get install net-tools

网络信息;

ifconfig # 查看所有网络接口的属性
iptables -L # 查看防火墙设置
route -n # 查看路由表
netstat -lntp # 查看所有监听端口
netstat -antp # 查看所有已经建立的连接
netstat -s # 查看网络统计信息
netstat -an #查看哪些IP连接本机
netstat -nap | grep 22066 查看Linux端口的占用及连接情况


临时关闭防火墙
service firewalld stop 直接关闭防火墙
service iptables stop  直接关闭防火墙

永久关闭防火墙

systemctl stop firewalld

systemctl disable firewalld

firewall-cmd --reload




用户信息：

w # 查看活动用户
id <用户名> # 查看指定用户信息
last # 查看用户登录日志
cut -d: -f1 /etc/passwd # 查看系统所有用户
cut -d: -f1 /etc/group # 查看系统所有组
crontab -l # 查看当前用户的计划任务


进程信息：

ps -ef # 查看所有进程
top # 实时显示进程状态


基本分区方案：

1. 挂载点/；主分区；安装系统和软件；大小为30G；分区格式为ext4； 
2. 挂载点/home；逻辑分区；相当于“我的文档”；大小为硬盘剩下的;
分区格式ext4； 
3. swap；逻辑分区；充当虚拟内存；大小等于内存大小（本人2G）；
分区格式为swap 
4. /boot ；引导分区；逻辑分区； 大小为200M ；分区格式为ext4；

上传下载文件:lrzsz

1. 【安装命令】：yum install lrzsz
 
2. 【从linux服务器发送文件 filename 到本地 wndows】：
sz filename
这时会弹出窗口让你选择将文件保存到本地的位置
3. 【从本地 wndows 上传文件到 linux 服务器】：
rz
这时会弹出窗口让你选择上传的文件.
4. xshell中可以设置上传和下载文件的默认路径，文件/属性/zmodem.

解压文件 tar.gz

tar -zxvf  filename.tar.gz

移动文件夹/文件
mv fileoldpath/filename  filenewppath

重命名文件/文件夹
cp oldname newname

删除文件
rm filename -f

删除文件夹(递归删除)
rmdir name -f -r

新建文件

mk filename
touch filename
vi filename
vim filename

新建文件夹
mkdir name

查找文件
whereis filename

在vim模式下操作

进入 输入模式 i
进入 nomal模式 esc
查找字符串 / 然后输入字符串回车 n查找下一个，N上一个

创建用户，创建组

#建立一个mysqlgroup的组
groupadd mysqlgroup

#建立mysqluser用户，并且把用户放到mysqlgroup组
useradd -r -g mysqlgroup mysqluser

#为mysqluser用户设置密码
passwd mysqluser

#给目录/usr/local/mysql 更改拥有者
chown -R mysqluser:mysqlgroup /usr/local/mysql


ssh登录：

打开终端，或者是用工具登录到目标服务器（你要通过ssh登录到的那个服务器）

输入： ssh-keygen -t rsa

*

出现三个交互的地方，
第一个是你想要保存的地址，默认就好（默认回车），有需要自己更改
第二个是输入密码，不需要密码，直接回车
第三个是确认密码，同样回车

*

此时切换到ssh的目录
cd /root/.ssh

查看全部的文件
ll
*

部署公钥
6
ssh-copy-id -i /root/.ssh/id_rsa.pub root@yourip
如果你要用别的电脑登录此系统，则这个yourip为本机的ip，
如果你是要用此电脑登录别的系统，则这个yourip为要登录的系统ip

*

输入yes

然后复制id_rsa 到你的电脑，在x-shell或者putty里面导入。
一个liunx通过ssh登录另一个linux里退出的时候输入
exit


SSH登录的原理

先是客户端向服务器发送ssh连接请求
服务器返一个随机的字符串
客户端根据私钥进行加密并发送给服务器
服务器根据公钥进行解密，如果正确则和客户端连接



rpm 操作

1.安装rpm包
rpm -ivh *.rpm

2.查询已安装
rpm -qa：查询所安装的所有rpm软件包

rpm -qa | more ：查询所安装的所有rpm软件包 并且分页显示

rpm -qa | grep X [rpm -qa | grep firefox ] ：查询是否安装
有某个软件（火狐的软件）

rpm -q 软件包名 ：查询软件包是否安装 rpm -q firefox
rpm -qi 软件包名 ：查询软件包信息

rpm -ql 软件包名 ：查询软件包中的文件的安装位置

rpm -qf 文件全路径名：查询文件所属的软件包 ，例如：
rpm -qf /etc/passwd 

 

3.卸载rpm包：

基本语法 rpm -e RPM包的名称 

应用案例 ：删除firefox  软件包 

rpm -e firefox


权限相关


格式：
chmod 权限数字 文件名
 
r 读权限read  4
w 写权限write 2
x 操作权限execute  1

对应1234567，777为最高权限，所有人都能进行操作
 
权限数字对应权限组说明：
总共分为4部分
【文件或文件夹】【owner权限】【group权限】【others权限】
【文件是-，文件夹是d】【r/w/x相加】【r/w/x相加】【r/w/x相加】
Linux档案的基本权限就有九个，分别是owner/group/others
三种身份各有自己的read/write/execute权限。
 
 
OK,接口介绍完成，实际说明例子：
d rwx  rwx  rwx  =777  表示目录的操作权限
-  rwx  rwx  rwx = 777  表示文件的操作权限
 
 
 - rwx rwx rwx =777表示 文件的操作权限
- rw-  r--  r--  = 644  表示文件的操作权限


uname - a,
uname - v,
后台运行程序

nohup java -jar xxx.jar >>test.log &1 &

nohup command > myout.file 2>&1 &

这个命令比较厉害。。
tail -f nohup.out


(1) nohup 

加在一个命令的最前面，表示不挂断的运行命令

(2) &

加载一个命令的最后面，表示这个命令放在后台执行

2. 查看后台运行的命令
有两个命令可以来查看，ps 和 jobs。区别在于 jobs 只能查看当前终端后台执行的任务，换了终端就看不见了。而ps命令适用于查看瞬时进程的动态，可以看到别的终端的任务。

(1) jobs 

[root@localhost test]# jobs
[1]-  运行中               nohup java -Dfile.encoding=UTF-8 -Dname=Runtime-Name -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M -XX:+HeapDumpOnOutOfMemoryError -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -jar test.jar $1 $2 $3 &(工作目录：/home/ams/ams-server/test)
[2]+  运行中               nohup java -Dfile.encoding=UTF-8 -Dname=Container-Name -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M -XX:+HeapDumpOnOutOfMemoryError -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -jar test1.jar $1 $2 $3 &
先后起了两个后台运行的进程，使用jobs后都显示出来了。“+”代表最近的一个任务（当前任务），“-”代表之前的任务。

只有在当前命令行中使用 nohup和& 时，jobs命令才能将它显示出来。如果将他们写到 .sh 脚本中，然后执行脚本，是显示不出来的

 比如执行下面这个脚本后，jobs显示不出来：

#!/bin/bash
nohup java -Dfile.encoding=UTF-8 -Dname=Runtime-Name -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M -XX:+HeapDumpOnOutOfMemoryError -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -jar test.jar $1 $2 $3 &
(2) ps命令

[root@localhost test]# ps -aux|grep java
root     21219  0.3  3.9 6258172 148900 pts/0  Sl   10:08   0:02 java -Dfile.encoding=UTF-8 -Dname=Runtime-Name -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M -XX:+HeapDumpOnOutOfMemoryError -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -jar test.jar
root     21662  0.2  3.0 5041008 116648 pts/0  Sl   10:10   0:01 java -Dfile.encoding=UTF-8 -Dname=Container-Name -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M -XX:+HeapDumpOnOutOfMemoryError -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -jar test1.jar
root     23761  0.0  0.0 112664   972 pts/0    S+   10:19   0:00 grep --color=auto java
这个是查看进程常用的命令，不多说了。

a: 显示所有程序  u: 以用户为主的格式来显示   x: 显示所有程序，不以终端机来区分

3. 关闭当前后台运行的程序
kill 命令

（1）通过jobs命令查看jobnum，然后执行   kill %jobnum

（2）通过ps命令查看进程号PID，然后执行  kill %PID

如果是前台进程的话，直接执行 Ctrl+c 就可以终止了

4. 前后台进程的切换与控制
（1）fg命令

将后台中的命令调至前台继续运行

如果后台中有多个命令，可以先用jobs查看jobnun，然后用 fg %jobnum 将选中的命令调出。

（2）Ctrl + z 命令

将一个正在前台执行的命令放到后台，并且处于暂停状态

（3）bg命令

将一个在后台暂停的命令，变成在后台继续执行

如果后台中有多个命令，可以先用jobs查看jobnum，然后用 bg %jobnum 将选中的命令调出继续执行。







