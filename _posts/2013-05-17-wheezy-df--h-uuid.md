---
layout: post
title: "Wheezy df UUID"
description: ""
category: "*nix相关"
tags: ["Debian", "Wheezy", "df -h", "UUID"]
---
{% include JB/setup %}

早先把系统升级为Wheezy了，发现 `df` `-h` 命令查看磁盘剩余空间时会有一个annoying uuid，类似于

    /dev/disk/by-uuid/12e0ba5f-e958-4139-bcd0-a90e532ac6e6 
	
{: prettyprint }

今天发现console的分辨率有些小了，查看了下，`/etc/default/grub`里面可以修改的样子(`GRUB_GFXMODE`)，同时意外发现还有一个 `GRUB_DISABLE_LINUX_UUID` 选项。修改了之后(别忘了`update-grub`一下) `df` 里面就再没有那"uuid"项了。PS:console分辨率还是没变的样子，汗。
