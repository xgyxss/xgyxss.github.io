---
title: 用markdown写博的几点注意
date: 2022-03-01 18:28:18
tags: 
  - markdown
  - 查阅文档
  - 202203
categories: 学习笔记
---

不是 Typora 工具栏里的那些常规操作！

- <a href="#target1">特殊符号的转译</a>
- <a href="#target2">锚点的书写</a>
- <a href="#target3">换行只换一行</a>
- <a href="#target4">首行缩进两格</a>
- <a href="#target5">图片并排显示</a>
- <a href="#target5">多级有序列表渲染失败</a>

<!-- more -->

书写软件用的是 Typora，写作过程中遇到的需要注意的点：

## <a name="target1">特殊符号的转译</a>

使用`\`即可，比如需要在网页上完整显示 \_config.yml 配置，需要在`_`前用`\`。

## <a name="target2">锚点的书写</a>

```html
<a href="#target">从这里跳转</a>
<a name="target">跳转到这里</a>
```

## <a name="target3">换行只换一行</a>

默认的`enter`键是换两行，只换一行的操作是`Shift+enter`键。

## <a name="target4">首行缩进两格</a>

\&nbsp;\&emsp;\&ensp;这三个都没有达到想要的效果，用下面代码即可。

```html
<p style="text-indent:2em">你的内容</p>
```

## <a name="target5">图片并排显示</a>

1. 用 figure 标签

   ```html
   <!-- 用的是figure标签 -->
   <!-- markdown显示正常，该博客框架主题下显示异常-->
   <figure class="third">
     <img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" align=left>
     <img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" align=left>
     <img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" align=left>
   </figure>
   ```

2. 用`|`分隔符

   ```markdown
   # 简单来说，就是用|将img标签分隔开
   # markdown显示正常，该博客框架主题下显示异常
   ![图二](ur1)|![图二](url)|![图二](ur1)|![图二](ur1) 
   ---|---|---|---
   ```

3. 通过`table`标签解决：

   ```html
   <table style="border:none;">
       <tr style="border:none;">
           <th style="border:none;">左边</th>
           <th style="border:none;">右边</th>
       </tr>
       <tr style="border:none;">
           <td style="border:none;"><img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" /></td>
           <td style="border:none;"><img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" /></td>
       </tr>
   </table>
   ```

   <table style="border:none;">
       <tr style="border:none;">
           <th style="border:none;">左边</th>
           <th style="border:none;">右边</th>
       </tr>
       <tr style="border:none;">
           <td style="border:none;"><img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" /></td>
           <td style="border:none;"><img src="https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/github-avatar.jpeg" width="200" height="200" /></td>
       </tr>
   </table>

## <a name="target6">多级有序列表渲染失败</a>

详见[写博查阅文档](https://yexingshusheng.com/2022/02/xie-bo-cha-yue-wen-dang.html)这篇文章中的有序列表，可以看到渲染失败的案例。

两个相连序号间也没有空行，唯一有嫌疑的就是之间插入了 iframe，在 Typora 直接显示的是空白，可能是将此判断成了空行，导致有序列表渲染失败。







