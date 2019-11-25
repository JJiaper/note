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

git分本地仓库和远程仓库
在自己修改或者是新加了一部分代码的时候，先commit将代码提交到本地的
仓库里面；然后再push推送到远程仓库的地址；

在增加文件的时候，要将文件添加到git的追踪里面，就是所谓的add，这个
操作后就可以检测这个文件的改动记录了；

分支操作；
和远程仓库的概念类似，分支也分为本地分支和远程分支，你可以拉取不同分支的代码进行比对；
在新建分支后，记得先推送分支到远程地址；
每次写完代码或者是更新完文档后，将本地代码提交，然后推送到远程仓库分支，然后提交pull request。
将本地分支代码合并到主分支代码上，当然这个主分支是相对的主分支，不一定是master分支
