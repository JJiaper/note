
第一步下载安装 git； https://git-scm.com/downloads

检验安装是否成功： 在 cmd 里面输入 git ![](http://hiper.top/upload/2019/6/image-156379871961220190722123200313.png) 如果如这个样子则代表成功；

安装完成后在自己的代码的根目录地址栏输入 cmd 回车；

初始化库： `git init`

配置邮箱和用户名： `git config --global user.name "superGG1990"`

`git config --global user.email "superGG1990@163.com"`

配置 ssh

查看本机是否已经生成 ssh： 如果是 linux 系统

```
cd ~/.ssh
ls
authorized_keys2  id_dsa       known_hosts config            id_dsa.pub


```

该目录下如果存在这. pub 文件则已经存在 ssh 公钥了

windows 下

```
$ ssh-keygen -t rsa -C "your_email@youremail.com"


```

在 (/home/you/.ssh/id_rsa): 查看生成的 ssh 公钥对

然后在浏览器登陆自己的 github 账户，在设置里找到 ssh，点击 add 添加新的 ssh 对，随便写一个 tittle，然后将在本机生成的. pub 的内容添加到 key 里面

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 15,2020