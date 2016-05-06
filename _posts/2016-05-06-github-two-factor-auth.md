---
layout: post
title: "开启两步验证后Github通过HTTPS提交出现授权问题"
description: ""
category: 
tags: [Github, two-factor auth, ssh, https]
---
{% include JB/setup %}

将Jekyll布署完了之后用`git push origin master`提交更改时发现类似
{% highlight http %}
Username for 'https://github.com':
Password for 'https://USERNAME@github.com':
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/USERNAME/OTHER.github.com.git/'
{% endhighlight %}
这样的问题，于是仍旧Google之，得[之](http://wikimatze.de/github-two-factor-authentication-failed-for-https)，这里说了两种方法，我比较懒，于是用了第二种方法(偷偷地说一句，主要是我原来设定过Github里的SSH key，请自动忽略此句^_^)，看[这里](https://help.github.com/articles/changing-a-remote-s-url/)，
{% highlight shell %}
git remote set-url origin git@github.com:USERNAME/OTHERREPO.git
{% endhighlight %}
之，就可通过SSH的方式来提交更改了(当然前提是Github的ssh已设定好)。
