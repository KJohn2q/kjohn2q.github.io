---
title: github高效搜索
date: 2019-12-26 09:04:25
tags: github
categories: tool
---

## 概述

github是全球最大的开源项目网站，集聚了非常多优质的开源项目，我们可以利用它，学习优秀代码，行业前沿知识，动手实践。

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20191226085939.png)

上图为vue项目的主页，其中`name`为项目名称，description为项目的简要描述，`star`为项目的受关注程度，`fork`反映多少人克隆到了自己的仓库。除了这几个要素，还有项目的最后更新日期（`pushed`），项目的编程语言（`language`）,项目的创建日期（`create`）都可以作为我们搜索我们想要的项目时的依据。


## 高效搜索

以swoole举例

### `in:name swoole`

搜索仓库的名称，搜索仓库名称包含swoole关键字的所有项目

### `in:description swoole`

搜索描述中包含swoole关键字的项目

### `in:readme swoole`

搜索`readme`文件中包含`swoole`关键字的项目

### `start:>100 swoole`

搜索`swoole`关键字项目中关注超过100个的项目

### `fork:>100 swoole`

搜索`fork`超过100的`swoole`的项目

### `pushed:>2019-01-10 swoole`

搜索包含`swoole`项目，并且仓库1月10日后还有更新的项目

### `create:>2019-01-10 swoole`

搜索项目1月10日后创建的项目

### `language:php shop`

搜索编程语言是`php`的`shop`项目

### `user:kjohn2q language:php`

搜索用户是`kjohn2q` 开发语言是`php`的项目