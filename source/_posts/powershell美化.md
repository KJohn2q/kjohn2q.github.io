---
title: powershell美化
tags:
  - powershell
  - windows
  - terminal
  - 命令行
date: 2021-10-02 00:14:04
categories: tool
---


作为一个开发者，在日常开发过程中经常会使用命令行。`windows` 自带的 `cmd` 和 `powershell`  在功能上和界面美观度上总是不能让我满意。本文主要和大家分享如何使用 `windows terminal`  和  `oh my posh` 增强和美化`powershell`。

默认的powershell是这样的：

![image-20211001142221763](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011422866.png)

##  Windows Terminal 的安装

仓库地址: [microsoft/terminal: The new Windows Terminal and the original Windows console host, all in the same place! (github.com)](https://github.com/microsoft/terminal)

推荐使用 `Microsoft Store`  来进行安装.

![image-20211001142641266](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011426386.png)

##  Powerline 的安装

### 安装 `Powerline` 字体

`Powerline` 使用字形来设置提示符样式。 安装 ` [Meslo LGM NF `，包含` Powerline` 字形。 可以从[Nerd Fonts ](https://www.nerdfonts.com/)安装字体。

### 安装 `PowerLine`

使用 `PowerShell` ，安装 `Posh-Git`  和 `Oh-My-Posh`

```
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

> 如果尚未安装 NuGet，可能需要安装它。 如果是这种情况，PowerShell 命令行会询问是否要安装 NuGet。 选择 [Y]“是”。 你可能还需要批准从不受信任的存储库 [PSGallery](https://docs.microsoft.com/zh-cn/powershell/scripting/gallery/getting-started?view=powershell-7) 中安装模块。 选择 [Y]“是”。

![image-20211001144728179](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011447255.png)

[Posh-Git](https://github.com/dahlbyk/posh-git) 将 `Git` 状态信息添加到提示，并为` Git` 命令、参数、远程和分支名称添加  `tab`  自动补全。 [Oh-My-Posh](https://github.com/JanDeDobbeleer/oh-my-posh) 为 ` PowerShell`  提示符提供主题功能。

### 修改配置文件

使用 `notepad $profile` 或所选的文本编辑器打开 `PowerShell` 的配置文件。 该配置文件是一个脚本，会在每次 `PowerShell` 启动时运行。

将以下内容添加到 `PowerShell` 配置文件中：

```
Import-Module posh-git
Import-Module oh-my-posh
Set-PoshPrompt -Theme Paradox
```

重启 `PowerShell` ，可能会出现以下问题

![image-20211001145505754](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011455800.png)

这是由于启动 `PowerShell` 时，执行策略是 `Restricted` （默认）。`Restricted` 执行策略不允许任何脚本运行。

可以通过 `get-executionpolicy` 命令来查看当前的执行策略。

![image-20211001145750648](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011457687.png)

可将执行策略修改为 `RemoteSigned ` 或 `AllSigned `  解决此问题。

![image-20211001152859773](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110011528807.png)

### 修改主题

可以通过 `Get-PoshThemes` 列出当前目录的所有可用主题。

![image-20211001234003580](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110012340706.png)

可以通过 `Set-PoshPrompt -Theme [ThemeName]`  指定主题。

![image-20211001234341724](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202110012343768.png)

## 引用

* [Home | Oh My Posh](https://ohmyposh.dev/)
* [microsoft/terminal: The new Windows Terminal and the original Windows console host, all in the same place! (github.com)](https://github.com/microsoft/terminal)
* [Windows 终端 Powerline 设置 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/terminal/tutorials/powerline-setup)
* [Themes | Oh My Posh](https://ohmyposh.dev/docs/themes#agnoster)

