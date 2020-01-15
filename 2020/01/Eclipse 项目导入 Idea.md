Published on 四月 23,2019 in with [0 comment](#comments)

导入 Idea 的时候不是 maven 项目的话，是没有包引用的，里面的引用包会放在 WebRoot/WEB-INF/lib 文件夹下面![](http://hiper.top/upload/2019/3/image-15559941031642019042304350369.png) 这个时候到导入依赖包，步骤如下 工具栏 file->Project Structure->Modules-> 中间栏选中项目名称 -> 右边栏选择 dependencies-> 最右侧点击加号 -> 选择 jar or directories ![](http://hiper.top/upload/2019/3/image-155599442488520190423044029489.png) ![](http://hiper.top/upload/2019/3/image-155599450328220190423044143246.png) 选择刚才的 lib 里面的依赖包；

用 tomcat 调试：(web 项目) 刚才的那个 Project Struture 里面的 facets 添加上下文和 web 容器并配置路径 ![](http://hiper.top/upload/2019/3/image-155599477380020190423044613889.png) Project Struture 里面的 Artifacts 添加 WEB-INF 和刚才 wen 容器 ![](http://hiper.top/upload/2019/3/image-155599491353720190423044833554.png) 最后在运行配置里添加 tomcat 配置端口和 Artifacts

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 10,2020