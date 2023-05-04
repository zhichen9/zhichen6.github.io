---
title: Ways to view pictures via ssh
date: 2023-05-04 16:13:54
toc: true
tags:
    - mac
---

远程编程的痛点之一是显示图片。

<!--more-->

## **eog**

eog（Eye of Gnome）和 matplotlib 一样都是使用 X forwarding 把远程服务器上打开的窗口投射到本地，十分卡顿。

## **imgcat**

[iTerm](https://iterm2.com) 提供的 [imgcat](https://iterm2.com/documentation-images.html) 是一个更好的选择，也是我过去三年一直在用的，不仅可以在终端展示图片，还可以下载图片到本地。

## **sshfs**

今年三月份，基于 Rust 语言开发的 [Zed](https://zed.dev) 编辑器正式进入 Beta 阶段，速度之快、体验之好以至于我刚下载它就把仅使用了三个月的 [VScode](https://code.visualstudio.com) 卸载了。我最期待的 Vim 模式以及 Remote SSH 还正在开发中，为了可以更早的体验它，我甚至可以放弃使用 Vim 一段时间。在尝试寻找暂时的远程开发的替代品的时候，我发现了 [sshfs](https://github.com/libfuse/sshfs)（SSH FileSystem）！

它可以将远程目录以挂载的形式加载到本地，如果在本地直接进入挂载的目录，也就意味着可以使用 Zed 直接进行编辑。因为 brew 并没有对相关的包进行更新，所以安装教程参考 [Install MacFuse and sshfs on macOS Monterey](https://eengstrom.github.io/musings/install-macfuse-and-sshfs-on-macos-monterey)。

因为这涉及到好几个不再更新的包，所以之后不能随便升级系统！静静等待 Zed 开发完善。

一些相关的有用的命令

{% codeblock lang:bash line_number:false %}
sshfs jliu@alblas.strw.leidenuniv.nl alblas
umount alblas
{% endcodeblock %}
