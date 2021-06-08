---
title: OS X 删除文件后系统可用空间未增加
date: 2016-07-26 12:37:45
tags:
- OS X
- macOS
---
【OS X 10.11.5】

打算用 Boot Camp 装 Win 玩守望先锋，发现空间不够。于是想要把一些大文件拷贝进移动硬盘里。

1）先用 `Cmd + C` 复制文件，然后再在移动硬盘里使用 `Cmd + Opt + V` 将文件移动进入移动硬盘。系统中被移动的文件已经消失，但是发现系统可用空间并没有增加。

2）再使用 `Cmd + C` 复制文件，直接 `Cmd + V` 粘贴进移动硬盘，然后在本地删除，清空废纸篓。然而系统可用空间并没有增加。

为了查看被删除的文件去了哪里，想要借助 DaisyDisk 来查看。

经过再一次实验后，发现被删除的文件似乎被移动到了另一个地方，在 DaisyDisk 上显示为 `(hidden space)`[^HiddenSpace]，没有权限查看。

![daisydisk-hidden-space](/images/daisydisk-hidden-space.png)

[^HiddenSpace]: [DaisyDisk 官网对 Hidden Space 的解释](https://daisydiskapp.com/manual/2/en/Topics/HiddenSpace.html)

于是...

1）由于我使用了 Time Machine 并且没有插上我用作 Time Machine 备份的硬盘，那么有理由怀疑这是 Time Machine 的本地快照（Local Snapshot）。但是我接上硬盘开启备份后，显示下一个备份只有 27 MB，与我之前删除将近 50 GB 的文件明显不符，于是排除这个可能。

2）去 Genius Bar 进行了一次硬盘检测，据说会做一些非意识性数据的删除，之后查看空间，依然未变。

3）最后尝试重启 `Cmd + R` 进入恢复模式，用 Disk Utility 对 APPLE SSD 进行 First Aid，再重启，查看空间，依然没变。

但是此时打开 Boot Camp 分区，已经可以分出超过可用空间大小的分区。

\- -，所以，这是 Apple 自己的坑吧...



