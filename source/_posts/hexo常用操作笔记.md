---
title: hexo常用操作笔记
toc: false
date: 2024-06-30 18:27:21
categories:
tags:
keywords:
top:
cover:
summary:
password:
mathjax:
---

# 环境搭建

1. 安装nodejs [nodejs官网](https://nodejs.org/zh-cn)
2. 配置国内镜像 [npm使用国内淘宝镜像（最新地址）](https://code-nav.top/article/1004)
3. 全局安转hexo `npm install -g hexo-cli`
4. 安装依赖 `npm install`
5. 安装主题 参考 `.github/deploy.yml` 文件 `prepare build env` 是通过github action 自动将本项目打包通过gitub pages进行部署的命令，将主题克隆到themes目录

# 编写文章

1. 创建文章 `hexo new post 博客标题`
2. 本地预览 `hexo server`

# 发布部署

由于配置了github action 只需要提交代码即可

1. `git pull` 拉取最新代码
2. `git add . && git commit -m ""` 提交代码
3. `git push` 推送到github