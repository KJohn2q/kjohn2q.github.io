---
title: docker cheatsheet
date: 2021-10-15 14:15:54
tags: [docker]
categories: 笔记
---

## docker run

启动一个新的容器 (`container`). 如镜像不存在，会先从 `docker` 托管库中拉取镜像。

用法：`docker run [options] IMAGE`

* `-d, --detach`  容器在后台运行
* `--name string`  指定容器的名称
* `-e --env list`  设置环境变量
* `-p  --publish list`  建立容器到本地的端口映射
* `-i，--interactive`  保持命令行交互状态  
* `-t, --tty`   分配一个伪终端
* `-w, --workdir`  设置容器的工作目录
* `--rm`  如果容器已经存在，自动删除
* `-v, --volume list`  绑定挂载卷

例子： `docker run -d --rm --name dmysql -e MYSQL_ROOT_PASSWORD=secret -v mysql-data:/var/lib/mysql mysql:5,7 ` 该命令会运行一个 `mysql:5.7` 的容器，名称为 `dmysql`，`root` 账户密码为 `secret`, 数据存储在名为 `mysql-data` 的挂载卷中，并将本地端口 `3306` 与容器 `3306` 端口做了映射。

## docker image

管理 `docker` 镜像

用法： `docker image COMMAND`

* `ls`  查看所有镜像
* `build` 依据 `Dockerfile` 创建镜像
* `pull`  从远程仓库拉取镜像
* `push` 推送镜像到远程仓库
* `rm`  删除指定镜像

### docker image ls

列出所有 `docker` 镜像

用法 : `docker image ls [options]`

* `-a`  列出所有镜像，默认会隐藏中间镜像（多阶段构建中会用到）

### docker image build

依据 `Dockerfile` 创建镜像

用法：`docker image build [options]`

* `-f, --file` 指定 `Dockerfile` 路径
* `-t, --tag list` 指定要创建的镜像名称和可选的标签，格式为 `name:tag`

### docker image pull

从远程仓库拉取镜像

用法:  `docker image pull Name[:Tag]`

例子: `docker image pull mysql:latest`

### docker image push

推送仓库到远程仓库

用法：`docker image push Name:[:Tag]`

### docker image rm

删除指定镜像 

用法：`docker image rm [options]` IMAGE

* `-f, --force`  强制删除指定镜像 

## docker container

管理 `docker` 容器

用法: `docker container COMMAND`

* `ls`  列出容器
* `start` 启动停用（`stopped`）的容器
* `rm`  删除容器
* `stop` 停用运行中的容器

## docker ps

列出运行中的容器。

## docker logs

抓取容器的日志。

用法：`docker logs [OPTIONS] CONTAINER`

* `-f, --follow`  追踪日志输出
* `-n, --tail string`  显示末尾第`n`行  

