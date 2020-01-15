**一：下载文件：** http://nginx.org/en/download.html 选择操作系统，选择版本，现在用最新版演示； ![](http://hiper.top/upload/2019/8/image-156799408000820190909015441954.png) **二：安装** 1、下载完成后，解压缩，运行 cmd，使用命令进行操作，不要直接双击 nginx.exe，不要直接双击 nginx.exe，不要直接双击 nginx.exe 一定要在 dos 窗口启动，不要直接双击 nginx.exe，这样会导致修改配置后重启、停止 nginx 无效，需要手动关闭任务管理器内的所有 nginx 进程，再启动才可以。 2、使用命令到达 nginx 的加压缩后的目录

```
cd c:\nginx-1.15.2


```

3、启动 nginx 服务，启动时会一闪而过是正常的

```
start nginx


```

4、查看任务进程是否存在，dos 或打开任务管理器都行

```
tasklist /fi "imagename eq nginx.exe"


```

如果都没有可能是启动报错了查看一下日志，在 nginx 目录中的 logs 文件夹下 error.log 是日志文件 常见的错误：

(1) 端口号被占用

(2)nginx 文件夹路径含中文

其他错误就详细看 log 中的描述 5、修改完成后保存，使用以下命令检查一下配置文件是否正确，后面是 nginx.conf 文件的路径，successful 就说明正确了

```
nginx -t -c /nginx-1.15.2/conf/nginx.conf


```

6、如果程序没启动就直接 start nginx 启动，如果已经启动了就使用以下命令重新加载配置文件并重启。

```
如果程序没启动就直接start nginx启动，如果已经启动了就使用以下命令重新加载配置文件并重启


```

7：打开浏览器访问刚才的域名及端口 http://localhost:8800，出现欢迎页就说明部署成功了 **三. 配置优化** 打开 nginx.conf 按照自己需求进行配置，下面列出简单的一些常规调优配置

```
worker_processes  1;








events {

    
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    
    
    

    

    sendfile        on;
    

    
    
    
    keepalive_timeout  65;

    

    
    server_names_hash_bucket_size 512;

    
    
    server {
        
        listen       8800;
        
        server_name  localhost;
        
        
        charset utf-8;

        

        
        
        
        location / {
            
            root   html;
            
            index  index.html index.htm;
            
            
            

            
            
            
            
            
            
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Credentials' 'true';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
            
            
            proxy_set_header Host $host;
            
            proxy_set_header X-Real-IP $remote_addr;
            
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            
            proxy_set_header Cookie $http_cookie;
            
            proxy_redirect off;
            
            
            
            
            
　　         
            
            
            
            
　　　　　　  
            proxy_cookie_domain localhost .testcaigou800.com;
            
            
            
            
            proxy_connect_timeout 30;
        }

        

        
        
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }
    
　　
　　
　　server {
　　　　listen 80;
　　　　server_name www.abc.com;
　　　　charset utf-8;
　　　　location / {
　　　　　　proxy_pass http://localhost:10001;
　　　　}
　　}
　　server {
　　　　listen 80;
　　　　server_name aaa.abc.com;
　　　　charset utf-8;
　　　　location / {
　　　　　　proxy_pass http://localhost:20002;
　　　　}
　　}
}


```

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 14,2020