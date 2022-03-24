---
title: Hexo崩溃重装
date: 2022-03-01 05:20:00
tags: [Hexo,报错处理]
categories: 解决方案
---

记录一次博客被玩坏的经历！同时也学到了：

- 原始文件（不仅仅是渲染生成的文件）以及配置文件的备份的重要性！

- 形如<a href="#target1">`WARN No layout index.html`</a>报错的正确处理！

<!-- more -->

事情是这样的：<a href="#target">操作部分从这里开始看</a>

本来博客已经搭建完毕了，零零碎碎的基本功能也已经基本实现，但是在尝试使用`PWA功能`的时候，整个博客崩溃了，网上的帖子也看了几十上百篇，但仍然挽救不了，于是打算重装。

鉴于本地文件已经被玩坏了，各种报错，遂将GitHub上的内容给拷贝下来，才发现事情没有那么简单，配置文件那些全部都没有！！！才明白这个博客框架只是将一部分生成页面的文件发布到了GitHub，于是从废纸篓取出刚刚删除的配置文件。

<a name="target">操作部分：</a>

> 重装不是完完全全地重装，后续是找回垃圾篓里的配置文件操作的。
>
> 可能每个人写笔记的方式不一样，为了方便易懂：
>
> 注释即为操作的步骤，文档类型即为操作的位置或者修改文件的位置，例bash类型即为在命令行里的操作，markdown类型即为在某个文件里修改内容或其他操作。

```bash
# 初始化hexo博客目录
hexo init blog
# 查看hexo的版本
hexo -v
# 进入目录
cd blog
# 安装npm包
npm install
# 生成一片文章
hexo n '第一篇hexo文章'
# 生成静态文件
hexo g
# 启动服务，本地预览
hexo s
# hexo会根据source/_post中的文章生成网页，网页会放在public文件夹下。此时博客已部署，可以使用hexo的服务器模块生成一个测试网站。hexo 3.0之后，这个服务器模块已经独立出来
npm install hexo-server --save
# 清理
hexo clean
# 安装hexo的git部署器插件
npm install --save hexo-deployer-git
```

```markdown
# 修改配置文件_config.yml
type: git
repo: git@github.com:xgyxss/xgyxss.github.io.git
branch: main
```

```bash
# 推送到GitHub上
hexo d --message 'Blog Optimization'
```

```markdown
# 在hexo目录下，新建一个CNAME文件，该文件没有后缀名，内容即为GitHub Pages中的Custom domain，即为：yexingshusheng.com
yexingshusheng.com
```

```markdown
# 修改 _config.yml 文件
url: https://yexingshusheng.com
```

```markdown
# 在仓库xxx.github.io -> Settings -> Pages中将Custom domain改为：yexingshusheng.com，待其check完毕后，即可在网址中直接通过自定义域名yexingshusheng.com访问。
```

```bash
# 安装melody主题（Hexo版本 ≥5.0）
npm install hexo-theme-melody
# 修改主题，将theme里的landscape改为melody
vim _config.yml
```

```markdown
melody
```

```bash
# 安装pug 以及 stylus 的渲染器
npm install hexo-renderer-pug hexo-renderer-stylus --save
# 在hexo的工作目录下创建一个文件：_config.melody.yml
touch _config.melody.yml
# 将 ./node_modules/hexo-theme-melody/_config.yml 里的内容拷贝至 _config.melody.yml
cp ./node_modules/hexo-theme-melody/_config.yml _config.melody.yml
# 升级改主题
npm update hexo-theme-melody
# 生成标签页
hexo new page tags
# 修改生成的index.md文件（作者用的是iterm，直接可以用Command+左键进入该文件）
```

```markdown
---
title: 标签
date: 2021-12-15 05:20:00
type: "tags"
---
```

```bash
# 生成一下，看报不报错，之前的版本，在冒号后面需要加一个空格，否则报错
hexo clean;hexo g;hexo s;
```

```bash
#然后再依次生成分类页，修改
hexo new page categories
```

```markdown
---
title: 分类
date: 2021-12-15 05:20:00
type: "categories"
---
```

```bash
# 生成slide页面，修改
hexo new page slides
```

```markdown
---
title: Slides
date: 2021-12-15 05:20:00
type: "slides"
---
```

```bash
# 创建相册，修改
hexo new page gallery
```

```markdown
---
title: Gallery
date: 2021-12-15 05:20:00
type: "gallery"
---
```

```bash
# 创建404页面，修改
hexo new page 404
```

```markdown
---
title: 404
date: 2021-12-15 05:20:00
layout: 404
permalink: /404
---
```

```bash
# 创建运营历史页面，修改
hexo new page history
```

```markdown
---
title: 运营历史
date: 2021-12-15 05:20:00
type: "history"
---
```

```bash
# 生成关于作者页面，修改
hexo new page about
```

```markdown
---
title: 关于作者
date: 2021-12-15 05:20:00
type: "about"
---
```

```markdown
# 修改_config.melody.yml文件
theme_color:
  enable: true
  main: "#49B1F5"
  paginator: "#00C4B6"
  button_hover: "#FF7242"
  text_selection: "#00C4B6"
  link_color: "#858585"
  hr_color: "#A4D8FA"
  tag_start_color: "#A4D8FA"
  tag_end_color: "#1B9EF3"
  header_text_color: "#EEEEEE"
  footer_text_color: "#EEEEEE"

menu:
  Home: /
  Archives: /archives
  Tags: /tags
  Categories: /categories
  History: /history
  About: /about
```

至此，只需要根据官网完善后续步骤即可。

毕竟不是第一次安装了，后续就直接将垃圾篓里的文件package.json、\_config.yml、\_config.melody.yml、source目录找回，安装package.json里对应的插件，然后将\_config.yml、\_config.melody.yml这两个配置文件里的部分内容更改即可。

配置完之后本应该没问题了，又另外出了一点bug。

<a name="target1">报错大致如下：</a>

```bash
WARN No layout 404.html
WARN No layout categories/index.html
WARN No layout tags/index.html
WARN No layout comments/index.html
WARN No layout about/index.html
WARN No layout history/index.html
WARN No layout index.html
...
```

排查：

1. 插件

   ```bash
   # 检查是否报错
   npm ls --depth 0
   ```

2. 主题

   检查配置文件是否更改成当前安装的主题。

3. markdown文件

网上的资料千篇一律的是插件的丢失，**本博客最终查出是对应的markdown文件的空格问题**。

拿 404.md 文件为例：

```markdown
title: 404
date: 2021-12-15 16:08:14
layout: 404
permalink: /404
comments: false
```

当时写的是：

```markdown
title:404
date:2021-12-15 16:08:14
layout:404
permalink:/404
comments:false
```

对比可以看出，该问题是由于**缺少空格**，导致文件渲染出了问题，进而导致整个博客页面渲染空白。

解决：依次将报错的文件的对应位置添加空格，即可成功渲染。

