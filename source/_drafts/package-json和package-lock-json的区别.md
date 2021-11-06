---
title: package.json和package-lock.json的区别
date: 2021-11-06 10:41:33
tags: [npm, package, nodejs]
categories: [笔记]
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

## package.json和package-lock.json的作用

## package.json和package-lock.json的区别
