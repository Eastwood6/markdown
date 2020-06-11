---
title: hexo grammar
date: 2020-05-15 15:46:01
tags:
  - hexo
keywords:
cover: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/https.jpg
abbrlink:
top_img: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/TB10Vh7SpXXXXbZaFXXXXXXXXXX-2880-1080.jpg
---

[TOC]

## 安装

- git

- nodejs,cnpm:

首先要安装 Node.Js,顺带会有npm

本来是用npm来安装Hexo,但因为国内镜像系统较慢，利用npm安装cnpm也就是淘宝

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

`node -v`验证	`npm -v`验证

- hexo:

安装Hexo:`cnpm install -g hexo-cli`

`hexo -v`验证

## 初始化



- 初始化博客

`mkdir blog`

`cd blog`

`sudo hexo init`

- 启动博客

`hexo s`用来预览

- 创建博客

`hexo n "name"`



## 部署远端(cg:github)

- 安装git部署插件： `cnpm install --save hexo-deployer-git`

- 配置远端地址_config.yml:

`vim _config.yml`

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
- type: git
  repo: https://github.com/Eastwood6/Eastwood6.github.io.git
  branch: master
- type: git
  repo: root@47.110.150.78:/home/git/blog.git
  branch: master
```

- 部署`hexo d`(部署前需要`git clean`清理下)



## 更换主题

- Clone:

`git clone url.git themes/yourName`

- Config:

`vim _config.yml`修改`themes:`为`yourName`