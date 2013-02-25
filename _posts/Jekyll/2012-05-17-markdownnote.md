---
layout: post
title: "MarkDown一些笔记"
description: "关于MarkDown的一些笔记"
category: Jekyll
tags: [MarkDown]
---
{% include JB/setup %}

## MarkDown语法 ##


这里的内容来自对[MarkDown Base][MB]和[MarkDown Syntax][ms]的翻译。所有MarkDown不包含的语法，都可以直接使用HTML自己的标记。唯一的限制就是HTML中的块元素，如：`<div>`，`<table>`，`<pre>`，`<p>`等，必须和周围的内容用空行分开，并且这些块的开始和结束不能缩进。注意：不能在HTML块中使用MarkDown风格的标记。对于MarkDown有的语法也可以直接用HTML标签来代替。MarkDown不会处理代码(code)和HTML块中的MarkDown语法。   

[mb]: http://daringfireball.net/projects/markdown/basics "MarkDown Base"
[ms]: http://daringfireball.net/projects/markdown/syntax "MarkDown Syntax"

_[段、标题、块引用](#phb)_		_[强调](#em)_		_[列表](#list)_		_[链接](#link)_		_[图象](#img)_		_[代码](#code)_		_[其它](#other)_


### 段、标题、块引用 ### 
{: #phb}

段(paragraph)就是一行或多行连续的文字，这些文字由一个或多个空行将它们与其它内容分开。MarkDown支持硬换行(hard wrap)，若要在一段内加入一`<br />`标签，只需在一行的结尾加入两个或多个空格，再按下回车键。    
MarkDown提供两种方法来标记标题(header)：Setext和atx。Setex风格是以`=`或`-`做下划线来分别得到一级、二级标题：

	这是一级标题
	===
	
	这是二级标题
	------
{: .prettyprint}	
	
`=`或`-`的数目无关紧要。atx风格则由`#`做一行的开头引出标题，`#`的数目对应标题的等级(1~6个`#`分别对应1~6级标题)：

	# 一级标题 #
	## 二级标题 ##
	.
	.
	.
	###### 六级标题 ###
{: .prettyprint}	
	
标题后面可以跟上任意数目的`#`号(为了好看，可以跟上与标题等级对应数目的`#`)。  
块引用(blockquote)由`>`来指示，块引用中可以包含块引用、标题、列表以及代码块。

    >引用  
    >下面是一些代码
    >
    >     代码
    >
    >下面是一些块引用
    >>引用中的引用
    >   
{: .prettyprint}	
	
	
### 强调   {#em}

MarkDown用一对`*`或`_`以及一对`**`或`__`来表示强调：

     *<em>强调*
	 _<em>强调_
	 **<strong>强调**
	 __<strong>强调__
{: .prettyprint}	 
	 
`*`或`_`与要强调的内容间不要有空格。

### 列表    {#list}

无序列表(unordered list)由单个`*`或`+`或`-`引导：

     * 无序表
	 + 无序表
	 - 无序表
{: .prettyprint}	 
	 
有序列表(ordered list)由数字加`.`来引导。该数字并不影响列表最后的排序：

     3. 有序表
	 1. 有序表
{: .prettyprint}	 
	 
列表的引导符号前最多有3个空格，引导符号后至少要有一个空格或`tab`。一个表项(list item)中可能会有多个段落，每一个后续的段落的开始要缩进4个空格或1个`tab`。要在表项中引入块引用，`>`必须缩进。<del>__我这里测试中文表项好像有问题__</del><ins>将markdown引擎设为<code>kramdown</code>后就可以了，<del>只是<code>atx</code>风格的标记标题时，若要手动指定<code>header ID</code>就不能在标题后面加上<code>#</code>的样子</del>可在标题的下一行用`{: #id}`来设置标题的id</ins>。


### 链接   {#link}

MarkDown支持两种风格创建链接：行间(inline)风格和引用(reference)风格。   
行间风格由`[]`将链接文本括起，后面跟着`()`，`()`中放着链接的地址或地址加`title`属性：
     
	 [链接文本](地址)
	 [链接文本](地址  "title属性")
{: .prettyprint}	 
	 
引用风格可通过名字引用链接，链接的名字在别处定义。链接名可以包含字母、数字、空格，并不区分字母的大小写：

	[链接文本][链接名字]
{: .prettyprint}	
	
链接名字定义为`[]`括起链接名后紧跟一`:`，然后是空格加链接地址：
	
	[链接文本]:  地址   "title属性"
	[链接文本]:  地址   (title属性)
	[链接文本]:  <地址>  "title属性"
{: .prettyprint	}
	
链接的地址可以使用相对路径，链接名的定义可以任意位置。

### 图像   {#img}

图像的语法和链接的类似，只是在比链接多一`!`放在链接文本`[]`的前面：

    ![图像替代文字](图像地址 "可选的title属性")
	![图像替代文字][图像id]
{: .prettyprint }	
	
图像id的定义和链接名的定义是一样的：
    
	[图像id]: 图像地址  "可选的title属性"
{: .prettyprint}	
	
MarkDown中不能指定图像的宽、高，要想指定就要用HTML的`<img>`标签。
	
### 代码   {#code}

代码可放在一对`` ` ``之间，在代码中`&`和尖括号`<`或`>`都被解释为HTML实体。若代码中包含`` ` ``，可将代码放在一对 `` ` `` `` ` `` 中：

	`` 含有 ` 的代码 ``
{: .prettyprint }	

要使用代码块，只需将代码的每一行缩进至少4个空格或1个`tab`就可以了。 __注意：代码块其实会转成两个HTML标签:`<pre>`和`<code>`，所以代码块要用空行和周围内容分开。__

### 其它   {#other}

水平线可由三个或多个`*`或`-`放在一行来形成。`*`或`-`间可有空格。   
MarkDown中可由`\`引出转义字符，可被转义的字符有：

      \ ` * _ {} [] () # + - . !
{: .prettyprint }	  

