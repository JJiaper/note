## 解压缩命令
### 打包: tar

计算机中的数据经常需要备份，tar 是 Unix/Linux 中最常用的备份工具，此命令可以把一系列文件归档到一个大文件中，也可以把档案文件解开以恢复数据。

tar 使用格式 tar [参数] 打包文件名 文件  
**tar 命令只打包不压缩**

tar 命令很特殊，其参数前面可以使用 “-”，也可以不使用。

常用参数：

| 参数 | 含义 |
| --- | --- |
| -c | 生成档案文件，创建打包文件 |
| -v | 列出归档解档的详细过程，显示进度 |
| -f | 指定档案文件名称，f 后面一定是. tar 文件，所以必须放选项最后 |
| -t | 列出档案中包含的文件 |
| -x | 解开档案文件 |

注意：除了 f 需要放在参数的最后，其它参数的顺序任意。  
`tar -cvf name.tar name.txt`# 将 name.txt 打包成 name.tar  
`tar -xvf name.tar` # 将 name.tar 解包  
`tar -xvf name.tar -C dic/` # 将 name.tar 解压到该目录下的 dic 文件夹下

### 文件压缩解压：gzip

tar 与 gzip 命令结合使用实现文件打包、压缩。 tar 只负责打包文件，但不压缩，用 gzip 压缩 tar 打包后的文件，其扩展名一般用 xxxx.tar.gz。

gzip 使用格式如下：  
`gzip [选项] 被压缩文件`  
常用选项：

| 选项 | 含义 |
| --- | --- |
| -d | 解压 |
| -r | 压缩所有子目录 |

`tar -zcvf name.tar.gz *.txt` 把所有的. txt 文件打包并压缩成 name.tar.gz  
`tar -zxvf name.tar.gz` 解压缩  
`tar -zxvf name.tar.gz -C gz/` 将包解压缩到 gz 目录下



## more less命令

我们查看数据的时候，使用前面提到的 nl 与 cat、tac 等等，都是将文件内容一次性输出到屏幕上，看起来不是很方便，那我们就可以使用这个命令，一页一页查看，前面的数据不至于看不到。

#### 命令说明

```
[wenjie@localhost ~]$ more /etc/man.config
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
--More--(31%) <== 重点在这一行，光标也会在这里等待你的命令

```

*   **空格键（Space）**：代表向下翻一页。
*   **Enter**：代表向下滚动一行。
*   **/ 字符串**：代表在当前显示的内容中，向下查找 “字符串” 这个关键字。
*   **:f**：立刻显示出文件名与当前的行号。
*   **q**：代表立即退出，不予显示。
*   **b 或 [ctrl]-b**：往回翻，不过该操作只对文件有用。

有时候我们需要搜索`should`这个字符串

```
[wenjie@localhost ~]$ more /etc/man.config
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
/should <== 输入了 / 之后，光标会在最下面一行等待

```

你输入了`/`之后，光标会在最后一行等待，并且等待你的输入，你输入了字符串后并且按下`[Enter]`之后，就开始向下查找。如果想重复查找该字符串，可以直接按下`n`即可。

