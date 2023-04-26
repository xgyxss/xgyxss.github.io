---
title: IT文档中的一些术语（20220721更新）
date: 2022-06-25 20:06:39
tags: [202206, IT, 术语]
categories: [学习笔记]
---

在阅读IT文档的过程中经常出现一些易忘的、非字面意思的术语，从当前日期开始记录整理。

<!-- more -->

### shebang

也称为 Hashbang。由井号和叹号构成的字符序列`#!`，其出现在文本文件的第一行的前两个字符。在文件中存在 Shebang 的情况下，类 Unix 操作系统的程序加载器会分析 Shebang 后的内容，将这些内容作为解释器指令，并调用该指令，并将载有 Shebang 的文件路径作为该解释器的参数。

例如，以指令`#!/bin/sh`开头的文件在执行时会实际调用`/bin/sh`程序（通常是 Bourne shell 或兼容的 shell ，例如 bash、dash 等）来执行。这行内容也是 shell 脚本的标准起始行。

Unix 术语中，井号通常称为 *sharp*，*hash* 或 *mesh*；而叹号则常常称为 *bang*。

> rf.https://zh.wikipedia.org/wiki/Shebang

#### 食用方法：

##### 1.先添加shebang标识

使 Java 支持使用：

> ```java
> #!/usr/bin/java --source 11
> ```

使用`#!/usr/bin/env 脚本解释器名称`是一种常见的在不同平台上都能正确找到解释器的办法：

> 使某些脚本语言(例如 Python 或 Bash)支持使用：
>
> ```python
> #!/usr/bin/env python
> ```
>
> 使 Node.js 支持 JavaScript 文件的 shebang：
>
> ```javascript
> #!/usr/bin/env node
> ```
>
> 使 [ts-node](https://github.com/TypeStrong/ts-node) 支持 TypeScript 文件的 shebang：
>
> ```typescript
> #!/usr/bin/env ts-node
> ```

##### 2.修改文件的可执行权限

```bash
chmod +x [filename]
```

##### 3.运行脚本

```bash
./[filename]
```

作为单文件简单测试使用时，只要有正确的运行环境和 shebang 标识，对应文件后缀名可有可无，也可正确执行。

### Hooks

引用知乎上的一张著名的示意图：

![引用知乎上的图](https://cdn.jsdelivr.net/gh/xgyxss/picgo@main/img/hexo/hooks.webp)

字面理解，钩子。

专业理解，通过一系列技术，截获在软件代码之间传递的函数调用/事件，来更改/增强其他软件组件、应用程序或操作系统的行为，处理此类拦截的函数调用、事件或消息的代码称为“Hooks”。

简单理解，就是在消息过去之前，可以先把消息勾住，不让其传递，然后自己的操作优先处理。即在操作某行为之前，优先处理一下。

生活示例：在发朋友圈之前，P 一下（即 Hook 操作），发朋友圈。

### FOSS

Free and open-source software：软件; 自由和开源软件; 开源软件;

### OAOO

Once and only once 一次且仅一次，又称 DRY，Don't repeat yourself。

一个规则，实现一次（One rule, one place）是面向对象编程中的基本原则，程序员的行事准则。旨在软件开发中，减少重复的信息。

### WET

违反 DRY 原则的解决方案通常被称为 WET，其有多种全称，包括“ Write everything twice ”（把每个东西写两次）、“ We enjoy typing ”（我们就是喜欢打字）或“ Waste everyone's time ”（浪费大家的时间）。

WET大致能分成4种：
Imposed duplication：开发者认为不得不的重复
Inadvertent duplication：开发者没有意识到的重复
Impatient duplication：开发者复制自己或他人的程式码造成的重复
Interdeveloper duplication：不同开发者间共同开发或交接造成的重复
有时，为了可读性，或避免耦合，或过早重构，应放弃 DRY 原则。 
