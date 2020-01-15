以前写桌面的时候都是用 c#、c++；无疑是 ui 太丑，框架内空间样式固定，自定义太繁琐； 不过现在的这个 electron 是解决了这一问题，因为它的 ui 是由 html 和 js、css 组成，这样界面就可以花里胡哨了。。； 使用步骤： 1：安装 node；

```
检验：`node -v  `  
				`npm -v `    


```

2：全局安装 electron `npm install -g ``electron` 如果安装太慢可以切换淘宝的 cnpm; 1: 切换淘宝镜像 `npm configsetregistry https://registry.npm.taobao.org` 2：安装 cnpm `npm install -g cnpm` 全局安装 electron `cpm install -g ``electron` 3: 下载 demo [https://github.com/electron/electron-quick-start](https://) 4: 安装依赖 在下载好的文件解压好的文件夹下 地址栏输入 cmd `npm install` 5：运行 `electron .`或者 `npm start` 或者 `node run`

6: 打包成 exe 运行文件 安装打包工具，我是使用的 electron-packager，首先全局安装一下： `npm install electron-packager -g` 有两种打包方式 1）在 app 根目录执行命令行 `ectron-packager . 'HelloWorld' --platform=win32 --arch=x64 --icon=icon.ico --out=./out --asar --app-version=0.0.1` 2）首先编辑 package.json

```
"scripts": {
        "start": "electron .",
        "package": "electron-packager . 'nocat' --platform=win32 --arch=x64 --icon=icon.ico --out=./out --asar --app-version=0.0.1"
    },


```

然后运行 npm run-script package

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 10,2020