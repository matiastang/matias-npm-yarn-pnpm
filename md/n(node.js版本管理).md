# n

[node.js版本查看](https://nodejs.org/zh-cn/download/releases/)
[n](https://www.npmjs.com/package/n)

## 介绍

`n` 模块可以管理`Node`版本。

## 安装

1. 查看`node`版本。
```
$ node -V
```
2. 清除`node`缓存
```
$ sudo npm cache clean -f
```
3. 安装`n`
```
$ sudo npm install n -g
```
4. 安装指定版本的`node`或者升级到最新版本`node`。
```
$ sudo n stable （安装node最新稳定版本）
$ sudo n 10.15.0 （安装node指定版本/切换版本）
```