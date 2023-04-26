---
title: vysor工具——在电脑上控制Android/iOS
date: 2022-04-23 23:25:42
tags: [vysor, tools, 202204]
categories: 工具网站
---

官网网址：https://www.vysor.io/

使用场景：

1. 通用场景：减少切换手机/电脑频次的场景；
2. 办公场景：需要分别在手机和电脑上给客户展示、介绍、讲解产品时；
3. 拓展使用：适用手机线上答题的各种场景。举个栗子，线上的一些<span style="color:red;font-weight:bold;">无关紧要</span>的考试用，使用原理：利用电脑的含 OCR 功能的应用截屏取字，再键入搜索引擎直接搜索，这样既保证了答题软件没有切换应用、没有进入后台，又保证了手机的屏内录屏、摄像头内的人物稳定拍摄；可替代用双手机答题的场景，一个手机答题，一个手机拍照搜题。

<!-- more -->

以 Mac 连接 Android 手机为例，使用步骤：

1. 电脑和手机下载应用（[<span style="color:red;font-weight:bold;">Android 直链下载地址</span>](https://app.vysor.io/Vysor-release.apk)、[官网下载地址(含Mac/Windows/Linux/ChromeOS)](https://www.vysor.io/download/)、[GitHub下载地址（含Mac/Windows/Linux/ChromeOS/Android/Vysor CLI）](https://github.com/koush/vysor.io)）并打开；
2. 手机用 USB 线（<span style="color:red;font-weight:bold;">能充电+能传输数据</span>）连接 Mac，打开【开发者模式】；
3. 开启【USB 调试】；
4. 将默认 USB 配置的【仅充电】改为-->【PTP （图片传输）】；（根据 Mac 找不到 Android 时的软件提示 [网页](https://support.vysor.io/technical/notfound/) 查找得知此项）
5. 手机操作？经典的下一步即可，上述配置好后，手机自动有弹窗，根据提示操作即可连接上。

> 连不上手机的问题排查：
>
> 1.开发者模式没开；
>
> 2.没有开启允许调试；
>
> 3.USB 接口有问题；
>
> 4.数据线有问题，可能是只有充电没有数据传输功能的线。先排除软件问题，最后检查硬件问题。
>
> 连上手机后断开：
>
> 1.USB 线断开；
>
> 2.手机黑屏（一些考试软件的限制问题）；
