---
title: git自建服务器权限管理
date: 2020-03-19 10:28:19
tags: ['git','服务器',‘Gitolite’]
category: translate
---

> 本文部分译自 [`Gitolite README`](https://github.com/sitaramc/gitolite#gitolite-readme),仅作学习使用，不用于商业用途

## `Gitolite`

`git` 仓库托管 -- `Gitolite` 允许你在一台中心服务器上安装 `git` 托管，具有很多细粒度的访问控制和更强有力的特性。

## 安装

首先，准备 `ssh` key

* 使用 `git` 用户登录服务器
* 确保 `~/.ssh/authorized_keys` 为空或不存在
* 确保你工作区的 `ssh` 公钥复制到了 `$HOME/YourName.pub`

下一步，通过执行下面的命令来安装 `gitolite`

```
git clone https://github.com/sitaramc/gitolite
mkdir -p $HOME/bin
gitolite/install -to $HOME/bin
```

最后，作为管理员安装 `gitolite`

```
gitolite setup -pk YourName.pub
```

如果最后的命令不能执行，也许是 `$HOME/bin` 没有添加到你的环境变量 `PATH` 中，你也可以添加它，或者直接执行：

`$HOME/bin/gitolite setup -pk YourName.pub`

如果出现其他错误，请查阅[官方文档](https://gitolite.com/gitolite/)

## 添加用户和仓库

不要手动地在服务器上添加新的仓库或者用户。 通过推送对指定仓库 " `gitolite-admin` " 的修改，并推送至服务器，能够维护 `Gitolite` 用户，仓库和访问规则。

开始在你的工作区做以下操作，你可以管理 `gitolite`的安装（如果你还没有安装的话）

```
git clone git@host:gitolite-admin
```

> 注意：如果提示输入密码的话，配置有误。可以查看[完整版文档](https://gitolite.com/gitolite/)。

现在，如果你执行 `cd gitolite-admin`, 你将看到两个子目录 `conf` 和 `keydir`

添加新用户 `alice`, `bob`, `carol` 以及他们的公钥，将它们复制到 `keydir` 文件夹， 并分别重命名为 `alice.pub`, `bob.pub`, `carol.pub`.

添加一个新仓库 `foo`，给这些用户设置不同的访问级别，通过编辑 `conf/gitolite.conf`，添加类似下面这些行：

```
repo foo
    RW+      =  alice
    RW       =  bob
    R        =  carol

```

一旦做了这些修改，执行下面的命令

```
git add conf
git add keydir
git commit -m "added foo, give access to alice, bob, carol"
git push
```

一旦推送完成，`gitolite` 将会在服务器的 `~/.ssg/authorized_keys`，同时创建一个新的、空的叫做 `foo` 的仓库

## 对你的用户提供帮助

一旦一个用户向你发送了他们的公钥，你执行了上面的指定操作，设置了访问级别，你就告诉了他们仓库的地址。通常是 `git clone git@host:reponame`;通过 `man git-clone`，查看其它的操作

注意：再次强调，如果提示输入密码，那一定是哪里出错了

如果他们需要知道他们可以访问哪些仓库，他们只需要执行 `ssh git@host info`.

## 访问规则例子

`Gitolite`的例子是非常强大。以上为最简单的使用。下面展示稍微详细一点的例子：

```
repo foo
    RW+                   =   alice
    -  master             =   bob
    -  refs/tags/v[0-9]   =   bob
    RW                    =   bob
    RW refs/tags/v[0-9]   =   carol
    R                     =   dave

```

例子中的规则表示：

* `alice` 可以在所有分支或者标签做所有事情 -- 创建，推送，删除，回退/覆盖 等等。
* `bob` 可以创建或者快速推送名字不以 `master` 开头的分支，且可以创建名字不以 "`v`+数字" 开头的的标签
* `carol` 可以创建名字以 " `v` + 数字"开头的标签
* `dave` 可以 `clone/fetch`

请查看以上链接的主文档查看所有细节，也有更多的特性和例子

## 分组

`Gitolite` 可以方便的对用户或者仓库进行分组。以下为创建两个用户组的例子：

```
@staff     =  alice bob carol
@interns   =  ashok

repo secret
    RW     =  @staff

repo  foss
    RW+    =  @staff
    RW     =  @interns

```

积累分组列表。一下两行和以上之前对 `@staff` 的定义。

```
@staff    =   alice bob
@staff    =   carol

```

你可以在其他分组名字中使用分组名字。

```
@all-devs  =  @staff @interns
```

最后， `@all` 是一个特殊的名字，常用来表达 `all repos` 或者 `all users`.

## 命令

用户可以远程执行命令，使用 `ssh`, 执行

```
ssh git@host help
```

打印可用命令的列表

最常使用的命令为 `info`。 所有的命令适宜的信息响应，使用一个简单的参数 `-h`

如果你有服务器上的 `shell`, 你有很多可用的命令。尝试执行 "gitolite help" 来查看。