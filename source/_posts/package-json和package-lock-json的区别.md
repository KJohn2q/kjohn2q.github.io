---
title: package.json和package-lock.json的区别
tags:
  - npm
  - package
  - nodejs
categories:
  - 笔记
date: 2021-11-06 10:41:33
---


在我刚开始接触 `npm` 包时，常会困惑 `package.json` 和 `package-lock.json` 各自的作用和两者的区别。本篇文章就详细梳理一下：

##  生成package.json

新建一个空目录，执行 `npm init`， 会提示你输入包名，版本号，描述，入口文件等信息，引导在当前目录生成  `package.json` 文件，如全部默认，则文件内容为：

```
{
  "name": "pack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

```

![image-20211106113604539](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111061136595.png)

## 生成 package-lock.json

当我们安装软件包时，改文件会发生变化。如在当前目录下安装 `hexo-cli`

```
npm install hexo-cli
```

安装完成后，会在 `package.json` 文件中，插入下面的内容

```
"dependencies": {
    "hexo-cli": "^4.3.0"
  }
```

`dependencies` 表明了当前项目所依赖的包。同时会在当前目录中生成 `node_modules` 文件夹和 `package-lock.json` 文件。

![image-20211106113824866](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111061138926.png)

`package-lock.json` 显示当前项目依赖的所有包，包括依赖包的依赖。

```json
"hexo-cli": {
      "version": "4.3.0",
      "resolved": "https://registry.npmjs.org/hexo-cli/-/hexo-cli-4.3.0.tgz",
      "integrity": "sha512-lr46h1tK1RNQJAQZbzKYAWGsmqF5DLrW6xKEakqv/o9JqgdeempBjIm7HqjcZEUBpWij4EO65X6YJiDmT9LR7g==",
      "requires": {
        "abbrev": "^1.1.1",
        "bluebird": "^3.5.5",
        "chalk": "^4.0.0",
        "command-exists": "^1.2.8",
        "hexo-fs": "^3.0.1",
        "hexo-log": "^2.0.0",
        "hexo-util": "^2.0.0",
        "minimist": "^1.2.5",
        "resolve": "^1.11.0",
        "tildify": "^2.0.0"
      }
    },
```

需要注意的是，`node_modules` 树或 `package.json`文件的更新，都会自动生成 `package-lock.json`

## package.json和package-lock.json的作用

* `package.json` 定义了所有项目相关属性：名称，版本号，依赖项，入口文件，运行脚本等。使得 `npm` 能识别该项目，知道该项目如何安装依赖，如何启动。
* `package-lock.json` 是要提交到代码仓库中去的，有以下几点作用：
  - 描述了依赖项的实际版本号，使得同事在部署和持续集成时能安装相同的依赖
  - 描述了 `node_modules` 的状态，无需将 `node_modules`提交到代码仓库中
  - 通过避免重复解析之前安装过的包，优化安装进程
  - 通过版本控制中的 `diff` 工具，能清晰地看到依赖树的变更

## package.json和package-lock.json的区别

* `package-lock.json` 描述了每个依赖项的实际版本号，使得在重新安装依赖项时能得到相同的依赖树
* `package.json` 描述了应用依赖项的最低版本。单个依赖项的版本更新，不会反映到该文件中

如上面提到的例子，安装完 `hexo-cli` 后，`package.json` 中依赖项 `hexo-cli` 保存的版本为 `^4.3.0`。 `^` 表示该项目支持 `4.3.0`及更高的版本。而` package-lock.json` 中依赖项 `hexo-cli`保存的版本为 `4.3.0`， 为实际安装的版本。

`npm install` 不带任何选项默认会读取 `package.json` 中的依赖项来进行安装，这样可能使得 `node_modules` 依赖树不一致的情况，而在一个项目中如果有 `package-lock.json`，`npm ci`会读取 `package-lock.json`中依赖项的定义来进行安装，确保依赖树一致。

## 引用

* [What Is package.json?](https://heynode.com/tutorial/what-packagejson/)
* [package-lock.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-lock-json)
* [package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
* [package.json Vs package-lock.json](https://medium.com/dlt-labs-publication/package-json-vs-package-lock-json-c8d5deba12cb)

