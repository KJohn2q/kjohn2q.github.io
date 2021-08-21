---
title: vmware 虚拟机联网的三种方式
date: 2020-07-31 18:05:44
tags: [虚拟机, 网络]
---

* 虚拟机联网有三种方式：桥接（bridge）, NAT, 仅主机模式（Host-Only)。联网方式可以在虚拟机设置中进行设置。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731170113.png)

  ## 桥接（bridge）模式

  网络桥接是一种计算机联网设备，可从多个通信网络或网段中创建单个聚合网络。（原文：A network bridge is a computer networking device that creates a single aggregate network from multiple communication networks or network segments. ）。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731170555.png)

  如图所示，主机网卡通过虚拟网桥连接虚拟交换机，各网络模式为桥接的虚拟机连接虚拟交换机 `VMNet0`,各虚拟机  `IP` 均和主机 `IP` 处于同一网段且不能冲突。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210819162442.jpg)

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

  #### 总结

  桥接网络的方式配置简单，但并不适用于ip地址稀缺的情况。

  ## NAT

  网络地址转换（NAT）是一种通过在数据包通过流量路由设备传输时修改数据包IP报头中的网络地址信息，将IP地址空间重新映射到另一个地址的方法。（原文：Network address translation (NAT) is a method of remapping an IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.）

  `vmware` 中新建虚拟机默认网络配置为 `NAT` 模式,虚拟机处于独立的网络，通过 `NAT` 转换器可以访问外网，且能和主机相互通信。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210821174734.jpg)

  如图所示，虚拟的 `VMware Network Adapter VMnet8` 网卡与虚拟交换机 `VMNet8` 相连，`IP` 地址段为 `192.168.9.0/24`，网关默认为 `192.168.9.2`. 具体的 `NAT` 设置可点击NAT设置查看。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210819170322.png)

  #### 网络配置

  首先，先将虚拟机的网络配置修改为`NAT`模式。

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200731174109.png)

  可在 `vmware` 中的虚拟网络编辑器中查看 `NAT` 模式的 `ip` 地址段、网关地址和子网掩码。

  使用 `root` 用户登录虚拟机系统，配置网络信息为刚刚查到的（IP地址，子网掩码，网关地址），添加 `DNS` (114.114.114.114, 114.114.115.115)。

  然后重启网络服务即可访问网络和宿主机。

  #### 总结

  `NAT` 模式适用于 `IP` 地址稀缺的情况。

  ## 仅主机（Host-Only）

  仅主机模式表示虚拟机只能访问宿主机，不能访问网络。整个虚拟机和宿主机工作在一个大的内网下,宿主机可以访问虚拟机，虚拟机不能访问宿主机。如需要连接外网，可以利用宿主机共享网络。此时，处于 `host-only` 网络模式下的虚拟机可以通过宿主机网络访问外网，且可以访问宿主机

  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210819173636.jpg)

  如图所示，宿主机通过虚拟网卡 `VMware Network Adapter VMnet1` 与主机网络进行通信，虚拟网卡的 `IP` 地址需要设置为仅主机模式的网段。默认为主机号为 `.1`
  
  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210821173642.png)
  
  #### 网络配置
  
  可在 `vmware` 中的虚拟网络编辑器中查看 仅主机模式的 `IP` 地址段,在虚拟机中配置IP地址，子网掩码。
  
  重启网络服务，宿主机即可访问该虚拟机。
  
  #### 访问外网
  
  宿主机中联网的网卡，配置网络共享，选中 `host-only` 对应的那块虚拟网卡。
  
  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210812115332.png)
  
  点击确定后，该虚拟网卡的`ip` 地址会改为 `192.168.137.1`,需要改为该虚拟网卡对应的虚拟网络交换机的地址段
  
  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210812115648.png)
  
  如上图所示，地址段位 `192.168,17.0`,于是需要把虚拟网卡的 `ip` 地址改为 `192.168.17.1`
  
  ![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20210812115917.png)
  
  然后，将联网方式为 `host-only` 的虚拟机网关设置为  `192.168.17.l` 即 `VMware Network Adapter VMnet1` 的地址就可以访问外网了，此时也可以访问宿主机。
  
  #### 总结
  
  仅主机模式一般用于公司对机密性要求比较高的网络，个人不常用。
  
  ## 参考链接
  
  * [What is a network bridge?](https://geek-university.com/ccna/what-is-a-network-bridge/)
  * [Bridging (networking)](https://en.wikipedia.org/wiki/Bridging_(networking))
  * [Network address translation](https://en.wikipedia.org/wiki/Network_address_translation)
  * [vmware联网解决方案：host-only共享上网](https://www.cnblogs.com/yihr/p/7348304.html)
  * [VMware的三种网络模式](https://zhuanlan.zhihu.com/p/24758022)
