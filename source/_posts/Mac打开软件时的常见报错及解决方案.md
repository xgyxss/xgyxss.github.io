---
title: Mac打开软件时的常见报错及解决方案
date: 2022-08-21 19:59:00
tags: [202208,Mac]
categories: 解决方案
---

起因是今天打开一款第三方软件（通过包管理器 brew 安装的软件）时，报错：是否含恶意软件...

<!-- more -->

常见三种报错：

1. xxx已损坏，无法打开，你应该将它移到废纸篓解决办法
2. 打不开 xxx，因为它来自身份不明的开发者
3. 打不开xxxx，因为 Apple 无法检查其是否包含恶意软件

通常解决方案：

1. 打开任何来源
   - 终端键入并回车：`sudo spctl --master-disable`
2. 绕过公证
   - 终端键入：`sudo xattr -rd com.apple.quarantine <应用路径>`，回车。（注意路径与前面的空格）
   - 简单点，终端键入：`sudo xattr -rd com.apple.quarantine`，然后将该打不开的软件拖入终端，自动生成路径，回车。
3. 应用签名
   - 安装Command Line Tools 工具：`xcode-select --install`
   - 给应用签名：`sudo codesign --force --deep --sign - <应用路径>`（这里注意应用路径和前面短横线之间的空格）
   - 成功提示：/文件位置 : replacing existing signature
   - 暂未遇到过失败，如遇到参见文末引用链接

至此，95% 的应用都能正常运行。以上方法在以前的电脑版本基本上都能解决。

但，这次遇到的事情没这么简单，以上方法均失效，可能需要关闭 SIP 系统完整性保护，但这无异于系统裸奔，遂不尝试。

替代方案：brew 上的软件大多是开源软件，GitHub 上大多都能找到，或者到第三方软件聚合平台、破解软件平台。

原因：抛开版本谈崩坏有点扯淡，当前电脑版本：macOS Monterey 12.5.1，也可能和修补漏洞有很大关系。

> 19号的资讯原文（原文见文末引用链接）：
>
> Apple 已警告Mac、iPhone、iPad 和一些 iPod 最近的一些操作系统存在重大安全漏洞，可能允许黑客控制您的设备。
>
> 这种安全漏洞可以“执行任意代码”，意味着黑客可以在您的设备上运行任何代码。苹果在他们的发布中表示，他们收到了一份报告，称此漏洞可能已在 Mac 和 iPhone/iPad 上被滥用，但没有透露人们如何受到影响。
>
> 苹果表示，这些漏洞影响操作系统的两个不同部分：内核和 WebKit。

> rf.
>
> 官网的解决方案：[打开来自身份不明开发者的 Mac App](https://support.apple.com/zh-cn/guide/mac-help/mh40616/mac)
>
> [软件已损坏,无法打开,你应该将它移到废纸篓，打不开 xxx,因为它来自身份不明的开发者](https://juejin.cn/post/6971720447549243405)
>
> [Users Beware: Apple Announces Security Flaw Affecting iPhones, iPads, and Macs](https://gizmodo.com/apple-security-hack-iphone-ipad-mac-1849433434)
