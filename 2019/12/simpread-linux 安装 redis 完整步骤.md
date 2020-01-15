> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 https://www.cnblogs.com/limit1/p/9045183.html

安装：
===

1. 获取 redis 资源

　　wget http://download.redis.io/releases/redis-4.0.8.tar.gz

2. 解压

　　tar xzvf redis-4.0.8.tar.gz

3. 安装

　　cd redis-4.0.8

　　make

　　cd src

　　make install PREFIX=/usr/local/redis

4. 移动配置文件到安装目录下

　　cd ../

　　mkdir /usr/local/redis/etc

　　mv redis.conf /usr/local/redis/etc

 5. 配置 redis 为后台启动

　　vi /usr/local/redis/etc/redis.conf // 将 **daemonize no** 改成 daemonize yes

6. 将 redis 加入到开机启动

　　vi /etc/rc.local // 在里面添加内容：/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf (意思就是开机调用这段开启 redis 的命令)

7. 开启 redis

　　/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf 

常用命令　　

　　redis-server /usr/local/redis/etc/redis.conf // 启动 redis

　　pkill redis  // 停止 redis

　　卸载 redis：

　　　　rm -rf /usr/local/redis // 删除安装目录

　　　　rm -rf /usr/bin/redis-* // 删除所有 redis 相关命令脚本

　　　　rm -rf /root/download/redis-4.0.4 // 删除 redis 解压文件夹

1. 获取 redis 资源

　　wget http://download.redis.io/releases/redis-4.0.8.tar.gz

2. 解压

　　tar xzvf redis-4.0.8.tar.gz

3. 安装

　　cd redis-4.0.8

　　make

　　cd src

　　make install PREFIX=/usr/local/redis

4. 移动配置文件到安装目录下

　　cd ../

　　mkdir /usr/local/redis/etc

　　mv redis.conf /usr/local/redis/etc

 5. 配置 redis 为后台启动

　　vi /usr/local/redis/etc/redis.conf // 将 **daemonize no** 改成 daemonize yes

6. 将 redis 加入到开机启动

　　vi /etc/rc.local // 在里面添加内容：/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf (意思就是开机调用这段开启 redis 的命令)

7. 开启 redis

　　/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf 

常用命令　　

　　redis-server /usr/local/redis/etc/redis.conf // 启动 redis

　　pkill redis  // 停止 redis

　　卸载 redis：

　　　　rm -rf /usr/local/redis // 删除安装目录

　　　　rm -rf /usr/bin/redis-* // 删除所有 redis 相关命令脚本

　　　　rm -rf /root/download/redis-4.0.4 // 删除 redis 解压文件夹