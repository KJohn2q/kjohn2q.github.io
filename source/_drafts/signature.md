---
title: signature
date: 2021-10-11 11:14:25
tags: [加密，非对称，签名]
categories: [笔记]
---

## 加密

在如今的互联网世界中，我们不可避免的会传输敏感信息：服务器的账户密码，身份证号，或者仅仅是你想和某人说话，不想让其他人听见。那如何实现安全、有效的向对方传输信息呢？这就需要对信息进行加密。接下来我将通过一个例子进行表述：

### 信息发送步骤

想象一下

`A` 要给 `B` 发送消息 `Hello` 。刚开始对信息没有任何加密

![image-20211011111533617](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111115034.png)

此时，如果有不怀好意的 `C`  , 可以对数据包劫持。因为没有任何加密，`C` 能看到信息内容为 `Hello`

![image-20211011112136572](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111121624.png)

`A` 意识到了这个问题，于是和 `B` 协商了密码和加密算法，用于信息的加密。如选择加密算法为 `AES`, 密码为 `123456`, 则对 `Hello` 加密后，结果为  `U2FsdGVkX1+tSNz3t5BLBi97cEu+9WavFv3mdrf3NGQ=`   加密工具地址： [文本加密解密 - 一个工具箱 - 好用的在线工具都在这里！ (atoolbox.net)](http://www.atoolbox.net/Tool.php?Id=679)。`B` 在收到信息的时候，依据约定好的加密算法和密码对信息进行解密，得到真实的信息内容。这种加密方式称之为对称加密（`sysmetric encryption`）。

![image-20211011114218625](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111142676.png)

此时，如 `C` 再对数据包进行劫持，则只能看到加密后的结果。不知道真实信息

![image-20211011115448821](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111154890.png)

## 引用

* [What is a Digital Signature?](http://www.youdzone.com/signature.html)