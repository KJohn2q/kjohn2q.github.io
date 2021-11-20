---
title: 打造windows下易用终端
tags:
  - windows
  - terminal
  - 终端， 命令行
categories:
  - tool
date: 2021-11-05 23:25:49
---


`windows` 下的命令行工具一直被人诟病：老旧，功能弱，界面。我一直在寻找 `windows` 下比较好用的终端工具，尝试使用过 `cmder`， `cygwin`等，都因各种各样的原因放弃了。直到微软推出了新的终端工具：`Windows Terminal`。 `Windows Terminal` 是一款界面美观，现代化易用的终端工具。我将会基于此构建功能丰富、易用的终端。

## Windows Terminal 的安装

`windows terminal` 是一款微软开源的免费、好用的终端工具。可以集成多种 `shell`，如 `powershell`,`cmd`, `git` 等。可通过 `Microsoft Store` 或 `winget`工具来进行安装。

![image-20211112083938310](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111120839432.png)

```
winget install --id=Microsoft.WindowsTerminal -e
```

## powershell core的安装

## 安装 powershell-core

`powershell core` 与 `windows powershell` 不同，是一款开源、跨平台的命令行 `shell`。可以通过 `Microsoft Store` 或 `winget`工具来进行安装。

![image-20211105234447288](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111052344351.png)

```
winget install Microsoft.PowerShell
```

![image-20211105234717887](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111052347936.png)

安装完成后，重新启动 `windows terminal`，可以看到 新的`powershell`。

![image-20211105234953712](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111052349773.png)

### 将powershell-core设置为默认启动终端

打开 `windows terminal` 设置，将默认配置文件改为 `PowerShell` ，重启 `windows terminal`

![image-20211105235409289](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111052354342.png)

## 修改主题

[Oh-My-Posh](https://ohmyposh.dev/)是一款用于 `shell` 的提示主题引擎。 

### 安装 Oh-My-Posh

```
winget install JanDeDobbeleer.OhMyPosh
```

安装完成后，重启 `windows terminal`,执行 `oh-my-posh`进行测试

![image-20211106000238888](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060002931.png)

命令成功执行，不过显示有点问题，需要修改下字体。

###  更新字体

下载 [Caskaydia Cove Nerd Font Complete](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/CascadiaCode.zip?WT.mc_id=-blog-scottha)，解压后进行安装。

打开 `PowerShell` 外观设置 ，修改字体为 `CaskaydiaCove Nerd Font`, 重新启动 `windows terminal`

![image-20211106000911797](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060009860.png)

重新测试 `oh-my-posh`，可以看到显示正常

![image-20211106001121625](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060011665.png)

### 配置 `oh-my-posh`

打开配置文件

```
notepad $PROFILE
```

如提示找不到指定的路径，可检查配置文件的路径

```
echo $PROFILE
```

![image-20211106001639782](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060016827.png)

在指定目录，新建配置文件

```
mkdir C:\Users\John\Documents\PowerShell\
New-Item -Path 'C:\Users\John\Documents\PowerShell\Microsoft.PowerShell_profile.ps1' -ItemType File
```

下载 `shanselman` 修改好的配置文件，复制至自定义目录，我这边放置到了 `OneDrive`中

![image-20211106002606638](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060026675.png)

重新打开配置文件,添加以下内容

```
oh-my-posh --init --shell pwsh --config D:/OneDrive/OhMyPosh/ohmyposhv3-2.json | Invoke-Expression
```

刷新配置文件

```
. $PROFILE
```

![image-20211106002858874](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060028912.png)

## 启用终端图标

命令行环境下 ，执行

```
Install-Module -Name Terminal-Icons -Repository PSGallery
```

![image-20211106003341545](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060033585.png)

将以下内容添加至配置文件中

```
Import-Module -Name Terminal-Icons
```

刷新配置文件

```
. $PROFILE
```

![image-20211106003510634](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060035676.png)

## git 自动补全

安装 [Posh-Git](https://github.com/dahlbyk/posh-git)

```
Install-Module Posh-Git
```

将以下内容添加至配置文件中

```
Import-Module Posh-Git
```

![](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060931112.gif)

##  基于历史建议与 tab 自动补全

`PSReadLine` 能基于命令历史记录来提示输入，首先进行安装

```
Install-Module PSReadLine
```

将以下内容添加至配置文件中

```
# 导入PSReadLine
Import-Module PSReadLine
# 基于历史提示
Set-PSReadLineOption -PredictionSource History
Set-PSReadLineOption -PredictionViewStyle ListView
Set-PSReadLineOption -EditMode Windows
# tab键自动补全
Set-PSReadLineKeyHandler -Key Tab -Function Complete
```

![tab自动补全与历史命令提示](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202111060939879.gif)

## 引用

* [My Ultimate PowerShell prompt with Oh My Posh and the Windows Terminal](https://www.hanselman.com/blog/my-ultimate-powershell-prompt-with-oh-my-posh-and-the-windows-terminal)
* [Announcing PSReadLine 2.1+ with Predictive IntelliSense](https://devblogs.microsoft.com/powershell/announcing-psreadline-2-1-with-predictive-intellisense/?WT.mc_id=-blog-scottha)
* [A1.6 Appendix A: Git in Other Environments - Git in Powershell](https://git-scm.com/book/ms/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Powershell)

