---
title: windows10下修改docker镜像存储位置
date: 2021-11-04 15:55:45
tags: [docker, 镜像, windows, wsl]
categories: 笔记
---

## docker 镜像占用空间问题描述

在平时使用 `docker` 过程中，使用一段时间后，经常会出现 `C` 盘爆满的情况，不得已去清理 `C` 盘空间，保证系统正常使用。

![image-20211104155929332](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111041559044.png)

如 `docker`  使用 `wsl2` 作为基础引擎，则 `docker` 镜像默认存储在 `%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx`。可以通过 `Settings` -> `General` 查看是否使用了 `wsl2`

![image-20211104160655271](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111041606488.png)

可以通过修改 `docker` 镜像存储位置，将 `docker`镜像存储在 `HDD` 中，不影响系统正常使用。

## 修改镜像存储位置

首先，需要关闭 `docker desktop`，可以通过右击任务栏  `docker` 图标，点击 `Quit Docker Desktop `

![image-20211104161227253](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111041612312.png)

打开命令行，检查运行状态

``` 
wsl --list -v
```

确保状态均为 `Stopped`

![image-20211104161719233](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111041617285.png)

导出 `docker-desktop-data` 

```
wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
```

如提示文件夹不存在，可新建文件夹后再次执行

```
mkdir D:/Docker/wsl/data/ -ea 0
```

在 `wsl`中注销 `docker-desktop-data`， 需要注意的是这一步会自动删除 `ext4.vhdx` 文件，如有重要的镜像或容器，可以先备份

```
wsl --unregister docker-desktop-data
```

将 `docker-desktop-data` 备份导入到  `wsl`中，指定新的存储位置

```
wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
```

接下来，可以再次启动 `docker desktop`，之后拉取或新创建的镜像会存储在新的位置

如测试没有问题，可将 `D:\Docker\wsl\data\docker-desktop-data.tar` 文件删除。

## 引用

* [How can I change the location of docker images when using Docker Desktop on WSL2 with Windows 10 Home?](https://stackoverflow.com/questions/62441307/how-can-i-change-the-location-of-docker-images-when-using-docker-desktop-on-wsl2)
* [Where is docker image location in Windows 10?](https://stackoverflow.com/questions/42250222/where-is-docker-image-location-in-windows-10)
* [powershell equivalent of linux "mkdir -p"?](https://stackoverflow.com/questions/47357135/powershell-equivalent-of-linux-mkdir-p)