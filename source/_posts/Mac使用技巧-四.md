---
title: Mac使用技巧(四)
date: 2022-03-27 18:00:00
tags: [Mac, 使用技巧, 202203]
category: 学习技巧
---

Mac 使用技巧，一篇文章写完太长，影响阅读体验，于是写成了一个系列。

该系列相对比较全面，对于 Mac 0 基础的小白有着很大的提升。

同时为了便于查找，将每篇文章的主要内容都会做一个简单的目录介绍和锚点跳转。

- <a href="#target1">Macbook/iMac 上灰尘清除小技巧</a>
- <a href="#target2">快速修改图片尺寸</a>
- <a href="#target3">修改 Mac 基础设置的几个终端命令</a>
- <a href="#target4">清理和优化 Mac 的几个强大技巧</a>
- <a href="#target5">如何更改您的 Mac 区域</a>
- <a href="#target6">复制粘贴不能用了？</a>

<!-- more -->

### <a name="target1">Macbook/iMac 上灰尘清除小技巧</a>

出现灰尘问题的三个迹象：

1. 意外停机
2. 系统性能缓慢
3. 风扇噪音过大

- 定期清洁，在低尘环境中至少每6个月一次，在高尘环境中更频繁
- 基本的 MacBook 维护
  - 始终使用坚硬的表面，在柔软的床上使用，只会让它过多地暴露在更多的灰尘中
  - 保持房屋和表面无灰尘
  - 每隔一段时间让风扇转动：在灰尘颗粒结块之前将其清除
- 苹果服务中心

### <a name="target2">快速修改图片尺寸</a>

双击打开图片，macOS 默认的打开图片是【预览】，如果更改了默认打开的应用，可以右键，打开方式选择【预览】。在菜单栏，选择【工具】->【调整大小】。在弹出窗口中的，宽度那个输入框，输入你想要用图片宽度，点【好】后，图片将会按照长宽比自动缩小。如果你不需要保持长宽比，可以取消下方的【比例缩放】的勾选即可。最后，需要将修改的图像进行保存，可以通过快捷键【⌘ + S】，或在菜单中【文件】->【存储】进行保存。

### <a name="target3">修改 Mac 基础设置的几个终端命令</a>

- 设置关机定时器：

  ```bash
  sudo shutdown -h +60 #以分钟为单位
  ```

  > -h 停止或关闭
  >
  > -r 重新启动
  >
  > -s 睡眠
  >
  > 如果需要，可以使用格式为 yymmddhhmm 的特定日期和时间。
  >
  > 要在计时器结束之前取消计时器，只需运行：
  >
  > ```bash
  > sudo killall shutdown
  > ```
  >
  > 它会终止在后台运行的关闭进程。

- 防止您的 Mac 进入睡眠状态：

  ```bash
  caffeinate -u -t 3600 && killall Dock #以秒为单位
  ```

  > -u 告诉系统就好像用户处于活动状态一样，因此显示器也不会进入睡眠状态
  >
  > -t 设置一个定时器

- 显示隐藏的文件和文件夹

  ```bash
  defaults write com.apple.finder AppleShowAllFiles -bool TRUE && killall Dock
  ```

  > 快捷键：【⌘ + ⇧ + .】

- 隐藏自己的文件和文件夹

  ```bash
  chflags hidden ~/Dekstop/MySecrets && killall Dock
  ```

  将路径改成自己的秘密文件夹或文件的路径。

- 自定义 dock

  - 添加一个空白间隔

    ```bash
    defaults write com.apple.Dock persistent-apps -array-add '{"tile-type"="spacer-tile";}' && killall Dock
    ```

  - 隐藏当前未运行的所有应用程序

    ```bash
    defaults write com.apple.Dock static-only -bool TRUE && killall Dock
    ```

  - 用 ⌘ + H 来隐藏应用程序，也可在 Dock 中将它们的图标变暗

    ```bash
    defaults write com.apple.Dock showhidden -bool TRUE && killall Dock
    ```

  - 自动显示和隐藏 Dock

    ```bash
    defaults write com.apple.Dock autohide-delay -float 0 && killall Dock
    ```

  - 默认的自动隐藏设置

    ```bash
    defaults delete com.apple.Dock autohide-delay && killall Dock
    ```

- <span style="color:red;">**最后，别忘了，以上命令需要重启 Finder 让修改的命令生效！**</span>

  ```bash
  killall Finder
  #或者在每条命令后面加上 && killall Dock，例如：
  defaults write com.apple.Dock persistent-apps -array-add '{"tile-type"="spacer-tile";}' && killall Dock
  ```

- 更改屏幕截图的存储位置

  ```bash
  defaults write com.apple.screencapture location ~/Pictures && killall SystemUIServer
  #替换~/Pictures为您要使用的任何文件夹。如果要恢复默认行为，只需将该路径~/Desktop替换为。
  ```

- 删除屏幕截图周围的阴影

  ```bash
  defaults write com.apple.screencapture disable-shadow -bool TRUE && killall SystemUIServer
  ```

- 将这些屏幕截图的文件类型（默认为 PNG）更改为其他类型

  ```bash
  defaults write com.apple.screencapture type JPG && killall SystemUIServer
  ```

- 更改屏幕截图文件的默认名称

  ```bash
  defaults write com.apple.screencapture name "mycapture" && killall SystemUIServer
  ```

  > 可以将mycapture替换为您想要的任何文件名。

- 观看星球大战

  ```bash
  nc towel.blinkenlights.nl 23
  ```

  > 很久以前，在一个很远很远的终端里，一些有进取心的人用 ASCII 重新创建了《新希望》的全部内容。它今天仍然可以在终端中使用，并且在当前版本的 macOS 上。观看以文本形式播放的故事。

### <a name="target4">清理和优化 Mac 的几个强大技巧</a>

- 删除缓存文件

  打开【Finder】-【前往】-【前往文件夹】，Type /Library/Caches 并清理您在其中找到的文件夹的内容（确保删除内容而不是文件夹），清空垃圾桶。

- 减少启动和登录项的数量

  【用户与群组】-【登陆项】

- 删除浏览器缓存

- 使用维护脚本

- 清理下载文件夹

  即使您下载应用程序并将其移动到应用程序，它也会在您的下载中留下一个安装程序文件。你可以到【Finder】-【下载】并手动删除文件。

- 删除旧的 iOS 备份

  1. 在Apple菜单中，选择关于本机
  2. 导航到【存储】-【管理】
  3. 单击左侧选项卡中的 iOS 文件
  4. 删除备份

- 修复磁盘权限

  修复损坏的权限可以帮助某些应用程序运行得更快，或者，如果您在删除文件时遇到问题，这也可以修复它。

- 删除未使用的应用程序

  如果你只是将一个应用程序移到 Bin，它会留下很多痕迹。要清除应用程序遗留物，您需要打开 【Finder】-【Go】-【 Go to folder】-【~/Library/Application Support/您的应用程序名称】，然后删除文件夹中的内容。

  在 【~/Library/Caches/Your app name】中重复相同的操作。

  然后，转到 【~/Library/Preferences】，键入您的应用程序名称，然后删除应用程序首选项。

- 减少杂乱

  在Apple菜单中选择【关于本机】-【存储】-【管理】。单击【减少混乱】选项旁边的【查看文件】。删除占用太多空间的特别大的文件。

- 清倒废纸篓

### <a name="target5">如何更改您的 Mac 区域</a>

【系统偏好设置】-【语言和地区】-【地区】，更改您的地区也会更改 Mac 的主要语言，具体取决于您选择的国家/地区。您将收到有关此更改的提示。单击立即重新启动以应用新更改重新启动 Mac。

### <a name="target6">复制粘贴不能用了？</a>

- 如何修复 Mac 中的复制和粘贴。

  在 macOS 中修复不能使用的剪贴板的方法本质上是找到该特定进程并重新启动它。您可以通过两种方式执行此操作：使用终端或活动监视器。

  1. 终端：

     ```bash
     killall pboard
     ```

  2. 活动监视器：找到 pboard，单击停止图标，选择强制退出。





