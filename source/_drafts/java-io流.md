---
title: java io流
date: 2021-12-04 16:40:13
tags: [io, stream, java]
categories: [java]
---

`java io `流提供了可以从网络设备，缓冲区，文件，管道和数组中输入，输出的一切。

## Stream

流这个概念源于水流。可表示为一系列数据。有两种数据流：

* `InputStream` 输入流，用于从源中读取数据
* `OutputStream` 输出流，用于将数据写入到目标位置

![Streams](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112041647284.png)

## java中io流的种类

* 按流向划分为输入流和输出流
* 按操作单元可划分为字节流和字符流
* 按流的角色可划分为节点流和处理流

## java中io流类的层级结构

`java io`流类都是从以下四个抽象类中派生出来的。

* `InputStream` / `Reader`，所有输入流的基类。前者是字节输入流，后者是字符输入流。
* `OutputStream` / `Writer`，所有输出流的基类。前者是字节输出流，后者是字符输出流。

类层级结构图：

![Files IO](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112041657421.jpeg)



按操作方式分类结构图：

![IO-操作方式分类](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112041655170.png)

按操作对象分类结构图：

![IO-操作对象分类](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112041656705.png)

## 引用

* [Java - Files and I/O](https://www.tutorialspoint.com/java/java_files_io.htm)
* [Java 中 IO 流](https://snailclimb.gitee.io/javaguide-interview/#/./docs/b-1面试题总结-Java基础?id=_2132-java-中-io-流)
