---
layout: post
title: "Cygwin下安装matplotlib"
description: ""
category: Progs
tags: [Cygwin, Python, matplotlib]
---
{% include JB/setup %}
已经忘了是怎么样找到[这个网页](http://www.zhihu.com/question/21664179)的，反正是看到了用`matplotlib`画的一些图像觉得挺漂亮。看到这些图像，忍不住想要看一下这个`matplotlib`是个啥(虽然不懂Python，不管了，装了再说)。

由于是在Windows下，还装好了Cygwin，所以就在Cygwin下测试了。安装`matplotlib`之前要安装好`libfreetype-devel`还有`numpy`。这里我用的是`python3`，这样`Python`的版本号为`3.2.5`，`python3-numpy`的版本号为`1.7.2-1`，`libfreetype-devel`的版本号为`2.5.3-1`，其它一些依赖的版本号就没太注意。

从网上down下`matplotlib-1.3.1.tar.gz`解压，按[这里](http://stackoverflow.com/questions/5151755/how-to-install-matplotlib-on-cygwin)给的操作，`cd`到解压后的目录，如`matplotlib-1.3.1`，将`setup.cfg.template`复制为`setup.cfg`并修改其中的`#tkagg = auto`为`tkagg = False`(取消注释，并将`auto`改为`False`)。然后直接`python3 setup.py install`会发现有一错误
{% highlight bash %}
lib/matplotlib/tri/_tri.cpp: …… expected identifier ……
{% endhighlight %}
(省略了该错误提示中的大部分)。

看到[这里](https://github.com/matplotlib/matplotlib/issues/2463)说是`_tri.cpp`和`_tri.h`中的一个变量`_C`的问题，将其改个名字就好了，偷懒给它改为`_Co`了(注意不要把以`_C`开头的其它变量也给改了)。然后再运行`python3 setup.py install`就没有问题了。

到此，`matplotlib`在Cygwin下就安装完成了。
