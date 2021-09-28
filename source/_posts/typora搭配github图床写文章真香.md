---
title: typora搭配github图床写文章真香
date: 2021-09-28 09:00:01
tags: [typora, github, 图床，博客，markdown]
categories: [tool]
---

平时写博客，记录知识用的最多的就是 [Typora](https://typora.io/). `typora` 是一歀简洁，优雅，高效的 `markdown` 文件编辑器。当插入图片时，图片会保存在 `C:/Users/[用户名]/AppData/Roaming/Typora/typora-user-images/文件名` 中，文章写好后，需要将图片同步上传到云端，可供他人访问，或在其它平台引用。这时就需要用到图床，也就是一个云端图片存储的地方。常见的图床有：`sm.ms`,   腾讯云 `cos`, 微博图床，七牛云， 阿里云 `oss`等。我主要使用 `github+jsdelivr cdn` 的方式。完全免费，稳定且几乎无限制。

## github 新建图床仓库

`github` 新建一个公共的仓库，以 `image-gallery` 为例

![image-20210928105538243](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928105538.png)

打开`settings`-> `Developer settings` -> `Personal access tokens` ，新建一个 `token`

![image-20210928110138862](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928110138.png)

验证密码后，填入 `token` 信息，生成 `token`

![image-20210928110445510](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928110445.png)

![image-20210928110626114](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928110626.png)

保存好新生成的`token`，只会出现一次，如果没有保存，就需要重新生成

![image-20210928110905660](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928110905.png)

## picgo 配置图床信息

[picgo下载地址](https://github.com/Molunerfinn/PicGo/releases)

安装好后，配置 `github` 图床， 仓库名为之前新建的仓库  `KJohn2q/image-gallery`， 分支名为  `main`,  `token` 为之前新建的  `token`,  存储路径可自定义，我设置的是 `image/`， 自定义域名先不填

![image-20210928112656761](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928112656.png)

### github 图床搭配 CDN

github的服务器在国外，故访问速度及稳定性有时会出一些问题。我们可以搭配 `CDN` 来使用。推荐使用  [jsDelivr](https://www.jsdelivr.com/). `jsDelivr` 是一款用于开源项目的免费公共 `CDN`, 与国内的 `CDN` 厂商也有合作。

直接配置自定义域名为  `https://cdn.jsdelivr.net/gh/[用户名]/[仓库名]`， 如  `https://cdn.jsdelivr.net/gh/KJohn2q/image-gallery`

![image-20210928113452717](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928113452.png)

## typora 插入图片

图床配置好后，我们可以使用两种方式在 `typora` 中插入图片，第一种方法是：先在 `picgo` 中上传图片，在 `typora` 中插入图片的 `markdown` 链接，另一种方法是： 直接在 `typora` 中插入图片，图片自动通过 `picgo` 上传到图床， 替换本地 `markdown` 链接

###  typora 配置图片自动上传

打开偏好设置 -> 图像 , 插入图片时选项改为自动上传, 勾选对本地位置的图片应用上述规则。上传服务设定中，上传服务选择 `PicGo(app)`, `PicGo` 路径选择 `PicGo`的安装路径，通常为 `C:\Program Files\PicGo\PicGo.exe` 

![image-20210928114253032](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928114253.png)

## 上传图片测试

![image-20210928114923508](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/20210928114923.png)

可以看到图片已经上传到  `github` 图床，并使用了 `jsdelivr cdn` 加速

## 引用

* [图床对比与Github图床的优化](https://lovelijunyi.gitee.io/posts/a833.html)
* [jsDelivr - A free, fast, and reliable CDN for open source](https://www.jsdelivr.com/)

  

