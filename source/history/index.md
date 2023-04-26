---
title: 运营历史
date: 2022-02-16 05:20:00
type: "history"
comments: false
---

### 2022-09-10

本想配置 [站点地图](https://search.google.com/search-console/sitemaps?resource_id=https%3A%2F%2Fyexingshusheng.com%2F) ，结果验证失败。

查看 Google 收录情况，已全部收录。

GA 仍然没有数据，排查：

- 浏览器下的 Network 的状态码 200，可以找到 analytics.js。
- 根据 [这篇文章](https://ahrefs.com/blog/zh/how-to-use-google-analytics/) 知，可能是 GA 的没有设置好，通过 [Tag Assistant Chrome 扩展程序](https://support.google.com/tagassistant/answer/2947093?hl=en) 检测，果然是设置的问题。

原因：[验证网站所有权](https://support.google.com/webmasters/answer/9008080#html_verification&zippy=%2Chtml-%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0:~:text=%E5%A4%87%E6%B3%A8-,HTML%20%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0,%E7%9A%84%E7%89%B9%E5%AE%9A%E7%BD%91%E5%9D%80%E3%80%82%E5%9C%A8%E7%BD%91%E7%AB%99%E6%89%98%E7%AE%A1%E5%B9%B3%E5%8F%B0%E4%B8%8A%E5%8F%AF%E8%83%BD%E6%97%A0%E6%B3%95%E4%BD%BF%E7%94%A8%E3%80%82,-HTML%20%E6%A0%87%E8%AE%B0) 一文中有说明：

>  相对简单，但您需要能够上传文件，并将其发布到您网站上的特定网址。在[网站托管平台](https://support.google.com/webmasters/answer/9008080#cms)上可能无法使用。

值得一试的方法：将验证方法由 HTML 文件上传改为 Google Analytics（分析）跟踪代码，不是修改博客框架里配置文件的 google_analytics，而是将完整的 gtag.js 代码复制到网站的`<head>`部分。因为并非所有平台都为 GA4 中的新“G-” ID 提供支持。

GA4 支持的平台：[Which platforms accept a "G-" ID?](https://support.google.com/analytics/answer/10447272?hl=en=#:~:text=Which%20platforms%20accept%20a%20%22G%2D%22%20ID%3F) 

总结：要想使用 GA4，在博客或应用（官网说 GA4 已开始支持应用）中加入完整的 gtag.js 代码即可。

### 2022-06-05

本来想配置`Google Search Console `的站点地图，结果卡在了验证网站所有权这步，连后台都进不去了。可能是之前删掉了验证所有权的文件，因为当时没起作用，实质上，是过了一段时间才被验证成功。因为当时可以进入后台。

在永久链接中重新添加日期。最初在博客优化的过程中，将永久链接改为了中文拼音。无意中发现[一篇文章](https://talk.jekyllrb.com/t/why-do-permalinks-have-year-month-day-in-them/6044/2)，里面提到几个月或者几年内的重复文章问题，通过包含date使URL独一无二，为避免问题，遂又重新添加日期。

`Algolia`的问题彻底清除的两种方法：
1.在`Algolia`后台的`Manage index`处直接`Clear`，然后按照提示输入`CLEAR`即可。
2.在生成时，添加可选参数，`Hexo algolia --flush`即可。（推荐）

> rf.
>
> https://github.com/thom4parisot/hexo-algolia
>
> 文中有关于`algolia`的options用法。

### 2022-06-02

2022-02-28折腾`PWA`导致博客被玩坏的原因找到了，有插件但并不适配，只支持到Hexo 4.2.0之前的版本，只能通过[非插件的方法](https://senorui.top/posts/bce7.html)让Hexo博客支持`PWA`。

###  2022-05-07

经观察，写完文章再更改文章名或者更改permalink之后，会生成重复名称的记录，`Algolia`的搜索结果需要在后台手动删除冗余的数据。

### 2022-05-06

域名短信被警告未使用x里云内地节点服务器。但是在2022-03-22时，已经解析过一条x里云内地节点服务器的域名记录。售后工程师今天告知是本域名（`yexingshusheng.com`）没有指向x里云大陆节点服务器上或者没有访问量，对，没有听错，需要将解析到x里云的那条记录，刷访问量（不是本网站，而是其中的一条子域名`gb.yexingshusheng.com`）。至于x里云官方系统没有捕捉到数据的原因可能是：该服务器已经解析了一条顶级域名和几条子域名，并将其余的强制跳转了（包括这条子域名`gb.yexingshusheng.com`）。

### 2022-04-22

近一个月没看，`Google Search Console`中的有效网页只有一个，站点已被Google收录，查询方法参照2022-03-06历史；

在`Google Search Console`的设置中关联`Google Analytics`；

`npm`添加站点地图；

添加`robots.txt`文件（用来一种存放于网站根目录下的 ASCII 编码的文本文件，它通常告诉网络搜索引擎的漫游器【又称网络蜘蛛】）；

在`Google Search Console `中添加站点地图 `/sitemap.xml`，状态目前是`无法获取`。

### 2022-03-28

添加功能`Google Search Console `，数据和效果过段时间再查看，[站点地图](https://search.google.com/search-console/sitemaps?resource_id=https%3A%2F%2Fyexingshusheng.com%2F)暂待配置。

### 2022-03-23

`Algolia`搜索结果多余，已删除冗余文章名。

### 2022-03-22

x里云节点信息核查。备案号链接地址错误，正确地址如下：https://beian.miit.gov.cn

### 2022-03-10

添加页面`留言板`。

### 2022-03-06

添加功能`百度统计`，网站被百度收录，网页查看：`site:yexingshusheng.com`。

将网址的中文链接转成英文链接（确切来说是转拼音）；

当前主题下的导航栏图标添加无效。

### 2022-03-03

根据 [这篇文章](http://www.yanbaolong.com/post/3728.html) 知，关联Google Ads，仍无数据；

### 2022-03-02

`local search`配置未生效；

`GA`不显示数据。

### 2022-02-28

尝试添加`PWA`（Progressive Web App）功能，博客被玩坏了，重新安装，重装时遇到各种报错！

> 该博客框架只提交生成的部分，所以需要做好备份，于是，重新添加一个私密仓库，用来保存该博客下所有的文件！

### 2022-02-27

添加功能`点击烟花效果`，`代码高亮优化`，`RSS订阅`（只需将 https://yexingshusheng.com/atom.xml 添加到RSS阅读器即可）；

去除功能`看板娘`，提升阅读体验。

### 2022-02-26

添加功能`Google Analytics（简称GA）`，`看板娘`，`插入网易云音乐`；

> 当前使用的是GA4。

### 2022-02-25

添加功能`搜索`。

### 2022-02-20

添加功能`分享`。

### 2022-02-19

添加页面`运营历史`、`关于作者`；

添加功能`字数统计`、`置顶帖`、`评论`、`评论里的头像完善`；

完善区域`ICP`。

### 2022-02-17

更换主题`melody`、`背景图`；

完善区域`GitHub图标链接`、`侧边栏头像`、`Follow Me`、`友链`、`站点建立时间`、`支付宝打赏`、`微信打赏`。

###  2022-02-16

博客创建！！！

### 小功能待添加和优化

~~`PWA`功能需要一些 icon 图标，或者通过[Web App Manifest](https://app-manifest.firebaseapp.com/)生成，暂无合适的 icon 图标。~~

~~`站点小图标`暂未找到合适的图标。~~

~~`网站运行时间`该主题下无其他主题的ejs文件，不方便修改，不想花大量时间折腾。~~

`评论自定义表情`评论表情改成自定义的，比如bilibili的。
