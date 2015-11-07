---
layout: post
title: TextView——setCompoundDrawables用法
date: 2014-05-20
categories: blog
tags: [android]
description: TextView——setCompoundDrawables用法/无效/不显示


---
###TextView——setCompoundDrawables用法/无效/不显示

TextView——setCompoundDrawables用法

Drawable drawable = mContext.getResources().getDrawable(R.drawable.duringtime);

drawable.setBounds(0, 0, drawable.getMinimumWidth(), drawable.getMinimumHeight());//必须设置图片大小，否则不显示

holder.time.setCompoundDrawables(drawable, null, null, null); hehe