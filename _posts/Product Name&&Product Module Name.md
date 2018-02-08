---
date: 2015-02-25 15:27:31
layout: post
title: ProductName&&ProductModuleName
category: iOS
tags: iOS
keywords: ProductName ProductModuleName
description:  产品名称，产品模块名称
---


product module name 产品模块名称

product name    产品名称

--
> 路径

> Target->Build Settings->all->packaging 
在默认情况下，product module name和工程的Product Name一样。

> 在OC中引入Swift会自动生成ProductModuleName-Bridging-Header.h的头文件用于混编

>如果修改的话切记要修改product name的话也要修改info.plist路径Info.plist.File