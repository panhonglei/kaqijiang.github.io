---
date: 2018-02-08 15:27:31
layout: post
title: OC混编Swift && Swift混编OC及命名空间
category: Swift
tags: Swift
keywords: OC Swift混编 ProductName ProductModuleName
description:  OC Swift混编 ProductName ProductModuleName
---

Obj-C混编Swift && Swift混编Obj-C

---

![](https://raw.githubusercontent.com/kaqijiang/kaqijiang.github.io/master/images/brdging.png)
	
#### Swift引用OC实现通过桥接头文件，OC引用Swift实现直接importProductModuleName-Swift.h

#### OC引用Swift或者Swift引用OC都需要将Defines Module选项设为YES
>TARGETS ->Build Settings -> Packaging 中 设置Defines Module为YES

第一次在Swift创建OC文件，或者第一次OC创建Swift时，xcode会提示桥接，Creat Bridging Header即可,这个文件用于Swift调用OC文件，与OC调用Swift无关。

![](https://raw.githubusercontent.com/kaqijiang/kaqijiang.github.io/master/images/bridgingheader.png)

### 手动创建桥接文件
首先介绍下这两个选项

product module name 产品模块名称

product name    产品名称 Swift中的命名空间

> 路径

> Target->Build Settings->all->packaging 
在默认情况下，product module name和工程的Product Name一样。

> 在OC中引入Swift或Swift中引入OC会自动生成ProductModuleName-Bridging-Header.h的头文件用于Swift访问OC文件

>如果修改的话切记要修改product name的话也要修改info.plist路径Info.plist.File 命名空间要与其一致


#### 在Obj-C中混编Swift
- Defines Module 设置为YES
- OC引用Swift Xcode自动式实现的桥接文件命名方式是ProductModuleName-Swift.h
- 直接在OC项目中，import ProductModuleName-Swift.h即可
- 如果单纯OC调用Swift以上即可，不需要倒入什么桥接文件。


#### 在Swift中混编Obj-C
- Defines Module 设置为YES
- Xcode在Swift中新建OC会生成ProductModuleName-Bridging-Header.h
//File > New > File > iOS > Source > Header File
- 在ProductModuleName-Bridging-Header.h桥接文件中，直接import需要引用的OC文件即可。


### 说到product Name 这里说一下命名空间
> OC中没有命名空间这一说，都是使用类前缀(Class Prefix)，当作命名空间用区分名称相同的文件，苹果规定，两字前缀苹果拥有所有权，三个字母的前缀为开发者使用。但是不冲突就没事。例如AFNetWorking NSString MBProgressHUD ···

> Swift中终于添加了命名空间，在任意类中打印一下self 会出现"命名空间.className"
> 
>注意。swift中的命名空间的使用不是一个项目,而是需要跨项目,在一个项目中,都是一个命名空间,在同一个命名空间下,所有全局变量或者函数共享,不需要import,从swift开始,官方更多的建议大家使用pod来管理第三方框架，不然倒入一个框架到处都可以用


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
```

也可以创建一个Bundle的extension

```
extension Bundle {
    //使用计算属性
    var spaceName: String {
//        return Bundle.main.infoDictionary?["CFBundleExecutable"] as? String ?? ""
        return infoDictionary?["CFBundleExecutable"] as? String ?? ""
    }
}

/**
guard let nameSpace = Bundle.main.infoDictionary!["CFBundleExecutable"] else {
    print("获取命名空间
    return
}
*/
//上边的获取命名空间就可以写成这个

guard let spaceNamee = Bundle.main.spaceName else {
    print("获取失败")
}


```