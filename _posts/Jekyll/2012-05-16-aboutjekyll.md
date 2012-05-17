---
layout: post
title: "Jekyll相关"
description: "与Jekyll相关的一些笔记"
category: [Jekyll]
tags: [Jekyll]
---
{% include JB/setup %}

博客转到[GitHub][github]来了，网站的生成器就用的[Jekyll][jekyll]。从[JekyllBootstrap] [JB] fork下来一些东西，改了改主题，就算正式开工了。看了看Jekyll Bootstrap的文档，这里做点笔记。

[github]: https://github.com "GitHub"
[jekyll]: https://github.com/mojombo/jekyll/ "Jekyll"
[JB]: http://jekyllbootstrap.com "Jekyll Bootstrap"

## Post或Page的创建及发布 ##

_创建Post文章_

	rake post title="文章标题"
会自动创建一个具有合适文件名和YAML Front Matter的文件(使用时将"文章标题"替换成你要创建的文章的标题)。

_创建Page页面_

	rake page name="页面名称.md"   或者
	rake page name="pages/页面名称.md"

_发布Post或Page_

	git add .
	git commit -m '一些说明'
	git push origin master



## Jekyll 目录及一些说明 ##

_Jekyll 标准目录树_

	_config.yml   Jekyll的配置文件
	_includes     include 文件所在的文件夹
	_layouts      模版文件夹
	_posts        自己要发布的内容
	_sites        预览时产生的文件都放在该文件夹中

Jekyll的安装及配置请查看 [Jekyll wiki][jekyll wiki]。  
`_includes`文件夹中所放的文件是最终要放到模版中的一些代码片段。  
`_layouts`中放的一些模版，模版是用包含page或post内容的。Jekyll的模版使用HTML语法来写，并包含YAML Front Matter。所有的模版都可用[Liquid] [liquid] 来与网站进行交互。所的的模版都可以使用全局变量`site`和`page`，`site`变量包含该网站所有可以接触得到的内容和元数据(meta-data)，`page`变量包含的是当前渲染的page或post的所有可以接触得到的数据。  
`_post`文件夹中放的是自己要发布的post文章。post文件的命名规则为`YEAR-MONTH-DATE-title.MARKUP`，使用`rake post`会自动将post文件命名合适。而对于page，所有放在根目录下或不以下划线开头的文件夹中有格式的文件都会被Jekyll处理成page。这里说的有格式是指文件含有YAML Front Matter。所有的post和page都要用`markdown`或者`texile`或者HTML语法来写，并可以包含`Liquid`模版的语法。还要有 YAML Front Matter (Jekyll只处理具有YAML Front Matter的文件)。YAML Front Matter必须放在文件的开头，一对`---`之间，用户可在这一对`---`间设置预先定义的变量或用户自己的数据：

	---
	变量或用户自己的数据
	---
	
Jekyll Bootstrap在根目录下还有一文件夹`assets`，这里可以用来放一些图片、CSS文件或Javascript文件，这些文件不应包含YAML Front Matter，以免被Jekyll处理成页面。在自己post或page中引用该文件夹下的内容时可用\{\{`ASSET_PATH`\}\}代替该目录。

[jekyll wiki]: https://github.com/mojombo/jekyll/wiki/
[liquid]: http://liquidmarkup.org/
