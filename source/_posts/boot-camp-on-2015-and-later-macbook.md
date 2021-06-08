---
title: 2015年后的 Macbook 的 Boot Camp 安装问题
date: 2016-07-26 19:46:49
tags:
- OS X
- macOS
---
【OS X 10.11.5】

# 前情提要

不太确定是 2015 年后 Macbook 的因素还是 OS X 10.11 的因素，Boot Camp 安装的方式发生了改变。

根据官网只提供了 2015 年以前的 Boot Camp Assistant 的下载，推测多半是硬件因素。

# 安装流程

新 Boot Camp 双系统的安装不再需要使用外部 U 盘来创建安装盘，同时也不会自动在成功安装后的 Windows 中自动安装 Boot Camp 助理，使得触摸板双指滑动、右键等等功能均无法使用。

在 2015 年后的 Macbook 中打开 Boot Camp Assistant，选择镜像并选定分区空间后，将会下载 Support Software，并且每次重新安装 Windows 都会重新下载，估计大小为 1 GB 左右。

如果你所在的网络环境下载速度过慢，可以去你所在地的苹果直营店，在直营店 Genius Bar 里接入该店的网线用其内部网络进行下载，速度如下：
![boot-camp-download-speed-under-network-in-apple-store](/images/boot-camp-download-speed-under-network-in-apple-store.png)

下载安装完毕后，会开始分区，拷贝 Windows 文件。

以上流程完毕会自动重启进入 Windows 安装界面，在安装过程中，需要将划分出的 BOOTCAMP 分区格式化为 NTFS 格式。同时你会发现该分区比你之前分区的大小少了近 8 G，和另一个 OSXRESERVED 分区。

安装完成后进入 Windows 系统，打开 `计算机` 会发现除了 C 盘意外，还有一个我们之前见过的 OSXRESERVED 盘，点击其目录下的 `setup.exe` 会重新开始安装 Windows。

进入其目录下的 `Boot Camp`，再点击 `Boot Camp` 下的 `setup.exe` 会进入 Boot Camp 助理的安装引导，完成后，OSXRESERVED 分区会消失，其占用空间会合并进 C 盘。

# 可能遇见的问题

安装成功并进入 Windows 后，在 `计算机` 中可能没有 OSXRESERVED 盘，如果多次重启仍然没有，似乎只有尝试重新安装，直至其出现。

我第一次安装时不清楚需要手动安装 Boot Camp 助理，在发现没有 Boot Camp 助理后尝试多次重启，并且在开机时进入启动管理器界面，会看到 OSXRESERVED 分区，但多次重启之后消失，Boot Camp 助理也没有自动安装。似乎新的 Boot Camp 仍然有一些 Bug。


