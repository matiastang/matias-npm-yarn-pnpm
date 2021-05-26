<!--
 * @Author: tangdaoyong
 * @Date: 2021-05-26 11:21:36
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-05-26 16:18:00
 * @Description: dart-sass
-->
# dart-sass

[dart-sass 文档](https://sass-lang.com/dart-sass)
[dart-sass中文网](https://sass.bootcss.com/dart-sass)

## 介绍

`Dart Sass` 是 `Sass` 的主要实现版本，这意味着它集成新 功能要早于任何其它的实现版本。`Dart Sass` 速度快、易于安装，并且 可以被编译成纯 `JavaScript` 代码，这使得它很容易集成到现代 `web` 的开发流程中。

## 安装

### 命令行

[sass 安装](https://sass.bootcss.com/install)

`Dart Sass` 的独立命令行可执行文件是跑在高速的 `Dart 虚拟机`（`VM`）上来编译你的样式代码的。如需在命令行上安装 `Dart Sass`。 安装之后，你就可以使用它来编译源码文件了：
```
$ sass source/index.scss css/index.css
```
执行 `sass --help` 即可获取关于命令行界面的额外信息。

* 全局安装
```
// npm 安装
$ npm install -g sass 
// yarn 安装
$ yarn add -g sass 
// pnpm 安装
$ pnpm add -g sass
```

* 查看版本
```
$ sass --version   
1.34.0 compiled with dart2js 2.13.0
```

* help
```
$ sass --help   
Compile Sass to CSS.

Usage: sass <input.scss> [output.css]
       sass <input.scss>:<output.css> <input/>:<output/> <dir/>

━━━ Input and Output ━━━━━━━━━━━━━━━━━━━
    --[no-]stdin               Read the stylesheet from stdin.
    --[no-]indented            Use the indented syntax for input from stdin.
-I, --load-path=<PATH>         A path to use when resolving imports.
                               May be passed multiple times.
-s, --style=<NAME>             Output style.
                               [expanded (default), compressed]
    --[no-]charset             Emit a @charset or BOM for CSS with non-ASCII characters.
                               (defaults to on)
    --[no-]error-css           When an error occurs, emit a stylesheet describing it.
                               Defaults to true when compiling to a file.
    --update                   Only compile out-of-date stylesheets.

━━━ Source Maps ━━━━━━━━━━━━━━━━━━━━━━━━
    --[no-]source-map          Whether to generate source maps.
                               (defaults to on)
    --source-map-urls          How to link from source maps to source files.
                               [relative (default), absolute]
    --[no-]embed-sources       Embed source file contents in source maps.
    --[no-]embed-source-map    Embed source map contents in CSS.

━━━ Other ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
-w, --watch                    Watch stylesheets and recompile when they change.
    --[no-]poll                Manually check for changes rather than using a native watcher.
                               Only valid with --watch.
    --[no-]stop-on-error       Don't compile more files once an error is encountered.
-i, --interactive              Run an interactive SassScript shell.
-c, --[no-]color               Whether to use terminal colors for messages.
    --[no-]unicode             Whether to use Unicode characters for messages.
-q, --[no-]quiet               Don't print warnings.
    --[no-]quiet-deps          Don't print compiler warnings from dependencies.
                               Stylesheets imported through load paths count as dependencies.
    --[no-]verbose             Print all deprecation warnings even when they're repetitive.
    --[no-]trace               Print full Dart stack traces for exceptions.
-h, --help                     Print this usage information.
    --version                  Print the version of Dart Sass.
```

### Dart库

[安装 Dart SDK](https://www.dartlang.org/install#automated-installation-and-updates)

* 查看版本
```
$ dart --version
Dart SDK version: 2.13.0 (stable) (Wed May 12 12:45:49 2021 +0200) on "macos_x64"
```

* 创建一个 `pubspec.yaml` 文件，内容如下：
```
name: my_project
dev_dependencies:
  sass: ^1.26.4
```

* 执行 `pub get` 命令。
* 创建一个 `compile-sass.dart` 文件，内容如下：
```dart
import 'dart:io';
import 'package:sass/sass.dart' as sass;

void main(List<String> arguments) {
  var result = sass.compile(arguments[0]);// sass编译第一个参数地址文件
  new File(arguments[1]).writeAsStringSync(result);// 编译结果输出到第二个参数地址
}
```
* 现在就可以使用此命令来编译文件了（就是使用刚刚创建的`.dart`脚本文件进行编译）：
```
$ dart compile-sass.dart styles.scss styles.css
```

### JavaScript 工具库

[Dart Sass npm package](https://npmjs.com/package/sass)

`Dart Sass` 还被编译为纯 `JavaScript` 并在 `npm` 上作为 `sass` 软件包 发布。 纯 `JS` 版本 比独立版本执行速度慢，但是它很容易集成到 现有的工作流中，并且允许你通过 `JavaScript` 自定义函数和 `importer`。通过执行 `npm install --save-dev sass` 命令将其添加到项目中并通过 `require()` 引入。
```js
var sass = require('sass');

sass.render({
  file: scss_filename
}, function(err, result) {
  /* ... */
});

// OR

var result = sass.renderSync({
  file: scss_filename
});
```
通过 `npm` 安装时，`Dart Sass` 提供了一个 `JavaScript API` 用于 兼容 `Node Sass`。 完全兼容的工作正在进行中，但是 `Dart Sass` 目前支持 `render()` 和 `renderSync()` 函数。不过，请注意，默认情况下 `renderSync()` 的速度是 `render()` 的两倍以上，这是由于 异步回调所带来的开销而导致的。

为了避免这种性能的下降，`render()` 可以使用 [`fibers`](https://www.npmjs.com/package/fibers) 软件包在同步代码的执行路径中调用异步 `importers` 。如需开启此功能，请将 `Fiber` 类传递给 `fiber` 参数：
```js
var sass = require("sass");
var Fiber = require("fibers");

sass.render({
  file: "input.scss",
  importer: function(url, prev, done) {
    // ...
  },
  fiber: Fiber
}, function(err, result) {
  // ...
});
```

## 使用

[dart-sass github](https://github.com/sass/dart-sass/blob/master/README.md#javascript-api)