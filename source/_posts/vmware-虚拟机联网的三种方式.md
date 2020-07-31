---
title: vmware 虚拟机联网的三种方式
date: 2020-07-31 18:05:44
tags: [虚拟机, 网络]
---

虚拟机联网有三种方式：桥接（bridge）, NAT, 仅主机模式（Host-Only)。联网方式可以在虚拟机设置中进行设置。

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731170113.png)

## 桥接（bridge）

网络桥接是一种计算机联网设备，可从多个通信网络或网段中创建单个聚合网络。（原文：A network bridge is a computer networking device that creates a single aggregate network from multiple communication networks or network segments. ）。

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731170555.png)

#### 网络配置

首先在虚拟机配置中选择桥接模式。

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731170914.png)

然后进入虚拟机系统，设置虚拟机IP和主机IP处于同一地址段。

我本机的 `IP` 为 `192.168.3.X` 网段。故需要设置虚拟机为 `192.168.3.X`,且不能与当前局域网内的主机 `IP` 地址冲突。

以 `centos7` 为例，使用 `root`账户登录后，`vi /etc/sysconfig/network-scripts/ifcfg-ens33`

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731173257.png)

如图所示进行修改.

然后重启网络服务(`service network restart`)

此时，便可访问外网和宿主机。

### 总结

桥接网络的方式配置简单，但并不适用于ip地址稀缺的情况。

## NAT

网络地址转换（NAT）是一种通过在数据包通过流量路由设备传输时修改数据包IP报头中的网络地址信息，将IP地址空间重新映射到另一个地址的方法。（原文：Network address translation (NAT) is a method of remapping an IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.）

### 网络配置

首先，先将虚拟机的网络配置修改为`NAT`模式。

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731174109.png)

可在 `vmware` 中的虚拟网络编辑器中查看 `NAT` 模式的 `ip` 地址段、网关地址和子网掩码。

使用 `root` 用户登录虚拟机系统，配置网络信息为刚刚查到的（IP地址，子网掩码，网关地址），添加 `DNS` (114.114.114.114, 114.114.115.115)。

然后重启网络服务即可访问网络和宿主机。

### 总结

`NAT` 模式适用于 `IP` 地址稀缺的情况。

## 仅主机（Host-Only）

仅主机模式表示虚拟机只能访问宿主机，不能访问网络。

### 网络配置

可在 `vmware` 中的虚拟网络编辑器中查看 仅主机模式的 `IP` 地址段。配置仅主机模式的默认网卡（通常是`VMnet1`）的网络信息（IP地址，子网掩码，网关和DNS为刚刚查到的信息。IP地址需要自己定）。然后在虚拟机中配置IP地址，子网掩码，网关需要配置为虚拟网卡的IP地址。

然后重启网络服务即可访问宿主机。

### 总结

因仅主机模式并不能访问外网，故这种方式不常用。

## 参考链接

* [What is a network bridge?](https://geek-university.com/ccna/what-is-a-network-bridge/)
* [Bridging (networking)](https://en.wikipedia.org/wiki/Bridging_(networking))
* [Network address translation](https://en.wikipedia.org/wiki/Network_address_translation)