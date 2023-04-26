---
title: 不建议将iTerm设置为VS Code的集成终端
date: 2022-08-14 19:39:10
tags: [202208]
categories: [转录归档]
---

最初问题出现在 VS Code 某一次更新后...

<!-- more -->

之前一直将 iTerm 作为 VS Code 的集成终端，此前，已经折腾过 iTerm 了，在 VS Code 某一次更新后，官网里面只有关于 Windows 的 powershell 配置，没有 Mac 的相关配置，后续一直在 VS Code 终端上出现奇怪的报错，比如 not found npm，根本原因终于找到了。[Kronos](https://stackoverflow.com/users/8030861/kronos) 的原文解释：

> **iTerm is not a shell but a terminal emulator which in your case is running the zsh shell.**
>
> I believe you are confusing the terms Shell and a terminal emulator.
>
> iTerm is a terminal emulator. Some examples of terminal emulator are Gnome terminal, Guake, Xterm etc. They provide a display to the shell which is installed in the OS.
>
> A shell is a command line interface that reads and interprets your commands. Examples of shell are bash which comes by default in Linux and other shells like zsh, fish, sh.
>
> **Visual Studio Code integrated terminals** use the **shell itself** and not the terminal emulator. In Windows OS the distinction between shell and terminal emulator is not present so Powershell and Command Prompt are both the shell and the emulator.
>
> But for Unix like OSes there is a distinction.
>
> I believe you use iTerm as the terminal emulator and the shell used is zsh (pronounced Z Shell which is a fork of bash Bourne Again Shell).
>
> Here is a wikipedia article on [Unix Shell](https://en.wikipedia.org/wiki/Unix_shell). This talks about what a Unix shell really is.
>
> This link is about [Terminal emulators](https://en.wikipedia.org/wiki/Terminal_emulator) which also talks about the history of terminals.
>
> This link gives a [list of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators) that are available. iTerm is a terminal emulator for Mac OS.

摘要大意就是：

VS Code 集成终端使用 shell 本身，而 Mac OS（类 Unix）上的 iTerm 是一个终端仿真器，而 Windows 中不存在 shell 和终端仿真器，因此， powershell 和命令提示符既是 shell 又是仿真器。

这也正好解释了 VS Code 官网为什么只有 Windows 下的终端配置而没有 Mac 下的终端配置的原因。

至于哪些开发软件只能采用 shell，没必要去纠结判断，结论就是：Mac OS 上开发工具的终端回归默认，可以从根源上避免终端仿真器带来的 bug。

> rf.
>
> [VS Code官网终端配置文件](https://code.visualstudio.com/docs/terminal/profiles)
>
> [不能将iTerm设置为VS Code的集成终端](https://stackoverflow.com/questions/43900516/integrated-terminal-setting-vs-code-and-iterm-returns-zsh/44163545#44163545)
>
> [Unix Shell](https://en.wikipedia.org/wiki/Unix_shell)
>
> [终端模拟器](https://en.wikipedia.org/wiki/Terminal_emulator)
>
> [终端模拟器的列表](https://en.wikipedia.org/wiki/List_of_terminal_emulators)
>
> [Change default terminal app in Visual Studio Code on Mac](https://stackoverflow.com/questions/29957456/change-default-terminal-app-in-visual-studio-code-on-mac)

