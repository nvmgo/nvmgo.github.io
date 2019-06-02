---
layout: post
title: "gitolite搭建git服务器"
description: ""
category: Tool
---

想搭建一个git服务器来玩玩，搜索了下比较喜欢两个gitlab和gitolite。gitlab更强大，但是需要较多配置，gitolite相对简单许多，但是也
够自己、几个朋友或者小团队使用了，所以先尝试下gitolite，以后再试试gitlab。

gitolite在github上的地址为 https://github.com/sitaramc/gitolite
上面有详细的安装步骤和使用说明，以下为我安装的具体步骤

操作系统为CentOS 6.3 64位, gitolite版本为 v3.6

##安装
连接服务器的终端  

	# root账户登陆服务器  
	ssh root@yourServer

	# 安装依赖软件git、perl  
	yum install git  
	yum install perl

	# 建立git用户  
	adduser git  
	passwd git  
	su git  

本机终端  

	# 如果本机没有ssh密钥对，需要先生成，~/.ssh/下的 id_rsa.pub、id_ras  
	# 生成方法为，需要三次回车  
	ssh-keygen -t rsa

	# 上传公钥到服务器git目录下  
	scp ~/.ssh/id_rsa.pub git@yourServer:~/yourName.pub  


连接服务器的终端  
 
	# 下载、安装gitolite，在git用户下操作  
	cd ~  
	git clone git://github.com/sitaramc/gitolite  
	mkdir -p ~/bin  
	gitolite/install -to ~/bin  
	bin/gitolite setup -pk yourName.pub  
  
貌似这里可能会遇到一个 类似default c的错误，如果遇到执行以下代码  

	echo "export LC_ALL=C" >> ~/.bashrc  
	source ~/.bashrc  

最后将git用户密码制空，去掉git登陆功能（也可不操作，貌似安装gitolite的过程中，做了修改，限制了登陆功能，没细研究，但是安装后就不能登陆了）

好了，安装工作全部完成

##管理  
接下来简单介绍下如何管理  
clone gitolite的管理项目  

	# 在安装时gitolite已经将你的公钥设置成管理员，并实现了ssh公钥免登陆，因此clone不需要输入密码  
	git clone git@yourServer:gitolite-admin  

添加新项目  

	# 打开conf下的gitolite.conf 在末尾追加以下代码后提交  
	repo testproject  
	RW+ = @all  
	# 然后就可以通过 git@yourServer:testproject 来访问了  


添加新用户  
 
	# 问新用户要他机器ssh的公钥id_rsa.pub，命名后放到keydir中，然后打开gitolite.conf，按照类似的格式添加到需要的项目下，然后提交即可  
	repo foss  
	RW+ = @usera  
	RW = @userb  

权限没仔细研究，需要的话详细看看gitolite的说明文档即可

