
**一: 启动、停止、重启；** 在当前的文件夹下打开终端，在命令行里操作： 1：启动

```
start ngingx


```

2：关闭

```
nginx -s -stop


```

3: 重启

```
nginx -s reload


```

4: 检查配置文件是否正确

```
nginx -t


```

**二：查看文件或者是配置** 1：在 log 文件夹下可以看运行中的日志； 2：在 config/nginx.conf 文件内配置反向代理和负载均衡 a: 反向代理配置多个 web，统一域名下访问，只需要带目录就行（不同 web 可以多个服务器上）

```
http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    
    upstream nana {
        server localhost:18880;
    }

    
    upstream nananana {
        server localhost:18881;
    }
        
    server {
        listen       8888;
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
        } 

        
        location ^~/first-path/ { 
            proxy_pass http://nana/;
            proxy_set_header X-real-ip $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_connect_timeout 5s;
        }

        
        location /firstPath { 
            proxy_pass http://nananana/first-path;
            proxy_set_header X-real-ip $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_connect_timeout 5s;
        }
}


```

b: 配置多个相同的 web 进行反向代理实现负载均衡

```
upstream tomcatserver1 {  
    server 192.168.72.49:8080 weight=3;  
    server 192.168.72.49:8081;  
    }   
  
 server {  
        listen       80;  
        server_name  8080.max.com;  
        
        
        location / {  
            proxy_pass   http://tomcatserver1;  
            index  index.html index.htm;  
        }  
     }


```

c: 实现负载均衡有三种模式： 1)、轮询 ——1：1 轮流处理请求（默认） 每个请求按时间顺序逐一分配到不同的应用服务器，如果应用服务器 down 掉，自动剔除，剩下的继续轮询。 2)、权重 ——you can you up 通过配置权重，指定轮询几率，权重和访问比率成正比，用于应用服务器性能不均的情况。 3)、ip_哈希算法 每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个应用服务器，可以解决 session 共享的问题。

d: 配置代表 1）down 表示单前的 server 暂时不参与负载

2）Weight 默认为 1.weight 越大，负载的权重就越大。

3）max_fails 允许请求失败的次数默认为 1. 当超过最大次数时，返回 proxy_next_upstream 模块定义的错误

4）fail_timeout max_fails 次失败后，暂停的时间。

5）Backup

```
其它所有的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻。


```

**三：安装组件** 未完继续。。

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 14,2020