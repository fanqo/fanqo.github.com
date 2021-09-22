---
layout: post
title: "macOS Sierra下REDUCE的安装"
description: ""
category: "*nix相关"
tags: [REDUCE, macOS]
---
{% include JB/setup %}

[REDUCE][reduce]是一个CAS系统，看功能还是比较强大，想着在macOS (Sierra)下替换[Maxima][maxima]
来使用，于是就下载了`Reduce-snapshot_5847.dmg`。按其中`README`文件说明，
试着用`./redcsl`来运行，该命令会运行具有图形界面的REDUCE(需事先安装XQuartz)，
却提示错误
{% highlight bash %}
dyld: Symbol not found: __ZNKSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE4findEcm
  Referenced from: /Volumes/Reduce-snapshot/csl/reduce.app/Contents/MacOS/reduce
  Expected in: /usr/lib/libstdc++.6.dylib
 in /Volumes/Reduce-snapshot/csl/reduce.app/Contents/MacOS/reduce
Abort trap: 6
{% endhighlight %}


[reduce]:http://www.reduce-algebra.com
[maxima]:https://maxima.sourceforge.io

使用`otool -L reduce.app/Contents/MacOS/reduce`来查看REDUCE可执行文件中使用的共享库的名称为：
{% highlight bash %}
reduce.app/Contents/MacOS/reduce:
	/System/Library/Frameworks/Carbon.framework/Versions/A/Carbon (compatibility version 2.0.0, current version 157.0.0)
	/System/Library/Frameworks/CoreServices.framework/Versions/A/CoreServices (compatibility version 1.0.0, current version 775.20.0)
	/System/Library/Frameworks/ApplicationServices.framework/Versions/A/ApplicationServices (compatibility version 1.0.0, current version 48.0.0)
	/opt/local/lib/libgcc/libstdc++.6.dylib (compatibility version 7.0.0, current version 7.29.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
	/opt/local/lib/libgcc/libgcc_s.1.dylib (compatibility version 1.0.0, current version 1.0.0)
	/System/Library/Frameworks/CoreFoundation.framework/Versions/A/CoreFoundation (compatibility version 150.0.0, current version 1350.10.0)
{% endhighlight %}

系统中不存在`/opt/local/lib/libgcc`文件夹，而`/usr/lib/libstdc++.6.dylib`使用`nm`查看
`nm libstdc++.6.dylib | grep '__ZNKSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE4findEcm'`
发现没有该Symbol。

先前系统`brew install gcc`安装了`GCC 6.3.0`，它里面的`libstdc++.6.dylib`中是包含该Symbol的。
所以这里有两种解决方法，一是把`brew`安装的GCC的库作链接：
{% highlight bash %}
sudo mkdir -p /opt/local/lib
cd /opt/local/lib
sudo ln -s /usr/local/Cellar/gcc/6.3.0_1/lib/gcc/6 libgcc
{% endhighlight %}
或者是用`install_name_tool`将可执行文件中库的路径替换掉：

{% highlight bash %}
cd csl/reduce.app/Contents/MacOS
install_name_tool -change /opt/local/lib/libgcc/libstdc++.6.dylib /usr/local/Cellar/gcc/6.3.0_1/lib/gcc/6/libstdc++.6.dylib ./reduce
install_name_tool -change /opt/local/lib/libgcc/libgcc_s.1.dylib /usr/local/Cellar/gcc/6.3.0_1/lib/gcc/6/libgcc_s.1.dylib ./reduce
{% endhighlight %}

两种方法均可，然后再运行`./redcsl`发现还是有问题，这次是fontconfig的问题了：
{% highlight bash %}
./redcsl 
Fontconfig error: Cannot load default config file
terminate called after throwing an instance of 'FX::FXFontException'
Abort trap: 6
{% endhighlight %}

这个处理起来就比较容易了，参照[这里](http://blog.neten.de/posts/2013/10/06/use-ffmpeg-to-burn-subtitles-into-the-video/)，在`.bashrc`中添加
{% highlight bash %}
export FONTCONFIG_PATH=/opt/X11/lib/X11/fontconfig
{% endhighlight %}
即可。