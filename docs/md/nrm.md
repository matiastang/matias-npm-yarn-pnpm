# nrm

[nrm](https://www.npmjs.com/package/nrm)

## 介绍

`nrm`是一个`npm`源管理工具，使用它可以快速切换`npm`源。

## 安装

全局安装：
```
$ npm install -g nrm
```

## 切换源

1. `nrm ls`查看所有源（前面有`*`的为当前源）

```
$ nrm ls

  npm -------- https://registry.npmjs.org/
  yarn ------- https://registry.yarnpkg.com/
  cnpm ------- http://r.cnpmjs.org/
  taobao ----- https://registry.npm.taobao.org/
  nj --------- https://registry.nodejitsu.com/
  npmMirror -- https://skimdb.npmjs.com/registry/
  edunpm ----- http://registry.enpmjs.org/
  bbdops ----- http://npm.bbdops.com/
* bbd -------- http://verdaccio.bbdops.com/
```

2. `nrm add <registry> <url> [home]`添加源（不添加可以忽略）

如添加`bbdops ----- http://npm.bbdops.com/`
```
$ nrm add bbdops http://npm.bbdops.com/
```

3. `nrm test [registry]`测试源速度

不加`registry`时，可测所有源：
```
$ nrm test

  npm ---- 952ms
  yarn --- 3163ms
  cnpm --- 4457ms
  taobao - 623ms
  nj ----- Fetch Error
  npmMirror  3792ms
  edunpm - Fetch Error
  bbdops - 4456ms
* bbd ---- 2079ms
```

4. `nrm use [registry]`切换源（完成后可以`nrm ls`查看一下）

如切换到淘宝源：
```
$ nrm use taobao
```

## 命令

`$ nrm help`：
```
Usage: nrm [options] [command]

Options:
  -V, --version                           output the version number//查看当前nvm版本。
  -h, --help                              output usage information//显示所有命令。

Commands:
  ls                                      List all the registries//显示所有源
  current                                 Show current registry name//显示当前源名称。
  use <registry>                          Change registry to registry//切换源。
  add <registry> <url> [home]             Add one custom registry//添加源。比如公司自己的私有源等。
  set-auth [options] <registry> [value]   Set authorize information for a custom registry with a base64 encoded string or username and pasword//设置自定义源的授权信息。
  set-email <registry> <value>            Set email for a custom registry//给自定义源设置路径。
  set-hosted-repo <registry> <value>      Set hosted npm repository for a custom registry to publish packages//设置发布到自定义源的npm托管仓储。
  del <registry>                          Delete one custom registry//删除自定义源。
  home <registry> [browser]               Open the homepage of registry with optional browser//浏览器中打开源首页。
  publish [options] [<tarball>|<folder>]  Publish package to current registry if current registry is a custom registry.
   if you're not using custom registry, this command will run npm publish directly//发布包到自定义源，如果没有使用自定义源，则直接发布到npm。
  test [registry]                         Show response time for specific or all registries测试源的访问速度。不加registry时，测试所有的。
  help                                    Print this help//打印帮助
```