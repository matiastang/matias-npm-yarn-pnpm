# react-devtools

[react-devtools](https://www.npmjs.com/package/react-devtools)

## 介绍

`React DevTools`可用作`Chrome`和`Firefox`浏览器的内置扩展。该软件包使您可以在其他地方调试`React`应用（例如，`iframe`内的移动浏览器，嵌入式`Webview`，`Safari`）。

## 安装方法一（npm）

1. 安装
```
$ npm i -g react-devtools
```

## 安装方法二（本地）

1. 下载`react-devtools`文件到本地。[下载地址](https://github.com/facebook/react-devtools) 
```
$ git clone https://github.com/facebook/react-devtools.git
```
2. 安装依赖
* 进入`react-devtools`目录
* 运行命令，指定了源为[淘宝镜像源](https://registry.npm.taobao.org)
```
$ npm --registry https://registry.npm.taobao.org install
```
也可以使用[`nrm`](https://github.com/matiastang/matias-npm-yarn-pnpm/blob/main/docs/md/nrm.md)换源后，直接运行指令
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