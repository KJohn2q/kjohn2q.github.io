---
title: how-to-install-ubuntu-server20.04LTS
date: 2021-06-23 11:08:50
tags: [linux, ubuntu]
categories: [笔记]
---

本文档演示如何安装`ubuntu server 20.04 LTS`

## 安装

[ubuntu server 20.04LTS 镜像下载](https://ubuntu.com/download/server)

可根据 [install-ubuntu-server](https://ubuntu.com/tutorials/install-ubuntu-server#3-boot-from-install-media) 一步一步进行安装。

其中有两个部分需要注意：

1. `proxy-url`: `http://host-address:proxy-port`
2. `software-source`:  `http://mirrors.aliyun.com/ubuntu/`

## 相关的信息查看命令

#### 网络配置查看

* `ip -a` 查看ip地址
* `ifconfig` 查看ip地址信息(需要安装`net-tools`)

## 优化

####  修改 `root` 账户密码

`ubuntu server` 安装时需要提供一个用户名和密码（非`root`）如需要`root` 账户，则首先需要修改 `root` 账户的密码

`sudo passwd root`  输入密码，并且再次输入，即可修改成功

#### 关闭防火墙

* `sudo ufw status`  查看防火墙状态
* `sudo ufw enable`  启动防火墙
* `sudo uft disable`  关闭防火墙

#### 启用`ssh-server`

`ubuntu server` 默认是不提供`sshd` 服务的，如需要通过`xshell`或`secureCRT`等工具进行连接，则需要安装`openssh-sever`

```
sudo apt update
sudo apt upgrade

sudo apt install openssh-server
```

可以通过 `sudo systemctl status ssh` 查看`ssh.server`的启动状态

如`ssh.service`未启动，则可以运行以下命令：

```
sudo systemctl enable ssh
sudo systemctl start ssh
```

#### 网络配置

`ubuntu 20.04`使用`netplan`作为默认的网络管理器。配置文件目录为 `/etc/netplan`

`00-installer-config.yaml`

```
network:
version: 2
renderer: NetworkManager
ethernets:
 ens33:
  dhcp4: no
  addresses:
  - 192.168.72.140/24
  gateway4: 192.168.72.2
  nameservers:
   addresses: [8.8.8.8, 8.8.4.4]

```

**`netplan`相关命令**

* `netplan try` 验证`netplan`配置
* `netplan apply` 应用新的配置

## 参考链接

* [Ubuntu Linux install OpenSSH server](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)
* [Ubuntu 20.04 Network Configuration](https://linuxhint.com/ubuntu_20-04_network_configuration/)
* [Network Configuration](https://ubuntu.com/server/docs/network-configuration)