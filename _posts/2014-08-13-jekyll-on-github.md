---
layout: post
title: "Github上搭建文本博客网站"
description: ""
category: Web
---

喜欢折腾，最近折腾了下文本博客，虽然不怎么写博客，但是这种方式是自己极其喜欢的。将折腾的过程记录一下：


## 可能会用到的东东

* Jekyll 可以将纯文本转化为静态博客网站，[http://jekyllcn.com](http://jekyllcn.com)
* JekyllBootstrap 可以快速在 Github Pages 上搭建blog，[http://jekyllbootstrap.com](http://jekyllbootstrap.com)
* gem 是用于ruby程序和程序库的一套打包系统，它让开发人员可以把自己的ruby程序库打包成一种易于维护和安装的形式。
* jekyll-import 转换博客插件, [https://github.com/jekyll/jekyll-import](https://github.com/jekyll/jekyll-import)


## 部署

安装JekyllBootstrap到Github

	$ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
	$ cd USERNAME.github.com
	$ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git
	$ git push origin master

安装Jekyll

	$ gem install jekyll

运行

	$ jekyll serve

这样本地就运行起来了，下面写个hello world

	$ rake post title="Hello World"
	$ jekyll serve

发布

	$ git add .
	$ git commit -m "Add new content"
	$ git push origin master

## 换皮肤

去 [http://themes.jekyllbootstrap.com](http://themes.jekyllbootstrap.com) 这里找到合适的按照提示安装即可

也可以直接去别人的github上clone一个，注意不要删掉别人的`_post`、`images`、`CNAME`

当然，你也可以在别人的基础上做修改，东西比较少，就一点html、css，jekyll的插件的是很简单。

## 修改评论系统

老外的模版里面默认的评论系统为disqus，如果需要可以换成国内的有言、多说

这里以uyan为例

修改_config.yml

	comments :
    	provider : uyan

_includes/JB/comments-providers里面增加一个文件，命名为uyan，内容为你自己的uyan嵌入代码

	<!-- UY BEGIN -->
	<div id="uyan_frame"></div>
	<script type="text/javascript" src="http://v2.uyan.cc/code/uyan.js"></script>
	<!-- UY END -->

_includes/JB/comments下添加（加入大括号，这里不能嵌入插件标记）

	when "uyan"
		include JB/comments-providers/uyan
		
ok，重启启动看效果吧

	$ jekyll serve

## 导入Blog

按照 [http://jekyllcn.com/docs/migrations/](http://jekyllcn.com/docs/migrations/) 进行操作即可

这里实验了wordpress的导入有问题，说找不到gems，最后到jekyll-import的github主页上，看了demo改写跑通了

	require 'jekyll-import'
	importer_class = "WordpressDotCom"
	JekyllImport::Importers.const_get("WordpressDotCom").run({ :source => "wordpress.xml" })

## 绑定域名

这里只说绑定二级域名，在USERNAME.github.com的根目录下建立CNAME文件，内容为你想绑定的域名

	blog.xxxxxx.com

然后到你域名管理处，创建CNAME记录，指向到USERNAME.github.com

大功告成，等会就可以使用blog.xxxxxx.com访问了，访问USERNAME.github.com也会重定向到自己的域名
