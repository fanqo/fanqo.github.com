---
layout: post
title: "Jekyll Again, 吼吼吼，我又回来啦"
description: ""
category: 
tags: [Jekyll, Cygwin, OpenFOAM]
---
{% include JB/setup %}

   最近在研究OpenFOAM，想着是不是要记录些东西，于是又把Jekyll在Cygwin下安装起来了，Jekyll的版本都升到`3.1.3`了，这一次安装起来也比较顺利，发现它的高亮可以用自带的一个叫**rouge**的东西，那就用它吧。配置完之后执行
	`jekyll s`
发现有问题`ERROR '/assets/themes/*/css/*.css' not found.`，只好放Google来搜，然后发现了[这里](https://github.com/plusjade/jekyll-bootstrap/issues/290)，好吧，对这种升级出的问题，我表示无语，按照说明对`_includes/JB/setup`和`_config.yml`进行相应修改就可以。其它的就是对`_config.yml`进行的一些细微修改。

