---
layout: post
title: 查看无root权限Android手机的app数据库
date: 2015-11-09
categories: blog
tags: [android]
description:  查看无root权限Android手机的app数据库


---
### 查看无root权限Android手机的app数据库

为了定位bug的位置，测试人员经常要自己查询数据库，方法其实很简单。

1、在电脑上安装ADB和手机驱动

2、在命令行中运行adb shell

3、执行如下命令：

     cd data/data

     run-as com.package   ‘’‘com.package是你的app的包名，这地方ls命令权限受限，无法真正看到文件名'''

     ls    ‘’‘查看com.package下面是否就是app放置databases的地方’‘’

     cd databases

     dd if=**.db of=/mnt/sdcard/**.db       '''前一个**.db是要导出的数据库文件，后一个可以自由命名，放在sdcard下面是为了第4步的复制’‘’

4、然后就可以通过91助手之类的工具直接将mnt/sdcard/目录下的db文件下载到电脑上了。

5、在电脑上的db文件可以用SQLite Expert之类的工具打开。

So easy(*^__^*) 嘻嘻……

【备注】升级到Android4.1.1之后，发现sdcard不在/nmt目录下，因此“of”之后的目录要随之改变。


=================


还有更简单的方法：

1、在电脑上安装ADB和手机驱动

2、在命令行中运行adb shell am broadcast -a com.package.copydb

'''com.package是你的app的包名，通过这个命令，数据库会直接被复制到sdcard目录下‘’‘
