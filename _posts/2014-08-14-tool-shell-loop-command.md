---
layout: post
title: 开发助手 - shell循环命令
description: ""
category: Tool
---

开发中经常需要写一些脚本辅助开发，脚本多了，使用频率高了，不容易记忆，执行起来也繁琐。就想起来弄一个总的命令来简化操作。

主要是想解决两点问题

* 帮助记忆：采用命令列表，并增加注释的方式来解决
* 简化命令：采用输入简短单词来执行命令，并实现循环执行，简化每次输入

按照上面的思路写了一个脚本，保存为easy.sh，打开一个终端，执行`./easy.sh`后放在屏幕的一个角落，需要的时候输入命令即可。

	#!/bin/bash

	while true;
	do
		# 之所以不用select是为了提高命令选择的准确性
		echo "========================="
		echo -e "asset	: 导出素材"
		echo -e "config	: 导出配置"
		echo -e "app	: 打包APP"
		echo "========================="
		echo -ne "选择要执行的命令: "
		read selectedId
		echo ""
		if [ "$selectedId" == "asset" ]; then
			echo "run commond: create asset"
			echo "这里要替换为真正要执行的脚本文件"
			for (( i=0; i<100; i+=10 ));
			do
			  echo "$i"
			done
			echo "done!"
		elif [ "$selectedId" == "config" ]; then
			echo "run commond: create config"
			echo "这里要替换为真正要执行的脚本文件"
			for (( i=0; i<100; i+=10 ));
			do
			  echo "$i"
			done
			echo "done!"
		elif [ "$selectedId" == "app" ]; then
			echo "run commond: create app"
			echo "这里要替换为真正要执行的脚本文件"
			for (( i=0; i<100; i+=10 ));
			do
			  echo "$i"
			done
			echo "done!"
		else
			echo "输入的命令还没出生或者死了"
		fi
		echo ""
	done