一、Charles基本工作原理
charles是通过网络代理来进行抓包的，下面先了解一下http代理的原理：

1.普通http请求过程

•一般情况下的HTTP请求与响应：

2.加入了Charles的HTTP代理的请求与响应过程

中间的代理服务器就是Charles

二、Charles的下载与安装过程
官网下载地址：http://www.charlesproxy.com/download/

三、Http抓包操作步骤
> 1：开启Charleshttp代理；
> 
> 2：手机端Wifi添加代理；

> 3：开启Charles录制功能；

> 4：启动应用开始抓包；

> 5：分析抓取的数据包。

Step 1: 开启Charleshttp代理
![第一次启动默认会开启本机的系统代理，因为我们只是监控移动端的所以将此选去除（去掉选项前面的小钩）](https://upload-images.jianshu.io/upload_images/2327528-91a2016d1ca23038.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/472)
第一次启动默认会开启本机的系统代理，因为我们只是监控移动端的所以将此选去除（去掉选项前面的小钩）

![](https://upload-images.jianshu.io/upload_images/2327528-faa0da5558647eaf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/583)
设置端口。80/8888/*/443



Step 2: 手机端Wifi添加代理 设置手机为手动。
注意：手机所连接Wifi要与电脑在同一个LAN(局域网)。

Step 3:开启Charles录制功能
![1.当手机连接上代理后Charles会弹出相应的提示框，点击Allow即可。2.点击工具栏上的开始录制按钮，即启动了Charles的抓包功能了。](https://upload-images.jianshu.io/upload_images/2327528-fb506210dc91714b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/410)

Step 5：分析抓取的数据包

四、视图

1.Charles 主要提供两种查看封包的视图，分别名为 “Structure”和 “Sequence”：

    a.Structure 视图将网络请求按访问的域名分类；

    b.Sequence 视图将网络请求按访问的时间排序。


六、Https抓包操作步骤
Step 1：了解一下https的基本原理；

Step 2：在手机端安装SSL证书；

Step 3：激活Charles的SSL代理；

Step 4：将指定的URL请求开启SSL代理功能

Step 5：其他步骤与Http抓包相同，请参考四、Http抓包操作步骤

Step 1：了解一下https的基本原理；
![](https://upload-images.jianshu.io/upload_images/2327528-846818e091a616cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/691)

HTTPS其实是有两部分组成：HTTP+ SSL / TLS，也就是在HTTP上又加了一层处理加密信息的模块。服务端和客户端的信息传输都会通过TLS进行加密，所以传输的数据都是加密后的数据。具体是如何进行加密，解密，验证的，且看图,下面这个图的解说
详细说明，请参考：

http://blog.csdn.net/clh604/article/details/22179907

Step 2：在手机端安装SSL证书

        1.将证书文件从Charles导出

        2.然后通过adb或者其他工具将其复制到手机的SD卡中。
        ![](https://upload-images.jianshu.io/upload_images/2327528-e047ba31fd769693.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/577)

从Charles导出证书文件

3.将证书文件导入Android手机

![](https://upload-images.jianshu.io/upload_images/2327528-adb197fcbcc3afec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/433)

在手机的设置界面找到【安全】---》【从内部存储设备或SD卡安装】----》选择SD卡上的证书---》弹出设置证书名对话框，输入一个易记的名字，然后根据提示进行导入即呵。

4.将证书文件导入iOS手机

1.在iPhone手机上打开Safari浏览器，然后在地址栏中输入www.charlesproxy.com/getssl。

2.稍后会弹出安装描述文件提示，点击右上角的【安装】按钮进行证书安装即可。

Step 3：激活Charles的SSL代理
![](https://upload-images.jianshu.io/upload_images/2327528-d69cf0feddcb0445.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/583)

1.选择【Proxy】--->【SSL Proxying Settings..】设置。

2.在弹出来的对话框中沟选【Enable SSL Proxying】。

Step 4：将指定的URL请求开启SSL代理功能


1.选择抓取的https链接，然后右键选择【Enable SSL Proxying】。2.如果不激活SSL代理，所以https请求都是乱码无法查看。


再次请求这个Https时，其请求内容已经一目了然了。
七、Charles进阶---修改请求也响应的内容
Step 1：设置Charless断点。

Step 2：对指定的URL开启断点功能。

Step 3：编辑请求与响应的内容。

Step 1：设置Charless断点


选择【Breakpoint Settings…】--->勾选【Enable Breakpoints】来激活断点功能
Step 2：对指定的URL开启断点功能。
1.选择一个URL链接-à右键开启菜单---》选择【Breakpoints】即可开启此请求的断点。2.这样Charles会遇到此请求时会弹出中断对话框。
Step 3：编辑请求与响应的内容。
a.编辑请求内容

在中断对话框中，用户可以点击Edit Request来编辑请求的内容，编辑完成后然后点击【Execute】发出去这个请求给服务端
b.编辑服务器响应的内容

在【Edit Request】对话中点击【Execute】发出请求后，服务端返回来数据后，用户点击【Edit Response】可对响应内容进行编辑完成后然后点击【Execute】发出去这个数据给客户端。
八、Charles进阶---弱网模拟
1.菜单中选择【Proxy】--->【Throttle Settings..】-à激活【Enable Throttling】。

2.在Throttle Configuration设置弱网的参数。

3.以下是各种网制式的速率参考文档：

移动网络制式与网速的参考文档



弱网模拟设置

作者：luckydaxian
链接：https://www.jianshu.com/p/68684780c1b0
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。