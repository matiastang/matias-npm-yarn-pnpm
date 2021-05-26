# n

[n github地址](https://github.com/tj/n)
[n npm package](https://www.npmjs.com/package/n)

## 介绍

`n`是`node`一个模块，可以用来管理和切换`node`版本，其作者是`TJ Holowaychuk`（出名的`Express`框架作者），使用非常之简单。

**注意**， `n` 不支持 `Windows`(Unfortunately n is not supported on Windows yet. If you're able to make it work, send in a pull request!)。

## 安装

安装`n`需要先安装`node`。

1. 查看`node`版本。
```
$ node -V
```
2. 清除`node`缓存
```
$ sudo npm cache clean -f
```
3. 安装`n`，`sudo`执行命令，需要输入机器密码。
```
$ sudo npm install n -g
```

## 使用


* 安装
安装指定版本的`node`
升级到最新版本`node`。
```
$ sudo n <version>  //安装某个版本并使用，如$n 6.2.2
$ sudo n 10.15.0 // 安装node指定版本/切换版本
$ sudo n latest  // 安装最新版本并使用
$ sudo n latest -d   // 下载最新版但不使用，-d参数表示为仅下载
$ sudo n stable  // 安装最新稳定版本并使用
```
* 查看
```
$ n ls    //查看可用版本
$ n --latest    //查看最新版本
$ n --stable    //查看最新稳定版
```

* 切换版本
```
$ n //查看已安装版本，选择版本切换
```

* 移除
```
$ sudo n rm <version ...> //删除某些版本
```

* 查看help文档。
```
$ n help
$ n h //查看帮助信息，更多命令在这里查看
```
如下：
```
$ n help

Usage: n [options] [COMMAND] [args]

Commands:

  n                              Display downloaded node versions and install selection
  n latest                       Install the latest node release (downloading if necessary)
  n lts                          Install the latest LTS node release (downloading if necessary)
  n <version>                    Install node <version> (downloading if necessary)
  n run <version> [args ...]     Execute downloaded node <version> with [args ...]
  n which <version>              Output path for downloaded node <version>
  n exec <vers> <cmd> [args...]  Execute command with modified PATH, so downloaded node <version> and npm first
  n rm <version ...>             Remove the given downloaded version(s)
  n prune                        Remove all downloaded versions except the installed version
  n --latest                     Output the latest node version available
  n --lts                        Output the latest LTS node version available
  n ls                           Output downloaded versions
  n ls-remote [version]          Output matching versions available for download
  n uninstall                    Remove the installed node and npm

Options:

  -V, --version         Output version of n
  -h, --help            Display help information
  -p, --preserve        Preserve npm and npx during install of node (requires rsync)
  -q, --quiet           Disable curl output (if available)
  -d, --download        Download only
  -a, --arch            Override system architecture
  --all                 ls-remote displays all matches instead of last 20
  --insecure            Turn off certificate checking for https requests (may be needed from behind a proxy server)
  --use-xz/--no-use-xz  Override automatic detection of xz support and enable/disable use of xz compressed node downloads.

Aliases:

  which: bin
  run: use, as
  ls: list
  lsr: ls-remote
  rm: -
  lts: stable
  latest: current

Versions:

  Numeric version numbers can be complete or incomplete, with an optional leading 'v'.
  Versions can also be specified by label, or codename,
  and other downloadable releases by <remote-folder>/<version>

    4.9.1, 8, v6.1    Numeric versions
    lts               Newest Long Term Support official release
    latest, current   Newest official release
    auto              Read version from file: .n-node-version, .node-version, .nvmrc, or package.json
    boron, carbon     Codenames for release streams
    lts_latest        node support aliases

    and nightly, chakracore-release/latest, rc/10 et al
```