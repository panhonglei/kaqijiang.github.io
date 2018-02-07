---
date: 2018-02-07 11:27:31
layout: post
title: SublimeText3安装、及插件配置
category: Mac工具
tags: Mac工具
keywords: SublimeText3安装 SublimeText3插件
description: Snippet SublimeText3
---

### 介绍

这是官网的一个介绍

A sophisticated text editor for code, markup and prose

对我来说，它就是一个简单、轻量、方便的编译器。用习惯了SublimeText，再去用xcode相信你，会吐血的。

### 下载
[官方下载地址](http://www.sublimetext.com/3)

### 安装
下载后，根据步骤安装到Mac应用程序中即可

### 激活
>
>如果可以，请尽可能支持正版软件。<br>
>如果可以，请尽可能支持正版软件。<br>
>如果可以，请尽可能支持正版软件。<br>
>

如果你是学生，没有资金购买正版，可以尝试一下方法。

打开Sublime菜单 > help > enter License,可尝试一下两个，如果不行失效，[请点击这里](https://www.baidu.com/s?wd=SublimeText3%20LICENSE&rsv_spt=1&rsv_iqid=0xe1ef6d110007686a&issp=1&f=8&rsv_bp=1&rsv_idx=2&ie=utf-8&rqlang=cn&tn=baiduhome_pg&rsv_enter=1&inputT=12265&rsv_t=ac416mDRQGAJgvV0gG9uMW2DtxVfSiiPyCVdXjPRGG8i%2FyiSz3ahfwWRAIurZDdIN3dX&oq=sublime%2520text%2520%2526lt%253B%2520LI%2526lt%253B%2526gt%253BNS%2526gt%253B&rsv_pq=ec58b56900071c8f&rsv_sug2=0&rsv_sug4=12266)
```
—– BEGIN LICENSE —–
TwitterInc
200 User License
EA7E-890007
1D77F72E 390CDD93 4DCBA022 FAF60790
61AA12C0 A37081C5 D0316412 4584D136
94D7F7D4 95BC8C1C 527DA828 560BB037
D1EDDD8C AE7B379F 50C9D69D B35179EF
2FE898C4 8E4277A8 555CE714 E1FB0E43
D5D52613 C3D12E98 BC49967F 7652EED2
9D2D2E61 67610860 6D338B72 5CF95C69
E36B85CC 84991F19 7575D828 470A92AB
—— END LICENSE ——

—– BEGIN LICENSE —–
Michael Barnes
Single User License
EA7E-821385
8A353C41 872A0D5C DF9B2950 AFF6F667
C458EA6D 8EA3C286 98D1D650 131A97AB
AA919AEC EF20E143 B361B1E7 4C8B7F04
B085E65E 2F5F5360 8489D422 FB8FC1AA
93F6323C FD7F7544 3F39C318 D95E6480
FCCC7561 8A4A1741 68FA4223 ADCEDE07
200C25BE DBBC4855 C4CFB774 C5EC138C
0FEC1CEF D9DCECEC D3A5DAD1 01316C36
—— END LICENSE ——
```

### packect control安装
- 插件安装方式一：直接安装：

    安装Sublime text 3插件很方便，可以直接下载安装包解压缩到Packages目录（菜单->preferences->packages）。

- 插件安装方式二：使用Package Control组件安装：

     1.按`` CTRL+` ``或者View - Showconsole调出console

    2.粘贴以下代码到底部命令行并回车：

    ```
    import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
    ```
    如果失效，请移步[这里](https://packagecontrol.io/installation#st3)用最新的。

    3.重启Sublime Text 3

    如果在**Perferences->package settings**中看到**package control**这一项，则安装成功。
    
### 通过packect control命令
packect control安装完成后，按下`Ctrl+Shift+P`调出命令面板

![](http://javen-blog-image.oss-cn-shenzhen.aliyuncs.com/control_package.png)

输入`Install Package`，然后在列表中选中要安装的插件。

其他一些常用

`list package` 查看已安装的插件

`enable package` 启用已安装的插件

`enable package`  禁用已安装的插件

`upgrade package` 升级已安装的插件

`remove package` 移除已安装的插件

其他更多的命令可以自己在命令面板查看


### 安装其他常用软件
- [20 个强大的 Sublime Text 插件](http://www.open-open.com/news/view/26d731)
- [Sublime插件：增强篇](https://www.jianshu.com/p/5905f927d01b)
- SublimeLinter
- Emmet
- MarkdownEditing
- MarkdownLivePreview
- ColorPicker
- SideBarEnhancements
- sublime-text-git
- TrailingSpaces
- SyncedSideBar
- [更多查看这里](https://jeffjade.com/2015/12/15/2015-04-17-toss-sublime-text/?jianshu)

### 代码块或者固定头

##### 使用Jekyll部署博客后需要每次填写固定的头部信息，比如
```
---
date: 2018-02-07 11:27:31
layout: post
title: Sublime Text3 代码块、固定头设置
category: Mac工具
tags: Mac工具
keywords: 
description: 描述
---
```
##### 或者你想在代码中加入你自己的信息，比如
```
/**
 4  * ============================
 5  * @Author:   xx
 6  * @Version:  xx 
 7  * @DateTime: xx
 8  * ============================
 9  */
```

##### SublimeText3 为例子，新建一个代码块

Tools -> developer -> New Snippet

```
<snippet>
    <content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <!-- <tabTrigger>hello</tabTrigger> -->
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <!-- <scope>source.python</scope> -->
</snippet>
```
##### 此时的你应该有点莫名，我们接着来看下完整的结构和说明：
```
<snippet>
    <content><![CDATA[ 你需要插入的代码片段${1:name} ]]></content>
    <!-- 可选：快捷键，利用Tab自动补全代码的功能 -->
    <tabTrigger>xyzzy</tabTrigger>
    <!-- 可选：使用范围，不填写代表对所有文件有效。附：source.css和test.html分别对应不同文件。 -->
    <scope>source.python</scope>
    <!-- 可选：在snippet菜单中的显示说明（支持中文）。如果不定义，菜单则显示当前文件的文件名。 -->
    <description>My Fancy Snippet</description>
</snippet>
```
##### 这是我根据结构来配置自己的。
```
<snippet>
    <content><![CDATA[
---
date: 2015-02-25 15:27:31
layout: post
title: 标题
category: iOS Swift Python Mac工具 about
tags: about
keywords: 关键字
description: 描述
---


]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <tabTrigger>blog</tabTrigger>
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <!-- <scope>source.python</scope> -->
</snippet>
```

然后保存到

Sublime Text-Preferences-Browse Packages-user-weappSnippet文件夹下

命名为xxx.sublime-snippet

重启

cmd + shift + p 输入自己设定的快捷键就可以了。

![image.png](https://raw.githubusercontent.com/kaqijiang/kaqijiang.github.io/master/images/Snip20180207_1.png)

### 更换图标
接下来做一些个性化的事情，[选择一个自己喜欢的图标](https://dribbble.com/)。

找到应用程序中的Sublime

Text右击显示简介，把下载下来的icns文件
![image.png](https://raw.githubusercontent.com/kaqijiang/kaqijiang.github.io/master/images/Snip20180207_2.png)