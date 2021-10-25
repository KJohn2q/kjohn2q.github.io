---
title: docker cheatsheet
tags:
  - docker
categories: 笔记
date: 2021-10-15 14:15:54
---

#  docker

* `docker -v, --version`    查看 `docker` 版本

## docker run

启动一个新的容器 (`container`). 如镜像不存在，会先从 `docker` 托管库中拉取镜像。

用法：`docker run [OPTIONS] IMAGE`

**OPTIONS**

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

**COMMAND**

* `ls`  查看所有镜像
* `build` 依据 `Dockerfile` 创建镜像, 详见 [docker build](#docker-build)
* `pull`  从远程仓库拉取镜像,详见 [docker pull](#docker-pull)
* `push` 推送镜像到远程仓库,详见 [docker push](#docker-push)
* `rm`  删除指定镜像,同 [docker rmi](#docker-rmi)

### docker image ls

列出所有 `docker` 镜像

用法 : `docker image ls [OPTIONS]`

**OPTIONS**

* `-a`  列出所有镜像，默认会隐藏中间镜像（多阶段构建中会用到）

## docker push

推送镜像到远程仓库

用法：`docker push [OPTIONS] NAME[:TAG]`

**OPTIONS**

* `-a, --all-tags`  推送所有标签的镜像到远程仓库
* `--disable-content-trust` 跳过镜像验证( 默认为 `true` )
* `-q, --quiet`  隐藏详细输出

## docker pull

从远程仓库拉取镜像或镜像仓库

用法： `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`

**OPTIONS**

* `-a, --all-tags`  从远程仓库拉取所有标签的镜像
* `--disable-content-trust` 跳过镜像验证( 默认为 `true` )
* `--platform string`   设置平台，如果服务器有多平台能力的话
* `-q, --quiet`  隐藏详细输出

## docker rm

删除一个或多个容器

用法： `docker rm [OPTIONS] CONTAINER [CONTAINER ...]`

**OPTIONS**

* `-f, --force`  强制删除运行中的镜像（使用 `SIGKILL`)
* `-l, --link` 删除指定的链接
* `-v, --volumes`  删除容器关联的匿名卷 

## docker rmi

删除一个或多个镜像

用法： `docker rmi [OPTIONS] IMAGE [IMAGE ...]`

**OPTIONS**

* `-f, --force` 强制删除镜像

## docker container

管理 `docker` 容器

用法: `docker container COMMAND`

**COMMAND**

* `ls`  列出容器
* `start` 启动停用（`stopped`）的容器
* `rm`  删除容器
* `stop` 停用运行中的容器
* `exec` 在运行中的容器中运行命令,详见 [docker exec](#docker-exec)

## docker ps

列出运行中的容器。

## docker logs

抓取容器的日志。

用法：`docker logs [OPTIONS] CONTAINER`

**OPTIONS**

* `-f, --follow`  追踪日志输出
* `-n, --tail string`  显示末尾第`n`行  

## docker network

管理 `docker` 网络

用法： `docker network COMMAND`

**COMMAND**

* `create`  创建网络
* `ls`  列出网络
* `prune`  删除所有无用的网络
* `rm`  删除网络
* `insecet` 查看网络详细信息，详见 [docker network inspect](#docker-network-inspect)

### docker network inspect

查看网络详细信息

用法： `docker network inspect [OPTIONS] NETWORK [NETWORK ...]`

**OPTIONS**

* `-f, --format string`  使用给定模板格式化信息输出
* `-v, --verbose`  用于诊断的详细输出 

## docker volume

管理 `docker` 卷

用法：`docker volumn COMMAND`

**COMMAND**

* `create` 创建卷
* `ls` 列出卷
* `prune` 删除所有无用的卷
* `rm` 删除卷

## docker build

依据 `Dockerfile` 构建 `docker` 镜像，同 `docker image build`

用法：`docker image build [OPTIONS]`

**OPTIONS**

* `-f, --file` 指定 `Dockerfile` 路径
* `-t, --tag list` 指定要创建的镜像名称和可选的标签，格式为 `name:tag`

## docker exec

在运行中的容器中执行命令，同 `docker container exec`

用法：`docker exec [OPTIONS] CONTAINER COMMAND [ARG ...]`

**COMMAND**

* `-d, --detach`  在后台执行命令
* `-e, --env list`   设置环境变量
* `-i, --interactive` 保持命令行输入状态
* `-t, --tty`   分配伪终端
* `-w, --workdir string`  指定容器内的工作目录

## docker tag

为指定镜像创建新的标签（不会创建新的镜像，而是引用之前的镜像）

用法：`docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

例子： `docker tag java-docker:latest  java-docker:1.0` 

# 引用

* [docker reference](https://docs.docker.com/reference/)

