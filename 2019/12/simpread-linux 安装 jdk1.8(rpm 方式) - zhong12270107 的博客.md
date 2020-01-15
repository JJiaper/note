> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 https://blog.csdn.net/zhong12270107/article/details/89762430

参考这个网址：https://blog.csdn.net/lg491733638/article/details/77696459

通过命令 java -version  查看是否已经安装了其他 jdk, 如果有需要先卸载，卸载命令网上查一下  
如果原来有 openjdk 需要先卸载 openjdk

// 添加可执行权限  
chmod +x jdk-8u101-linux-x64.rpm

// 安装 rpm 软件包  
rpm -ivh jdk-8u101-linux-x64.rpm

// 查看 java 的版本信息  
java -version

java version "1.8.0_60"

Java(TM) SE Runtime Environment (build 1.8.0_60-b27)  
Java HotSpot(TM) 64-Bit Server VM (build 25.60-b23, mixed mode)

设置变量环境

cd /etc/  
vi profile

export JAVA_HOME=/usr/java/jdk1.8.0_91

export JAVA_BIN=/usr/java/jdk1.8.0_91/bin

export PATH=$PATH:$JAVA_HOME/bin

export CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export JAVA_HOME JAVA_BIN PATH CLASSPATH

  
有时需要让 profile 起作用，需要执行 source /etc/profile 命令

*   [点赞](javascript:;)
*   [收藏](javascript:;)
*   [分享](javascript:;)
*   *   文章举报

 [![](https://profile.csdnimg.cn/6/F/A/3_zhong12270107) ![](https://g.csdnimg.cn/static/user-reg-year/1x/5.png)](https://blog.csdn.net/zhong12270107) [zhong12270107](https://blog.csdn.net/zhong12270107) 发布了 14 篇原创文章 · 获赞 23 · 访问量 12 万 + [关注](https://im.csdn.net/im/main.html?user>私信
                        </a>
                                                            <a data-report-click=)