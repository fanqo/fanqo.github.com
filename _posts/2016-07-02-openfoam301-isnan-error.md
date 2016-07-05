---
layout: post
title: "OpenFOAM301 isnan error"
description: ""
category: OpenFOAM
tags: [OpenFOAM]
---
{% include JB/setup %}

昨天逛了下[OpenFOAM的主页](http://openfoam.org/)，发现OpenFOAM更新到了4.0版本，于是心血来潮想要编译一下，把原来的OpenFOAM 3.0.1也`wclean all`了，结果今天来看时4.0版本没有编译成功，3.0.1也不行了，编译时出现错误
`error: ‘isnan’ was not declared in this scope`，
祭出Google来搜了下，发现[有人提交了bug](http://bugs.openfoam.org/view.php?id=2041)，于是按照说明修改了下`src/conversion/ensight/part/ensightPart.H`，在
{% highlight c++ %}
// Static data memebers
static const List<word> elemTypes_;
{% endhighlight %}
后面，即在ensightPart.H第63行后面加上
{% highlight c++ %}
// wrapper for isnan, namely C99 or C++11
inline bool isnan(const scalar value) const
{
#ifndef isnan
return std::isnan(value);
#else
return ::isnan(value);
#endif
}
{% endhighlight %}
编译继续。
至于OpenFOAM 4.0编译时出现错误：
{% highlight c %}
fatal error: CGAL/Delaunay_triangulation_3.h: No such file or directory
 #include "CGAL/Delaunay_triangulation_3.h"
{% endhighlight %}
这应该是CGAL的问题了，查看了下ThirdParty目录，发现里面没有CGAL文件夹，于是 `pacman -S cgal` 将CGAL安装好，编译就可以继续了。话说应该可以有方法不让它编译foamyHexMesh(它依赖于cgal)的吧。



