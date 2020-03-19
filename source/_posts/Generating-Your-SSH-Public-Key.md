---
title: "Generating Your SSH Public Key"
date: 2020-03-19 10:21:55
tags: ['git', 'ssh', 'keys']
categories: translate
---

> 本文译自[`Git on the Server - Generating Your SSH Public Key`](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key)，仅作学习使用，不用于商业用途

很多 `git` 服务器使用 `SSH` 公钥进行验证。为了提供一个公钥，如果你系统的用户还没有的话，他们必须生成一个。这个过程是跨所有的操作系统的。首先，你应该检查，确保你还没有公钥。默认，用户的 `SSH keys`存储在用户的 `~/.ssh` 目录。如果你已经有一个 `SSH key`，切换到那个目录，列出所有的内容，你可以轻松地看见。

```
$ cd ~/.ssh
$ ls

id_rsa  id_rsa.pub  known_hosts

```

你将会看到一系列名称为 `id_dsa` 或者 `id_rsa`，且有一个后缀名为 `.pub` 的文件。该 `.pub` 文件是你的公钥，其它文件是对应的私钥。如果没有看到这些文件（或者你甚至没有 `.ssh` 目录），你可以通过执行 由 `Linux/macOS` 操作系统和 `windows` 上的 `git` 提供的 `ssh-keygen` 程序来创建它们：

```
$ ssh-keygen -o

```

    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/schacon/.ssh/id_rsa):
    Created directory '/home/schacon/.ssh'.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /home/schacon/.ssh/id_rsa.
    Your public key has been saved in /home/schacon/.ssh/id_rsa.pub.
    The key fingerprint is:
    d0:82:24:8e:d7:f1:bb:9b:33:53:96:93:49:da:9b:e3 schacon@mylaptop.local

首先，你要确认保存密钥的位置（`.ssh/id_rsa`），然后向你询问一个密码短语两次，如果你在使用密钥的时候不想输入密码，你可以留空。然而，如果你使用了密码，确保你使用了 `-o` 选项；它会以比默认格式更能抵御密码强力破解攻击的格式进行存储私钥。你也可以使用 `ssh-agent` 工具，避免每次都需要输入密码。

现在，每个用户都做了以上操作，给你或者任何管理 `Git` 服务器的人发送了公钥。（假定你使用的是需要公钥的 `SSH` 服务器设置）。他们需要做的就是复制 `.pub` 文件的内容并通过邮件发送。公钥文件像这样：

```
$ cat ~/.ssh/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@mylaptop.local

```

获取更多在多操作系统创建 `SSH key` 的深入教程，可以查看 [`GitHub guide on SSH keys `](https://help.github.com/articles/generating-ssh-keys).