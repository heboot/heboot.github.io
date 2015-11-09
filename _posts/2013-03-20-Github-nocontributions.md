---
layout: post
title: contributions不显示在github上
date: 2014-03-20
categories: blog
tags: [github]
description: github提交不显示绿点


---
###contributions不显示在github上

最近不知道怎么搞的,提交了茫茫多次到github上,但在github账号页面不显示contributions绿点.自己的努力没有显示出来,十分的不爽.
尝试各种方法解决,最后发现是.gitconfig不知道被哪个软件修改了,应该是安装了sourceTree被删掉了.gitconfig配置文件.
再终端重新建立一个就行了:
1.  git config --global user.name "你的名字"
2.  git config --global user.email "your_email@youremail.com"

