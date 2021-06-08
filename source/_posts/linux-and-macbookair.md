---
title: 给 Macbook Air 安装 Linux
date: 2016-07-18 23:21:15
tags:
- Linux
- Macbook
---

从老妈那里拿到一台 Macbook 3,1 (Macbook Air 2010 Late)，Core 2 Duo 1.4GHz，2G RAM 可换，加上 Air 本身轻便，完全是刷个 Linux 就可以满血复活，杀人越货的利器！

最开始打算装 Ubuntu，在 Ubuntu Community Wiki 界面中 [Macbook Air 的支持页面](https://help.ubuntu.com/community/MacBookAir)，针对我这台 Model 最新只有 Ubuntu 13 的教程，而且各个步骤非常麻烦。

一气之下，改换 Elementary OS，一个基于 Ubuntu，界面神似 macOS（原 OS X）的 Linux。在 Elementary OS 官网直接有 [Installation Guide](https://elementary.io/zh_CN/docs/installation#installation) 具体步骤如下：

- 下载 Elementary OS 镜像
- 使用 [Etcher](http://www.etcher.io/) 将镜像烧录至U盘
- 重启设备，在开机时按住 Option 键从U盘启动
- 选择U盘（EFI Boot）可进入 Elementary OS

但第一次尝试直接安装 Elementary OS 时失败，随后重新启动，选择 `try elementary os` 进入 Elementary OS，再在 Elementary OS 中点击 Dock 栏中的 `Install Elementary OS` 即可安装。安装完成后可能进入无限重启，强制关机后再开机即可。

最后测试，Wifi，Bluetooth，功放均无问题。

知道这种方式之后，用同样的方式烧录 NixOS、Ubuntu、Arch，似乎都可以用这种方式安装，不过没有尝试。

查看 Arch 的 Wiki 感觉安装有些复杂。准备先跟《鸟哥的 Linux 私房菜》再深入了解一下 Linux，再去折腾。

