> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 https://blog.csdn.net/qq_35763837/article/details/79654023

下载 rpm 包

1 解压 rpm 包将解压目录移动到安装目录

```
tar -zxvf mongodb-linux-x86_64-3.2.8.tgz    mv  mongodb-linux-x86_64-3.2.8 /usr/local/mongodb

```

2 在 mongodb 目录下新建两个目录 db 和 logs 分别用于存放数据和日志

 ![](http://img-blog.csdn.net/20180322145742986?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NzYzODM3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

3 验证是否安装成功

```
./bin/mongod --dbpath /usr/local/mongodb/db

```

    3.1 如果遇到错误信息：Failed to obtain address inform

![](http://img-blog.csdn.net/20180322151155807?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NzYzODM3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

  vi /etc/hosts 在最后添加 127.0.0.1   bogon 保存退出编辑 重新启动

4 设置根据配置文件启动 mongodb

   4.1 新建文件 vi mongodb/conf/mongodb/conf 配置如下内容  

    dbpath = /usr/local/mongodb/db  
    # 日志文件存放目录  
    logpath = /usr/local/mongodb/logs/mongodb.log  
    # 端口  
    port = 27017  
    # 以守护线程的方式启用，即在后台运行  
    fork = true  
    # 日志输出方式，使用追加的方式写日志  
    logappend = true  
    #PID File 的完整路径，如果没有设置，则没有 PID 文件  
    pidfilepath = /usr/local/mongodb/mongo.pid  
    # 关闭 http 接口，默认关闭 27018 端口访问  
    #nohttpinterface = true  
    # 声明这是一个集群的分片，默认端口是 27018  
    shardsvr = true  
    # 设置每个数据库将被保存在一个单独的目录  
    #directoryperdb = true  
    # 开启认证  
    #auth = true  
    # 设开启简单的 rest API，置后打开 28017 网页端口  
    rest = true  

    4.2 保存退出进入 bin 目录输入命令 ./mongod -config mongodb.conf 

![](http://img-blog.csdn.net/20180322153048741?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NzYzODM3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

    如图启动成功

5 设置开机启动

    5.1 添加系统服务配置文件 vim /etc/rc.d/init.d/mongod, 添加如下配置

ulimit -SHn 655350  
#!/bin/sh  
# chkconfig: - 64 36  
# description:mongod  
case $1 in  
start)  
/usr/local/mongodb/bin/mongod  --maxConns 20000  --f /usr/local/mongodb/conf/mongodb.conf  
;;  
stop)  
/usr/local/mongodb/bin/mongo 127.0.0.1:27017/admin --eval "db.shutdownServer()"  
;;   
status)  
/usr/local/mongodb/bin/mongo 127.0.0.1:27017/admin --eval "db.stats()"  
;;  

esac

  对 mongod 添加权限 chmod 755 /etc/rc.d/init.d/mongod

  service mongodb start 启动 service mongodb stop (pkill mongodb) 停止

  5.2 设置开机启动 chkconfig mongod on

    验证 mongodb 是否启动  lsof -i :27017

6 设置开启安全验证

    6.1 先添加用户和分配角色 

db.createUser({user:"admin",pwd:"123456",roles:["root"]})   
db.auth("admin", "123456")  
db.createUser({user: "root", pwd: "123456", roles: [{ role: "dbOwner", db: "test"}]})  

db.grantRolesToUser("root", [ { role: "readWrite", db: "test"} ])

    停止 mongodb 服务 service mongodb stop

    6.2 将启动配置文件的 auth = true 选项前的的注释去掉保存退出启动 mongodb 服务 service mongodb start

    登陆时命令格式如： ./mongo 数据库名 -u 用户名 -p 密码

![](https://img-blog.csdn.net/20180322161522992?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NzYzODM3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

    登陆成功

转载自：https://www.linuxidc.com/Linux/2016-07/133413.htm

*   [点赞](javascript:;)
*   [收藏](javascript:;)
*   [分享](javascript:;)
*   *   文章举报

 [![](https://profile.csdnimg.cn/5/8/E/3_qq_35763837) ![](https://g.csdnimg.cn/static/user-reg-year/1x/3.png)](https://blog.csdn.net/qq_35763837) [qq_35763837](https://blog.csdn.net/qq_35763837) 发布了 4 篇原创文章 · 获赞 1 · 访问量 7866 [关注](https://im.csdn.net/im/main.html?user>私信
                        </a>
                                                            <a data-report-click=)