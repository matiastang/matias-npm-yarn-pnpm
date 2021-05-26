# react-devtools

react调试工具。
React DevTools可用作Chrome和Firefox浏览器的内置扩展。该软件包使您可以在其他地方调试React应用（例如，iframe内的移动浏览器，嵌入式Webview，Safari）。

[react-devtools](https://www.npmjs.com/package/react-devtools)

## 安装方法一（npm）

1. 安装
```
$ npm i -g react-devtools
```

## 安装方法二（本地）

1. 下载`react-devtools`文件到本地。
[下载地址](https://github.com/facebook/react-devtools) 
```
$ git clone https://github.com/facebook/react-devtools.git
```
2. 安装依赖
* 进入`react-devtools`目录
* 运行命令
```
$ npm --registry https://registry.npm.taobao.org install
```
可以使用`nrm`换源后，直接运行指令
```
$ npm install
```
3. 打包
命令在项目的`package.json`文件的`scripts`中找。
```
$ npm run build:extension:chrome
```
打包成功后会生成目录：`react-devtools/shells/chrome/build/unpacked`
4. 安装扩展
打开`chrome`浏览器的扩展程序（`chrome://extensions/`），找到 `load unpacked`，导入刚刚生成的`unpacked`。