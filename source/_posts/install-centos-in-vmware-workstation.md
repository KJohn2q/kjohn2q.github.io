---

title: install centos in vmware workstation
date: 2021-09-27 14:03:45
tags: [linux, vmware, centos]
categories: 笔记
---

本文档演示如何在 `vmware` 中新建一个 `centos` 的虚拟机。

## 镜像下载

centos源列表：

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927112748.png)

* [centos7 isos](http://isoredirect.centos.org/centos/7/isos/x86_64/)
* [centos8 isos](http://isoredirect.centos.org/centos/8/isos/x86_64/)

受限于网络环境，推荐以下镜像源：

* [163](http://mirrors.163.com/centos/7.9.2009/isos/x86_64/)
* [清华](http://mirrors.tuna.tsinghua.edu.cn/centos/7.9.2009/isos/x86_64/)
* [阿里云](http://mirrors.aliyun.com/centos/7.9.2009/isos/x86_64/)

### 版本选择

打开 `163` 镜像源地址，可以看到有四个版本供我们选择

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927114433.png)

分别为 `DVD`, `Everything`, `Minimal`, `NetInstall`

* `DVD`: 如果你不知道使用哪个镜像，就选择这个版本。该版本允许你在安装时选择自己想要安装的组件。
* `Everything`: 包含所有可用的软件包，包括那些不能直接通过安装程序安装的包。如果需要安装其它的包，可在系统安装后挂载安装媒体，从那里复制或安装包。对大多数用户来说，直接使用  `DVD`  镜像安装，随后使用 `yum install` 来安装其它的包是更容易的。
* `Minimal`:  最基础的系统，会安装一些系统功能所需的基础包。
* `NetInstall`:  通过网络进行安装或恢复的镜像。

## 新建虚拟机

打开 `vmware` ，文件 -> 新建虚拟机，选择自定义后，下一步

![image-20210927144407592](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927144407.png) 

下一步。

![image-20210927144524851](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927144524.png)

选择稍后安装操作系统，下一步。

![image-20210927144707464](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927144707.png)

选择客户机操作系统类型为 `Linux` ， 版本为 `CentOS7 64位`。 下一步

![image-20210927144807436](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927144807.png)

修改新建虚拟机的名称，指定该虚拟机放置的目录。如图所示，虚拟机名称为 `centos7_test_node`, 位置为 `D:\virtural machine\centos7 test node`。需要特别说明的是，新建虚拟机并不会生成虚拟机名称同名的文件夹，故我们需要指定一个空目录来放置新建的虚拟机。下一步。

![image-20210927145319367](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927145319.png)

处理器配置保持默认，下一步。

![image-20210927145634792](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927145634.png)

内存配置选择 `512M`，基本够用。下一步

![image-20210927145746773](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927145746.png)

网络模式选择 `NAT`, 在之前的文章 [vmware 虚拟机联网的三种方式](https://kjohn2q.github.io/2020/vmware-%E8%99%9A%E6%8B%9F%E6%9C%BA%E8%81%94%E7%BD%91%E7%9A%84%E4%B8%89%E7%A7%8D%E6%96%B9%E5%BC%8F/) 已经详细说明过。下一步

![image-20210927150053427](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150053.png)

`IO` 控制器 和 磁盘类型保持默认。下一步

![image-20210927150124572](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150124.png)

![image-20210927150140646](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150140.png)

选择创建新虚拟硬盘。下一步

![image-20210927150248376](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150248.png)

最大磁盘大小保持默认即可，选择将虚拟磁盘存储为单个文件。下一步

![image-20210927150351844](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150351.png)

保持默认，下一步。

![image-20210927150509757](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150509.png)

选择自定义硬件，移除无用的虚拟设备（打印机，声卡，`USB` 控制器）。并指定使用`ISO` 映像文件的位置。使用此镜像来为虚拟机安装操作系统。关闭。

![image-20210927150538935](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150539.png)

![image-20210927150734740](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927150734.png)

点击完成。

![image-20210927151000212](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927151000.png)

## 安装操作系统

开启此虚拟机，安装操作系统。

![image-20210927151103071](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927151103.png)

光标定位到虚拟机中，选择 `Install Centos 7` 。 回车

![image-20210927151334041](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927151334.png)

等待跑码后，出现该界面。因为我们要安装的是服务器的操作系统，不会安装桌面。故保持默认 `Continue`

![image-20210927151613118](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927151613.png)

出现该界面后，需要修改下时区，选择要安装系统的硬盘，关闭 `KDUMP` , 启用网卡。

![image-20210927151833814](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927151833.png)

首先点击  `DATE & TIME` ,进行时区的设置, 选择图中所示位置 `Asia Shanghai`. 点击 `Done`

![image-20210927152244374](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927152244.png)

点击 `INSTALLATION DESTATION` ,指定系统安装的位置。选中之前新建的硬盘，点击 `Done`

![image-20210927152450046](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927152450.png)

点击 `NETWORK & HOST NAME`, 开启网卡。 点击 `Done`

![image-20210927152207712](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927152207.png)

点击 `KDUMP`. 取消勾选  `Enable kdump`  。`Kdump` 是一种崩溃转储机制。当系统发生故障时，会抓取一些导致系统崩溃的关键信息，但会占用一部分内存。点击 `Done`

![image-20210927152825901](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927152826.png)

点击 `SOFTWARE SELECTION` 后可选择要安装的包。如之前使用的是 `Minal` 版本的镜像，则如下图所示

![image-20210927142512809](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927142512.png)

如之前使用的是 `DVD` 版本的镜像，则如下图所示

![image-20210927144030197](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927144030.png)

点击 `Begin Installation` 开始安装。点击 `ROOT PASSWORD` 设置 `Root`账户密码。

![image-20210927153228381](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927153228.png)

输入密码，确认密码，后点击 `Done`。 密码尽量为数字，大小写字幕，特殊符号的组合。否则会提示弱密码

![image-20210927153752121](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927153752.png)

等待安装完成后，点击 `Reboot` 重启

![image-20210927154940640](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927154940.png)

输入用户名和密码，回车。

![image-20210927155437426](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927155437.png)

### 网络配置

首先，检查虚拟 `DHCP` 服务器分配的  `IP` 地址。如图所示，自动分配的 `IP` 地址为 `192.168.9.130`

 ```
ip addr
 ```

![image-20210927155649705](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927155649.png)

修改网络配置，设置静态 `IP` 地址。

```
vi /etc/sysconfig/network-scripts/ifcfg-ens32
```

![image-20210927160115404](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927160115.png)

将 `BOOTPROTO` 从 `dhcp` 改为 `static`, 增加以下几行。`IPADDR`  为 `IP` 地址， `PREFIX` 为网络号的位数，`24` 表示子网掩码为 `255.255.255.0` ,  `GATEWAY` 为默认网关， `DNS1` 为主要的 `dns`.网关可以在 `NAT` 配置中找到

```
IPADDR=192.168.9.130
PREFIX=24
GATEWAY=192.168.9.2
DNS1=114.114.114.114
```

默认网关

![image-20210927160417810](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927160417.png)

最终配置如下

![image-20210927160713637](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927160713.png)

配置好后，重启网络配置 

```
service network restart
```

![image-20210927161333063](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927161333.png)

测试网络连接

```
ping baidu.com
```

![image-20210927161648471](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927161648.png)

网络连接正常，配置完成。

## 使用 SecureCRT 连接虚拟机

在`vmware` 中操作很不方便，界面又不美观。通常我们会使用 `SSH` 客户端连接虚拟机进行操作, 常用的有 `SecureCRT` 和  `xshell`.

### 使用 `SecureCRT` 连接

打开 `SecureCRT`,  `File` ->  `Quick Connect` ，输入要连接的虚拟机的地址 `192.168.9.130`，用户名 `root`

![image-20210927162303367](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927162303.png)

点击 `Accept & Save` 

![image-20210927162425095](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927162425.png)

输入密码，点击 `ok`

![image-20210927162557133](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927162557.png)

此时就可以在 `SecureCRT` 中对虚拟机进行操作了。

![image-20210927162749385](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210927162749.png)

##  系统更新

```
yum update
```

如下载速度比较慢或无法下载，则需要更换软件源：

网易、清华大学和阿里云都提供了对应的解决方案。

* [网易CentOS镜像使用帮助](https://mirrors.163.com/.help/centos.html)
* [阿里云 centos镜像](https://developer.aliyun.com/mirror/centos)
* [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/centos/)

> 先备份 `/etc/yum.repos.d/` 内的文件（CentOS 7 及之前为 `CentOS-Base.repo`，CentOS 8 为`CentOS-Linux-*.repo`）
>
> 然后编辑 `/etc/yum.repos.d/` 中的相应文件，在 `mirrorlist=` 开头行前面加 `#` 注释掉；并将 `baseurl=` 开头行取消注释（如果被注释的话），把该行内的域名（例如`mirror.centos.org`）替换为 `mirrors.tuna.tsinghua.edu.cn`.
>
> ```
> sed -e 's|^mirrorlist=|#mirrorlist=|g' \
>          -e 's|^#baseurl=http://mirror.centos.org|baseurl=https://mirrors.tuna.tsinghua.edu.cn|g' \
>          -i.bak \
>          /etc/yum.repos.d/CentOS-*.repo
> ```
>
> 最后更新软件包缓存：
>
> ```
> yum makecache
> ```

## 引用

*  [What is the difference between CentOS "DVD" vs "Everything" ISOs](https://superuser.com/questions/878135/what-is-the-difference-between-centos-dvd-vs-everything-isos)

