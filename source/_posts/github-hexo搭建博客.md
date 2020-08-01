---
title: github+hexo搭建博客
date: 2020-08-01 09:32:49
tags: [github, blog, hexo, "博客"]
---

本文介绍使用`hexo + github pages`搭建博客网站。

基础环境：nodejs(version < 14 && version > 12)

## hexo安装与配置

`npm install -g hexo-cli`

## github仓库配置

github中，新建一个 `public` 仓库，命名为 `TestBlog`

## 本地新建博客并连接到 `github` 远程仓库地址

```
hexo init <folder>

cd <folder>

npm install

```

## 配置博客信息

```
title: KJohn2q
subtitle: '一个专注技术的程序员'
description: '涉猎的主要编程语言为 Python、Php、C++、Java，领域涵盖爬虫、后端、架构等。'
keywords: "Python, Php, C++, Java, 爬虫, 架构, 分布式"
author: John Wang
language: zh-CN
timezone: ''

```

## 配置博客部署信息

```
deploy:
  type: git
  repo: git@github.com:KJohn2q/kjohn2q.github.io.git
  branch: master

```

## 本地博客连接到 `github` 远程仓库地址

```
git init

git add .

git commit -m "blog first commit"

git remote add origin git@github.com:KJohn2q/TestBlog.git

git push origin source
```

## 博客网站部署到远程仓库master分支

```
hexo clean

hexo generate

hexo deploy
```

## 配置 `github pages`

![](https://raw.githubusercontent.com/KJohn2q/John-s-figure-bed/master/image/20200801085153.png)

## hexo集成主题

`hexo` 默认主题为 `landscape`，这里集成 `next`

```
cd TestBlog

git clone https://github.com/iissnan/hexo-theme-next themes/next

```

为了便于保存主题文件，把主题文件夹中的 `.git` 文件夹删除。

## 配置评论功能

打开 `theme/next` 主题文件夹中的 `_config.yml`文件，修改以下配置

```
valine:
  enable: true
  appid: t6IFRai4uKVYoIIyrH84awuK-gzGzoHsz
  appkey: uo0ujaAY4BW05YV1NHgA4z0M
  notify: false # Mail notifier
  verify: false # Verification code
  placeholder: Just go go # Comment box placeholder
  avatar: mm # Gravatar style
  guest_info: nick,mail,link # Custom comment header
  pageSize: 10 # Pagination size
  language: # Language, available values: en, zh-cn
  visitor: false # Article reading statistic
  comment_count: true # If false, comment count will only be displayed in post page, not in home page
  recordIP: true # Whether to record the commenter IP
  serverURLs: # When the custom domain name is enabled, fill it in here (it will be detected automatically by default, no need to fill in)
  #post_meta_order: 0
```

## 配置页面浏览量统计

next集成了busuanzi访客统计插件

打开 `theme/next` 主题文件夹中的 `_config.yml`文件，修改以下配置

```
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: fa fa-user
  total_views: true
  total_views_icon: fa fa-eye
  post_views: true
  post_views_icon: fa fa-eye

```

## 配置头像和favicon

打开 `theme/next` 主题文件夹中的 `_config.yml`文件，修改以下配置

```
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.png
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false

```

## 页面底部标签信息`#`换图标

修改文件 `themes/next/layout/_macro/post.swig` ，找到 `rel="tag">#` ，将 `#` 替换为 `<i class="fa fa-tag"></i>` 即可。

## hexo编写页面部署

hexo 相关命令

```
hexo init

hexo new [post] # 新建一篇文章

hexo clean

hexo generate

hexo server

hexo deploy

```
## 语言配置

设置中文/英文

打开根目录的博客配置文件 `/_config.yml`,修改 `language`属性为 `zh-CN`（中文）或者 `en`（英文）

## 链接配置

设置页面路由

打开根目录的博客配置文件 `/_config.yml`,修改 `permalink` 属性为 `:year/:title/`，则最后呈现的路径为 '域名/年份/文章名/',如 `https://kjohn2q.github.io/2020/vmware-%E8%99%9A%E6%8B%9F%E6%9C%BA%E8%81%94%E7%BD%91%E7%9A%84%E4%B8%89%E7%A7%8D%E6%96%B9%E5%BC%8F/`

## 使用github workflows配置自动部署

在根目录新建 `.github/workflows` 文件夹，新建 `deploy.yml` 文件

```
name: Build and Deploy
on: [push]
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
        env: 
          CI: false

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@3.5.7
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: master # The branch the action should deploy to.
          FOLDER: public # The folder the action should deploy.

```

# 参考链接

* [hexo官网](https://hexo.io/zh-cn/docs/)
* [valine官网](https://valine.js.org/quickstart.html)
* [Hexo 博客美化配置](https://ylong.net.cn/hexo_conf.html)