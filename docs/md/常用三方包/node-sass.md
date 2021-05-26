<!--
 * @Author: tangdaoyong
 * @Date: 2021-05-26 11:11:19
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-05-26 14:00:49
 * @Description: node-sass
-->
# node-sass

[node-sass github](https://github.com/sass/node-sass)
[node-sass 发行版本](https://github.com/sass/node-sass/releases)
[node-sass npm](https ://www.npmjs.com/package/node-sass)

**警告**： [不推荐使用`LibSass`和`Node Sass`](https://sass-lang.com/blog/libsass-is-deprecated)。尽管他们将继续无限期地获得维护版本，但没有计划添加其他功能或与任何新的`CSS`或`Sass`功能兼容。仍在使用它的项目应移至 [`Dart Sass`]() 上。

## 介绍

`node-sass`是一个库，提供了`Node.js`与`LibSass`的绑定，`LibSass`是流行的样式表预处理器`Sass`的`C`版本。
它使您能够以惊人的速度通过连接中间件自动将`.scss`文件本地编译为`css`。

**注意**：`node-sass`是基于`LibSass`的一个`Node.js`库。`LibSass`及其上层包`node-sass`将被废弃，建议使用`Dart Sass`。

## Sass

`Sass`是一种预处理器脚本语言，可以解释或编译成层叠样式表（`CSS`）。

`Sass`包含两种语法：
1. 较旧的语法使用缩进将代码块和换行符分隔为单独的规则；
2. 较新的语法`SCSS`使用像`CSS`这样的块格式。它使用大括号来表示代码块和分号来分隔块中的行。

`缩进语法`和`SCSS`文件传统上分别给出扩展名`.sass`和`.scss`。

## 安装

* 使用淘宝镜像安装
```
// npm安装node-sass
$ npm install -g mirror-config-china --registry = http：//registry.npm.taobao.org
```

* 使用`cnpm`安装，原理还是使用淘宝镜像安装
```
// 安装cnpm（https://npm.taobao.org/）
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
// 在项目文件夹下安装node-sass
$ cnpm install --save-dev node-sass
```

**注意**： 安装好`node-sass`之后，`build`阶段会执行包中的`install`脚本。此时会下载系统`node`依赖文件（如：`darwin-x64-72-bunding.node`）。下载之后会保存在包下面的`vendor`->`darwin`或`linux-x64-72`等文件夹下，保存的文件名字都为`binding.node`。目录名称是`系统`和`node`版本觉得的。



## node-sass相关问题

### Cannot download "https://github.com/sass/node-sass/releases/download/v4.10.0/linux-x64-72_binding.node": 

* 安装好`node-sass`之后，`build`阶段会执行包中的`install`脚本。此时会下载系统`node`依赖文件（如：`darwin-x64-72-bunding.node`）。下载之后会保存在包下面的`vendor`->`darwin`或`linux-x64-72`等文件夹下，保存的文件名字都为`binding.node`。目录名称是`系统`和`node`版本觉得的。

* 下载这个文件的地址默认是：`https://github.com/sass/node-sass/releases/download/v4.10.0/linux-x64-72_binding.node`很可能超时。这时候有如下几种方式处理（这个阶段已经是下载好了`node-sass`，脚本中的下载，所以换源没什么用）。

1. 自己手动输入对应地址，如：`https://github.com/sass/node-sass/releases/download/v4.10.0/linux-x64-72_binding.node`下载好文件，然后修改文件名称放到`vendor`->``linux-x64-72`->`binding.node`。
2. 安装时指定文件地址，前提是如方法一一样，下载好了对应的文件。
查阅源码发现可以设置环境变量`sass_binary_path`指定路径，这样就不用自己去修改文件名称之类的处理了，可以直接获取我们路径下的文件，相当于下载本地文件。设置`SASS_BINARY_PATH`环境变量，目的是告诉程序直接使用本地的`.node`文件，无需从网上下载。
```
npm i node-sass --sass_binary_path=/{path}/linux-x64-72_binding.node
```
3. 安装时指定下载地址：
```
// 使用淘宝镜像源
$ npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass
// 也可以设置系统环境变量的方式。示例
// linux、mac 下
SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/ npm install node-sass

// window 下
set SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/ && npm install node-sass

// 或者设置全局镜像源：
npm config set sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
npm config set phantomjs_cdnurl=https://npm.taobao.org/mirrors/phantomjs/
npm config set electron_mirror=https://npm.taobao.org/mirrors/electron/
npm config set registry=https://registry.npm.taobao.org
// 如上使用 npm install 安装 node-sass、electron 和 phantomjs 时都能自动从淘宝源上下载。
```
查阅源码发现可以设置环境变量`sass_binary_site`指定下载地址。
`extension.js`文件中的获取方法。
```js
/**
 * Determine the URL to fetch binary file from.
 * By default fetch from the node-sass distribution
 * site on GitHub.
 *
 * The default URL can be overridden using
 * the environment variable SASS_BINARY_SITE,
 * .npmrc variable sass_binary_site or
 * or a command line option --sass-binary-site:
 *
 *   node scripts/install.js --sass-binary-site http://example.com/
 *
 * The URL should to the mirror of the repository
 * laid out as follows:
 *
 * SASS_BINARY_SITE/
 *
 *  v3.0.0
 *  v3.0.0/freebsd-x64-14_binding.node
 *  ....
 *  v3.0.0
 *  v3.0.0/freebsd-ia32-11_binding.node
 *  v3.0.0/freebsd-x64-42_binding.node
 *  ... etc. for all supported versions and platforms
 *
 * @api public
 */

function getBinaryUrl() {
  var site = getArgument('--sass-binary-site') ||
             process.env.SASS_BINARY_SITE  ||
             process.env.npm_config_sass_binary_site ||
             (pkg.nodeSassConfig && pkg.nodeSassConfig.binarySite) ||
             'https://github.com/sass/node-sass/releases/download';

  return [site, 'v' + pkg.version, getBinaryName()].join('/');
}

/**
 * Get binary dir.
 * If environment variable SASS_BINARY_DIR,
 * .npmrc variable sass_binary_dir or
 * process argument --sass-binary-dir is provided,
 * select it by appending binary name, otherwise
 * use default binary dir.
 * Once the primary selection is made, check if
 * callers wants to throw if file not exists before
 * returning.
 *
 * @api public
 */

function getBinaryDir() {
  var binaryDir;

  if (getArgument('--sass-binary-dir')) {
    binaryDir = getArgument('--sass-binary-dir');
  } else if (process.env.SASS_BINARY_DIR) {
    binaryDir = process.env.SASS_BINARY_DIR;
  } else if (process.env.npm_config_sass_binary_dir) {
    binaryDir = process.env.npm_config_sass_binary_dir;
  } else if (pkg.nodeSassConfig && pkg.nodeSassConfig.binaryDir) {
    binaryDir = pkg.nodeSassConfig.binaryDir;
  } else {
    binaryDir = defaultBinaryDir;
  }

  return binaryDir;
}

/**
 * Get binary path.
 * If environment variable SASS_BINARY_PATH,
 * .npmrc variable sass_binary_path or
 * process argument --sass-binary-path is provided,
 * select it by appending binary name, otherwise
 * make default binary path using binary name.
 * Once the primary selection is made, check if
 * callers wants to throw if file not exists before
 * returning.
 *
 * @api public
 */

function getBinaryPath() {
  var binaryPath;

  if (getArgument('--sass-binary-path')) {
    binaryPath = getArgument('--sass-binary-path');
  } else if (process.env.SASS_BINARY_PATH) {
    binaryPath = process.env.SASS_BINARY_PATH;
  } else if (process.env.npm_config_sass_binary_path) {
    binaryPath = process.env.npm_config_sass_binary_path;
  } else if (pkg.nodeSassConfig && pkg.nodeSassConfig.binaryPath) {
    binaryPath = pkg.nodeSassConfig.binaryPath;
  } else {
    binaryPath = path.join(getBinaryDir(), getBinaryName().replace(/_(?=binding\.node)/, '/'));
  }

  if (process.versions.modules < 46) {
    return binaryPath;
  }

  try {
    return trueCasePathSync(binaryPath) || binaryPath;
  } catch (e) {
    return binaryPath;
  }
}
```
如上下载地址指定为：`https://npm.taobao.org/mirrors/node-sass`。

4. 创建`.npmrc`文件

* 在项目根目录创建`.npmrc`文件，复制下面代码到该文件。
```
phantomjs_cdnurl=http://cnpmjs.org/downloads
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
registry=https://registry.npm.taobao.org
```
* 保存后删除之前安装失败的包(第一次安装请跳过此步)
```
npm uninstall node-sass
```
* 重新安装
```
npm install node-sass
```

5. 使用`VPN`
```
npm config set proxy (http://127.0.0.1:1080)此处是VPN的代理地址
npm i node-sass
```
下载完成后删除 `http` 代理
```
npm config delete proxy
```

比较推荐第三种方法或第四种。

### node版本切换，node-sass报错

报错信息如下：
```
Error: Missing binding /Users/matias/matias_bbd/bbd_git/FECB/SC-FECB-monitor/node_modules/node-sass/vendor/darwin-x64-72/binding.node
Node Sass could not find a binding for your current environment: OS X 64-bit with Node.js 12.x

Found bindings for the following environments:
  - OS X 64-bit with Node.js 10.x

This usually happens because your environment has changed since running `npm install`.
Run `npm rebuild node-sass` to download the binding for your current environment.
```

原因就是：没有找到`系统`和`node`版本对应的`binding.node`文件。这时我们需要执行：`npm rebuild node-sass`命令，让`node-sass`中重新`build`，重新执行`install`脚本，下载对应的依赖文件。如果下载时报错请查看`Cannot download "https://github.com/sass/node-sass/releases/download/v4.10.0/linux-x64-72_binding.node"`的解决方案。

### 使用了淘宝源还无法下载`linux-x64-72_binding.node`文件

如：
```
$ npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass
```
下载`linux-x64-72_binding.node`时，提示`404`，这时候就要看`node-sass`和`node`的版本是否对应。