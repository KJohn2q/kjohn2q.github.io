---
title: github-actions详解
tags:
  - github
  - github-actions
categories:
  - 笔记
date: 2021-10-18 11:57:28
---


## github actions 例子

通过使用 `github-actions`, 可以在自己的仓库中自动化地执行软件开发工作流。以我的博客工作流举例，当提交代码到远程仓库的 `source` 分支时，安装所有依赖，并将生成的静态页面文件部署到 `master` 分支上，具体的配置如下

```
name: Build and Deploy
on: 
  push:
    branches: 
      - source
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2.3.1 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false

      - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
        run: |
          npm install
          npm run build

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@4.1.5
        with:
          BRANCH: master # The branch the action should deploy to.
          FOLDER: public # The folder the action should deploy.
```

## github actions 语法解释

该 `workflow` 文件位于  `./github/workflows` 中

* `name`,  `workflow` 的名称
* `on` ，触发事件，如：`push`, `pull_request`。 
* `jobs` ,  一系列在相同运行环境中执行的步骤
* `build-and-deploy`， 在 `jobs`下定义的一个 `job` 的名称
* `runs-on`,  定义 `job` 的运行时环境
* `steps`,    定义一组执行步骤
* `name:Checkout`   执行步骤的名称
* `uses:actions/checkout@v2.3.1`  该执行步骤使用社区提供的 `action`, 名称为 `checkout`，`v2.3.1` 为该 `action` 的标签，详情参见 [checkout in github actions marketplace](https://github.com/marketplace/actions/checkout)
* `with` 定义 `action` 使用的变量
* `run` 定义 `job` 需要执行的命令

## 引用链接

* [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions)