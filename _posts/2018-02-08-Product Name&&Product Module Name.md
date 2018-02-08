---
date: 2018-02-08 15:27:31
layout: post
title: ProductName&&ProductModuleName
category: Swift
tags: Swift
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

swift获取product Name

根据类名转换成类的时候需要用到 product name + . + classStringName 也就是命名空间。

在这里需要说一下，OC Swift的命名空间的问题，别的语言都有命名空间这个概念唯独，OC Swift只有一个命名空间，就是它的Product Name

```
//这个key 在info.plist中source code打开即可看到。
//获取命名空间
guard let nameSpace = Bundle.main.infoDictionary!["CFBundleExecutable"] else {
    print("获取命名空间
    return
}
//根据类字符串转换
guard let VcClass = NSClassFromString("\(nameSpace).\(vcName)") else {
    print("转换失败")
    return
}
//类型转换
guard let viewController = VcClass as? UIViewController.Type else {
    print("类型转换失败")
    return
}
