---
title: kex_exchange_identification 连接被远程主机关闭
date: 2022-03-24 17:43:09
tags: [git, 报错处理, 202203]
categories: 博客站务
---

错误出现的背景：在进行 git 分支进行多终端工作部署中出现。

<!-- more -->

### git 分支多终端操作的起源

当现在在自己的笔记本上写的博客，部署在了网站上，那么在另外一台电脑上（自己家的台式机、或者要换电脑了），没有博客的文件，这个时候该怎么办呢？

在这里就需要利用 git 的分支系统进行多端操作了，这样每次打开不一样的电脑，只需要简单配置，把文件同步下来，就可以无缝衔接写博了。

### git 的机制

上一次博客被玩崩溃，才知道了这个博客框架的机制：由于命令`hexo d`上传部署到 GitHub 的其实是 hexo 编译后的文件，是用来生成网页的，也就是目录`.delopy_git`里面的文件。但是，其他的文件、配置文件、主题文件都没有上传到 GitHub。

### 又玩坏的过程

首先创建了一个 master 分支，然后把除了`.git`之外的所有文件都删掉了，然后将本地的hexo博客源目录除了`.deploy_git`文件全部复制过来，别忘了该目录(ssh 连接目录)下的隐藏文件，包括`.gitignore`文件，博主本人将`.github`目录也复制了，主题中没有`.git`文件，所以也不用担心上传的时候会出现报错，因为`.git`文件不能嵌套上传。

> 这里`.gitignore`文件里的内容如下：
>
> ```markdown
> .DS_Store
> Thumbs.db
> db.json
> *.log
> node_modules/
> public/
> .deploy*/
> ```

然后在 ssh 连接目录中，由于是同一台电脑，就不需要初始化操作：

> 安装 git（设置git全局邮箱和用户名、设置 ssh key）、安装 nodejs、安装 hexo。

直接在任意目录 X 下，将项目拉取下来，`git clone git@xxx`，然后进入该目录 X，先建立连接`npm install`、`npm install hexo-deployer-git --save`，然后生成`hexo clean;hexo s;hexo g;`，然后部署`hexo d --message 'Blog Optimization'`。接下来就可以愉快地写博了。

但是，在建立连接的过程中，hexo 它升级了，对，升级了，不是在打怪过程中的那种让人开心的升级，这导致 master 分支跟 main 分支不一样，在 GitHub 上就有一句醒目的提醒挂在上面，本应该去本地的 hexo 源目录下升级就可以了，但是偏偏使用升级命令`npm install -g hexo-cli`没有任何反应，于是，选择将它合并了，于是就多出了一个奇奇怪怪的机器人分支，删也删不掉，所以在这个项目下的 Contributors 处，可以看到一个名为“dependabot[bot\]”的机器人，最终都没法清除。

### 删除奇怪的机器人

中间是如何删掉这个分支的？

后面用这个命令`npm install -g hexo-cli`还是无效，然后检查npm，`npm install -g npm-check`，

```bash
npm WARN deprecated cross-spawn-async@2.2.5: cross-spawn no longer requires a build toolchain, use it instead
npm WARN deprecated core-js@2.6.12: core-js@<3.4 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Please, upgrade your dependencies to the actual version of core-js.

changed 279 packages in 7s
```

[这篇文章](https://forum.ghost.org/t/npm-warn-deprecated-cross-spawn-async-2-2-5/5218)底下有一段说明了，这不是一个bug，可以忽略：

```markdown
It’s not an error, it’s just a warning and is completely safe to ignore (you’ll probably see a lot of them over time :wink:) . It won’t go away from re-installing anything, the dependencies/code in https://github.com/TryGhost/Ghost-CLI need updating and a new Ghost-CLI version released, once a new releas…
```

检查系统中的插件是否有升级的，`npm-check`：

```bash
hexo-algolia                   😕  NOTUSED?  Still using hexo-algolia?
                                            Depcheck did not find code similar to require('hexo-algolia') or import from 'hexo-algolia'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-algolia

hexo-deployer-git              😕  NOTUSED?  Still using hexo-deployer-git?
                                            Depcheck did not find code similar to require('hexo-deployer-git') or import from 'hexo-deployer-git'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-deployer-git

hexo-generator-archive         😕  NOTUSED?  Still using hexo-generator-archive?
                                            Depcheck did not find code similar to require('hexo-generator-archive') or import from 'hexo-generator-archive'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-archive

hexo-generator-category        😕  NOTUSED?  Still using hexo-generator-category?
                                            Depcheck did not find code similar to require('hexo-generator-category') or import from 'hexo-generator-category'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-category

hexo-generator-feed            😕  NOTUSED?  Still using hexo-generator-feed?
                                            Depcheck did not find code similar to require('hexo-generator-feed') or import from 'hexo-generator-feed'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-feed

hexo-generator-index-pin-top   😕  NOTUSED?  Still using hexo-generator-index-pin-top?
                                            Depcheck did not find code similar to require('hexo-generator-index-pin-top') or import from 'hexo-generator-index-pin-top'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-index-pin-top
hexo-generator-search          😕  NOTUSED?  Still using hexo-generator-search?
                                            Depcheck did not find code similar to require('hexo-generator-search') or import from 'hexo-generator-search'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-search

hexo-generator-tag             😕  NOTUSED?  Still using hexo-generator-tag?
                                            Depcheck did not find code similar to require('hexo-generator-tag') or import from 'hexo-generator-tag'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-generator-tag

hexo-permalink-pinyin          😕  NOTUSED?  Still using hexo-permalink-pinyin?
                                            Depcheck did not find code similar to require('hexo-permalink-pinyin') or import from 'hexo-permalink-pinyin'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-permalink-pinyin
hexo-renderer-ejs              😕  NOTUSED?  Still using hexo-renderer-ejs?
                                            Depcheck did not find code similar to require('hexo-renderer-ejs') or import from 'hexo-renderer-ejs'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-renderer-ejs

hexo-renderer-marked           😕  NOTUSED?  Still using hexo-renderer-marked?
                                            Depcheck did not find code similar to require('hexo-renderer-marked') or import from 'hexo-renderer-marked'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-renderer-marked

hexo-renderer-pug              😕  NOTUSED?  Still using hexo-renderer-pug?
                                            Depcheck did not find code similar to require('hexo-renderer-pug') or import from 'hexo-renderer-pug'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-renderer-pug
hexo-renderer-stylus           😕  NOTUSED?  Still using hexo-renderer-stylus?
                                            Depcheck did not find code similar to require('hexo-renderer-stylus') or import from 'hexo-renderer-stylus'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-renderer-stylus

hexo-server                    😕  NOTUSED?  Still using hexo-server?
                                            Depcheck did not find code similar to require('hexo-server') or import from 'hexo-server'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-server

hexo-theme-landscape           😕  NOTUSED?  Still using hexo-theme-landscape?
                                            Depcheck did not find code similar to require('hexo-theme-landscape') or import from 'hexo-theme-landscape'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-theme-landscape
hexo-theme-melody              😕  NOTUSED?  Still using hexo-theme-melody?
                                            Depcheck did not find code similar to require('hexo-theme-melody') or import from 'hexo-theme-melody'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-theme-melody

hexo-wordcount                 😕  NOTUSED?  Still using hexo-wordcount?
                                            Depcheck did not find code similar to require('hexo-wordcount') or import from 'hexo-wordcount'.
                                            Check your code before removing as depcheck isn't able to foresee all ways dependencies can be used.
                                            Use --skip-unused to skip this check.
                                            To remove this package: npm uninstall --save hexo-wordcount

Use npm-check -u for interactive update.
```

报错的最前面，有一个笑脸😊的，就是然后一堆提示命令，然后根据提示升级`npm install --save hexo@6.1.0`，然后查看 hexo 的版本，`hexo version`，从`6.0.0`升级到了`6.1.0`，顺便也将那个机器人分支给删除了，于是也就多了一个名为“dependabot[bot\]”的机器人贡献者。

### 新的报错

后续在部署的过程中，就出现了这个报错：

```bash
kex_exchange_identification: connection closed by remote host
```

[这篇文章](https://linuxhint.com/kex-exchange-identification-connection-closed/) 叙述了关于这个问题的原因，引用原文的话：

> 下面列出了其中一些原因：
>
> - SSH 服务器和客户端的 socket 连接已经中断。
> - 防火墙的规则过于严格，以至于甚至会阻止合法的连接请求。
> - 将故障设备或设备添加到您现有的网络中。
> - SSH 守护进程可能会消耗大量的网络资源。
> - 连接请求可能会过度耗尽您的端口。
>
> 结论：
>
> 今天的文章主要关注在建立网络连接时发生的 kex_exchange_identification 连接被远程主机错误关闭。我们与您讨论了导致此错误的不同可能原因，但是，修复错误的不同解决方案超出了本文的范围。

至此，结束！

















