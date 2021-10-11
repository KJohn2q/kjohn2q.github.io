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

此时，如果 `C` 看到了 `B` 收到的信息，因为没有加密，能清楚看到信息内容为 `Hello`

![image-20211011153508522](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111535586.png)

`A` 意识了此问题，和 `B` 协商了个密码。以后 `A` 在发送信息的时候先用协商好的密钥对信息内容进行加密，`B` 在收到信息后使用密钥对收到的信息进行解密，得到真实的消息内容。同一个密钥对信息进行加密和解密，这种方式称之为**对称加密**（`symmetric encryption`）。

![image-20211011154820482](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111548541.png)

此时，如 `C` 看到 `B` 收到由 `A` 发送的信息，得不到真实的内容

![image-20211011155316727](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110111553785.png)



## 引用

* [What is a Digital Signature?](http://www.youdzone.com/signature.html)