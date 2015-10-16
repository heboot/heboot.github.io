---
layout: post
title: 在什么时候使用startService 或 bindService 或 同时使用startService 和 bindService
date: 2014-03-20
categories: blog
tags: [android,service]
description: 在什么时候使用startService 或 bindService 或 同时使用startService 和 bindService


---
###在什么时候使用startService 或 bindService 或 同时使用startService 和 bindService

如果你只是想要启动一个后台服务长期进行某项任务那么使用 startService 便可以了。
如果你想要与正在运行的 Service 取得联系，那么有两种方法，一种是使用 broadcast ，另外是使用 bindService ，前者的缺点是如果交流较为频繁，容易造成性能上的问题，并且 BroadcastReceiver 本身执行代码的时间是很短的（也许执行到一半，后面的代码便不会执行），而后者则没有这些问题，因此我们肯定选择使用 bindService（这个时候你便同时在使用 startService 和 bindService 了，这在 Activity 中更新 Service 的某些运行状态是相当有用的）。另外如果你的服务只是公开一个远程接口，供连接上的客服端（android 的 Service 是C/S架构）远程调用执行方法。这个时候你可以不让服务一开始就运行，而只用 bindService ，这样在第一次 bindService 的时候才会创建服务的实例运行它，这会节约很多系统资源，特别是如果你的服务是Remote Service，那么该效果会越明显（当然在 Service 创建的时候会花去一定时间，你应当注意到这点）。
