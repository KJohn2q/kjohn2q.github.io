---
title: npm全局和局部安装的区别
tags:
  - npm
  - nodejs
  - node
categories:
  - 笔记
date: 2021-11-05 14:54:58
---


`npm` 是基于 `nodejs` 开发的`javascript` 包管理器，用于管理开发中软件包的依赖关系，从远程仓库中下载我们需要的工具。我的博客就是基于 `hexo` 来构建的，我们可以通过  `npm install hexo-cli -g`  来安装 `hexo-cli` 工具。那么 `-g` 表示什么意思？与不带 `-g` 有什么区别？

## npm 安装

`npm` 安装软件有两种方式 ：局部安装和全局安装。为了测试，我们使用 `npm`初始化一个包。

```
mkdir -p pack
npm init
```

![image-20211105155130555](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051551886.png)

### 局部安装

```
npm install [package/module]
```

局部安装会在将包/模块安装在当前目录的 `node_modules` 目录中。以 `hexo-cli` 为例

```
npm install hexo-cli
```

安装完成后，当前目录中多了一个 `node_modules`目录。

![image-20211105155258331](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051552385.png)

`node_modules`目录中有 `hexo-cli`目录

![image-20211105155741122](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051557163.png)

`hexo-cli`提供了一些命令如 `hexo init`, `hexo generate` 等。此时，测试一下 `hexo` 命令, 新建一个博客目录，并执行 `hexo init`

![image-20211105160828637](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051608683.png)

提示命令不存在，可是我们已经安装了 `hexo-cli`，这是什么情况呢？其实局部安装，只会将包或模块安装在当前目录中。检查`node_modules`目录，可以看到其中有个 `.bin`隐藏目录，提供了 `hexo`命令的软链接。而 `shell`不会在当前目录的  `node_modules/hexo-cli/bin/hexo`或 `node_modules/.bin` 中查找 `hexo`命令，故提示命令不存在

![image-20211105161534828](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051615876.png)

可以通过使用全路径或者使用 `npx` 来执行 `hexo` 命令。

![image-20211105164034467](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051640522.png)

![image-20211105164107829](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051641884.png)

## 全局安装

```
npm install -g [package/module]
```

与局部安装不同，全局安装会将包或模块安装在 `prefix` 目录中，而不是当前目录。

* 软件包安装在 `{prefix}/lib/node_modules`中
* 可执行文件链接到了 `{prefix}/bin`
* 帮助页面链接到了 `{prefix}/share/man`

检查 `prefix`的值

```
npm config ls -l
```

![image-20211105165203966](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051652022.png)

以 `hexo-cli`为例：

```
npm install -g hexo-cli
```

安装完成后，检查安装情况

![image-20211105165421065](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051654118.png)

此时，在 `blog`目录中，测试 `hexo` 命令

![image-20211105165735196](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111051657247.png)

## 总结

`npm` 局部安装会将包安装在当前目录中，适用于不想全局安装，仅仅只在当前目录中引用模块或局部使用包的情况。 而全局安装会将包安装在指定的目录（`shell`可以读取），使得包在其它目录也可以使用。

## 引用

* [npm-install](https://docs.npmjs.com/cli/v7/commands/npm-install)