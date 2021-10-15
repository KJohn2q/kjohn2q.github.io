---
title: docker部署独立服务
date: 2021-10-15 10:06:37
tags: [docker, 服务，数据库，mysql, rabbitmq, redis]
categories: 笔记
---

> 独立服务指的是没有任何业务依赖，可独立部署，供其它系统调用的服务。如数据库，缓存服务，消息队列等。

## docker 部署 mysql

以 `mysql5.7` 为例

```
docker run -d \
--name dmysql \
-p3306:3306 \
-e MYSQL_ROOT_PASSWORD=secret \
mysql:5.7
```

如使用 `powershell`,则：

```
docker run -d `
--name dmysql `
-p3306:3306 `
-e MYSQL_ROOT_PASSWORD=secret `
mysql:5.7
```

### 参考

* [mysql dockerhub](https://hub.docker.com/_/mysql)

## docker 部署 redis

```
docker run -d \
--name redis-app \
-p6379:6379 \
redis:latest
```

如使用 `powershell`,则：

```
docker run -d `
--name redis-app `
-p6379:6379 `
redis:latest
```

### 参考

* [How to Deploy and Run Redis in Docker](https://phoenixnap.com/kb/docker-redis)
* [redis dockerhub](https://hub.docker.com/_/redis)

## docker 部署 rabbitmq

```
docker run -d \
--rm -it \
--hostname my-rabbit \
-p 15672:15672 \
-p 5672:5672 \
rabbitmq:3-management
```

如使用 `powershell`，则：

```
docker run -d `
--rm -it `
--hostname my-rabbit `
-p 15672:15672 `
-p 5672:5672 `
rabbitmq:3-management
```

端口 `15672` 为 `rabbitmq` 管理站点端口， 端口 `5672` 为客户端连接端口。上述命令执行完成后，我们可以打开地址 `http://localhost:15672` 打开 `rabbitmq` 管理站点，默认的用户名和密码都为 `guest`

### 参考

* [Get Started with RabbitMQ on Docker](https://codeburst.io/get-started-with-rabbitmq-on-docker-4428d7f6e46b)
* [rabbitmq dockerhub](https://hub.docker.com/_/rabbitmq)