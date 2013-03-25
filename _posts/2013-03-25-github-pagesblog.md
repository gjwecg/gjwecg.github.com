---
layout: post
title: "用github pages做blog"
description: ""
category: github 
tags: [blog]
---
{% include JB/setup %}


OS：ubuntu<br/>
首先要有个github的帐号<br/>

###一、安装###
####安装git<br/>
<p><code>
  $ sudo apt-get install git
</code></p>

####安装jekyll<br/>
<p>
  jekyll；是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。这个主要在本地做预览使用，可以不安装。
</p>
<p><code>
  $ sudo apt-get install jekyll
</code></p>

####安装Jekyll-Bootstrap<br/>
<p>Jekyll-Bootstrap在Jekyll基础上，集成了twitter-bootstrap界面风格和一些实用的插件，并且易于扩展。可选。
</p>
<p><code>
  $ git clone https://github.com/plusjade/jekyll-bootstrap.git gjwecg.github.com
</code></p>

###二、github配置
1、create a new repo，命名规则：'github帐号'+'.github.com'<br/>
2、在repo里，settings<br/>
3、Account settings 里设置SSH Keys<br/>
4、将本地gjwecg.github.com提交到github里。<br/>





