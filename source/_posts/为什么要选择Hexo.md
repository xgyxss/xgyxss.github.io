---
title: 为什么要选择Hexo
date: 2022-02-16 16:04:52
tags: [Hexo, 202202]
categories: 博客站务
---

从长期来看，花费大量的时间用来管理一个仅作记录、分享的静态博客，实在是得不偿失！

<!-- more -->

## 为什么要选择Hexo?

1. 初期
   自购服务器、域名，centos8 系统，自搭 LNMP 环境，搭建 Wordpress 博客。写文章是用拖放式的页面构建器——Elementor，只需单击几下即可轻松构建自定义页面。社区也有很多第三方插件用于可视化后台的管理、维护。这时有几个问题不得不考虑了：到后期文章数量比较多时的数据维护？服务器到期换厂家时的数据迁移？...这类问题，想想都觉得相当麻烦。至于该框架的利弊，这里不做讨论。但写作的初衷，只想简简单单地写作，所以只能另寻其他的框架风格。

2. 当下
   动态框架的后台管理实在是不想花太多时间折腾，想更加专注于内容，所以选用了静态框架，然后从众多轻量级静态框架里，选择了 Hexo，至于服务器那块，只需要挂载在 GitHub 上即可。最终选用了「 Hexo + GitHub Pages +自定义域名」搭建个人博客。

3. 核心点
   仅需两条命令，用于博客框架的升级（`npm install -g hexo-cli`）和博客主题的升级（`npm update hexo-theme-melody`）。

4. 后期

   待定...

## lighthouse审查结果

![lighthouse审查结果](https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/lighthouse%E5%AE%A1%E6%9F%A5%E7%BB%93%E6%9E%9C.webp)

这个主题下，就一个 yaml 文件，SEO 这块，我也不知道怎么弄才好...
