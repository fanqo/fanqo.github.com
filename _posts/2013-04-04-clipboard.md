---
layout: post
title: "Linux Clipboard"
description: ""
category: "*nix相关"
tags: ["linux", "clipboard", "X window system", "rdesktop"]
---
{% include JB/setup %}

这里所说的Linux Clipboard实际上指的是 [X window system 下的Clipboard](http://www.freedesktop.org/wiki/Specifications/ClipboardsWiki)。起因是我想在Virtualbox headless下的XP中使用剪贴板，看了看rdesktop的帮助文档，结果发现clipboard有两个选项：PRIMARYCLIPBOARD，CLIPBOARD。这不免让我想知道它们的区别，结果就发现了[这个Wiki](http://www.freedesktop.org/wiki/Specifications/ClipboardsWiki)。    
看了半天，没怎么看懂，听它的意思，说X有个类clipboard的东西，不过它叫selections，还有三个标准的selections：PRIMARY, SECONDARY, CLIPBOARD。还给出了定义，好吧，这里我看得一塌糊涂。简单地说，SECONDARY你就不用管了；CLIPBOARD就像是Mac或Windows下的剪贴板一样；至于PRIMARY就是一个“彩蛋”吧也就使你选中一段文字，然后在别的地方能用鼠标中键粘贴的东西。
