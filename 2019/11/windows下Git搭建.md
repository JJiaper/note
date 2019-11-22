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

```
# 在当前目录新建一个Git代码库
$ git init
# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]
# 下载一个项目和它的整个代码历史
$ git clone [url]
```

```
# 添加指定文件到暂存区
$ git add [file1] [file2] ...
# 添加指定目录到暂存区，包括子目录
$ git add [dir]
# 添加当前目录的所有文件到暂存区
$ git add .
# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...
# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]
# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]

```