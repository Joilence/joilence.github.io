---
title: OS X 使用 Disk Utility 分区后无法回收及后续问题
date: 2016-07-22 23:10:34
tags: 
- OS X
- macOS
---
【OS X 10.11.5】

// 此处应有故事起因

然后手快拿 Disk Utility 分了区，分了 75G 出去。

// 此处应有故事过程

然后之间点击 Partition，把饼状图中之前的分区通过点击下方 `-` 按钮移除，于是出现了以下情况： 

![Disk-Utility-SSD](/images/Disk-Utility-SSD.png)
![Disk-Utility-Partition](/images/Disk-Utility-Partition.png)
分区的确是删除了，APPLE SSD 也依然是 500G 容量但是分区的空间并没有被 Macintosh HD 回收。迷之消失的 75G。

打开终端，输入 `diskutil list`，回车。

![diskutil-list](/images/diskutil-list.png)

发现 Recovery HD 变成了 75G，也就是说，移除的分区被 Recovery HD 吃掉了。那么是不是只要把 Recovery HD resize 一下就好呢？然而...

![diskutil-resize](/images/diskutil-resize.png)

并不行。

问过 Apple Genius 之后，得知这个是一个存在很久的 Bug，当你在使用逻辑卷宗（比如使用了 FireVault 加密）时，直接移除分区，Recovery HD 就会直接吞掉分区容量。现在的办法只有把盘格式化掉再重装系统了。

重装完成后，发现虽然 Recovery HD 还在，但无法进入恢复模式。进入后屏幕左上角会提示如上信息。

![cannot-enter-recovery-hd](/images/cannot-enter-recovery-hd.png)

接着就开始自动重启。

再次求助 Apple Genius，Genius 表示也不太清楚是什么问题，做了硬盘测试，没有发现问题。随后再次重装系统测试，此时 Genius 给我讲了一个非官方的「古老」方法解决各种奇奇怪怪的硬盘问题。

当要格式化 APPLE SSD 时，选择 Erase，然后更改 Partition Scheme 为 [Apple Partition Map](https://en.wikipedia.org/wiki/Apple_Partition_Map)，格式化完成之后再格式化回 GUID Partition 即可。

Genius 表示也不知道为什么... 反正就是有效果，尤其是针对一些老设备。当然对我这台 MacbookPro12,1（2015 Late）似乎也生效了。

