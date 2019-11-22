  # Git

* 第一步， 先配置自己的名称和邮箱

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
* 第二步 生成ssh
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
直接三下回车，会生成一个两个文件在

````
C:\Users\用户\.ssh 
````

 用记事本打开 **id_rsa.pub**文件

![批注 20191121 204451.png](0)

添加后就可以在本地来拉取代码了

```
git clone @your`surl
```
# **常用命令：**
```
Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库
```