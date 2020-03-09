---
title: Configure CLion on Windows
date: 2020-03-05 08:45:43
tags: ['CLion', 'tool', 'compiler', 'windows']
---

> 该文选译自 `jetbrains` 官网 [`Quick Tutorial: Configure CLion on Windows`](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-windows.htm) 不用于商业用途

在 `windows` 系统,配置 `CLion` 需要安装环境： `Cygwin`、`MinGW`、`WSL`、`MSVC`等。你需要在你的系统上安装环境，分别为每个环境创建 `CLion` 工具链。作为工具链重要的一环，编译环境提供了 `C` 和 `C++` 编译器， `make` 工具， 还有调试器（使用默认工具的情况下）

想查看远程主机工具链的细节，可以访问 [Full Remote Mode](https://www.jetbrains.com/help/clion/remote-projects-support.html#remote-toolchain) 进行查看。

## Cygwin

1. 下载 [Cygwin](https://cygwin.com/install.html) 安装包，2.8 或者更新的版本。
2. 执行安装文件，选择以下的包：
    * `gcc-g++`
    * `make`
    * `gdb`
    你可以在搜索框中键入包的名字，点击列表中该包，直到在该包上有对勾出现。
    ![image](https://resources.jetbrains.com/help/img/idea/2019.3/cl_CygwinSetup.png)
3. 安装完成后，启动 `CLion`，依次打开 `File|Settings|Build,Exceution,Deployment|Toolchains`选择你想要配置的工具链。
4. 在环境列表中选择 `Cygwin`. `Clion`会自动地检测 `Cygwin`的安装情况。检查检测结果，手动指定需要的路径。
5. 等待工具检测完成，点击应用。
   ![](https://resources.jetbrains.com/help/img/idea/2019.3/cl_cygwin_toolchain.png)

## MinGW

1. 下载 [MinGW](http://www.mingw.org/) 或者 [MinGW-W64](http://mingw-w64.org/doku.php)安装包。
2. 运行安装包，在基础安装列表中选择一下的包： `mingw-developer-tool`, `mingw32-base`, `mingw32-gcc-g++`, `mingw32-msys-base`.
   ![](https://resources.jetbrains.com/help/img/idea/2019.3/cl_MinGWInstall.png)
3. 安装成功后，启动 `CLion`，`File|Settings|Build,Exceution,Deployment|Toolchains`选择你想要配置的工具链。
4. 在环境列表中选择 `MinGW`，`Clion`会自动地检测 `Cygwin`的安装情况。检查检测结果，手动指定需要的路径。
5. 等待工具检测完成。如果 `CLion` 不能检测到编译器或者 `make` ，在 `MinGW` 安装管理器中再次检查需要的包是否已安装。工具设置正确后，点击应用。
    ![](https://resources.jetbrains.com/help/img/idea/2019.3/cl_mingw_toolchain.png)

## GDB on Windows

如果使用了 `MinGW` , `CLion` 包含了内置的 `GDB` (8.3版本)。 如果是 `Cygwin`, 你需要在 `Cygwin` 包管理器中安装包 `GDB`，上面已经描述过。

你也可以切换到自己的 `GDB` 二进制包，支持的 `GDB` 版本为 `7.8.X - 8.3.X`

对于 `GDB` 8.0 或者更新的版本，调试器的输出默认会使用 `CLion`的控制台。你可以在 `Help|Find Action` 或者使用快捷键 `Ctrl+Shift+A`, 查找 `Registry` , 设置以下的值 `cidr.debugger.gdb.workaround.windows.forceExternalConsole.`,来使得程序输入/输出会打开额外的windows控制台窗口。