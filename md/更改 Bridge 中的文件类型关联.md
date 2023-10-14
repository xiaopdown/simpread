> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/436710348?utm_id=0)

**​关注▲边学设计边铲屎▲，一起共同进步**

![](https://pic3.zhimg.com/v2-327686c02c06709ca5b4c0f523813266_r.jpg)

在之前的教程中，我们学习了如何从 Bridge 打开图像到 Photoshop。了解到 Bridge 是一个文件浏览器。大多数时候，Bridge 会图像打开到 Photoshop 中。但是你可能会遇到这样的情况：Bridge 打开的图像不是 Photoshop，而是安装在你电脑上的其他程序。或者安装了多个版本的 Photoshop，Bridge 可能会在旧版本中打开图像。

为了解决这个问题，本节教程我们将了解如何使用 Bridge 首选项中的文件类型关联选项来解决 Bridge 在错误的程序或 Photoshop 版本中打开图像的问题。让我们看看它是如何工作的。

让我们开始吧!

从 Bridge 打开图像到 Photoshop
------------------------

在打开的 Bridge 界面中，图像的缩略图会显示在中间的【内容】面板中。

![](https://pic4.zhimg.com/v2-abe1ee5fc7d31507004d9dd89aaec2db_r.jpg)

在【内容】面板中你会发现里面有不同类型的文件，有 JPEG、PNG、TIFF、DNG 和 PSD。这些文件类型都是 Photoshop 所支持的，可以从 Bridge 打开到 Photoshop。

![](https://pic3.zhimg.com/v2-11ec9b1edd519338524fee6f07782c12_r.jpg)

正常的情况下
------

正常情况下我们想打开图像到 Photoshop 中，只需要双击图像的缩略图。

![](https://pic1.zhimg.com/v2-1da8ebcbdeceffeaa861edfd7122015c_r.jpg)

双击缩略图之后，Bridge 会将图像传送到 Photoshop 进行编辑。

![](https://pic4.zhimg.com/v2-99279dc3d0d1e965e0903b0e3627134b_r.jpg)

打开的 Photoshop 是电脑里目前安装的最新版本 2021（我还没有更新 2022），可以从界面顶部看到 Photoshop 的版本。

![](https://pic3.zhimg.com/v2-dfde20f37dcc4382b49cbc99ab64d72a_r.jpg)

出错的情况下
------

目前到 Bridge 将 JPEG 文件图像成功发送到了最新版本的 Photoshop。这个问题是有几率产生的，并不是一定会有。任何一种类型的文件都有可能出现问题。

双击 Bridge 中的 TIFF 文件缩略图，让它进入 Photoshop。

![](https://pic1.zhimg.com/v2-a8f072db53d59c8c1ed426ffaf346da0_r.jpg)

这里就发生了意外，因为电脑里还装了旧版本 Photoshop，打开的图像并不在最新的版本中。退出 Photoshop，我们开始设置 Bridge 的文件类型关联。

![](https://pic1.zhimg.com/v2-dd50da9d2dc787de8b76a9836ec09850_b.png)

设置 Bridge 的文件类型关联  

--------------------

对于打开版本出错的问题，我们需要设置 Bridge 的文件类型关联。  

**第 1 步 打开 Bridge 的首选项**  

首先我们需要进入 Bridge 的首选项。在 Windows 中，选择**【编辑】**菜单的**【首选项】**选项；在 Mac 中，选择**【Adobe Bridge】**菜单中的**【首选项】**选项。

![](https://pic4.zhimg.com/v2-88dba459a48ab8aabc33a27c5f9891bb_b.jpg)

**第 2 步 选择【文件类型关联】首选项组**

在首选项对话框中，选择左侧列表中的**【文件类型关联】**首选项组。

![](https://pic1.zhimg.com/v2-a19e7ee14ddef9a90bd6fde151be19bc_r.jpg)

**第 3 步 找到需要改变的文件类型**

在对话框右边会出现一个很长的列表，里面列出了 Bridge 可以打开的所有文件类型。在每个文件类型的右边都可以设置启动的应用程序。在这里我们可以看到 TIFF 文件是由 Photoshop 2018 打开，而 JPEG 文件则是由 2021 打开。

![](https://pic1.zhimg.com/v2-99ddd6269a005ff0f340ad18dd97900c_r.jpg)

**第 4 步 修改关联的应用程序**

单击**【Adobe Photoshop 2018】**，从列表中选择需要的版本。

![](https://pic2.zhimg.com/v2-d1181b7ca90fc71972c20b2ac7d35ef9_r.jpg)

修改后，我们单击首选项底下的**【确定】**按钮来关闭对话框。

![](https://pic1.zhimg.com/v2-6d3958651bf8bee594e0a2c84608ce0c_r.jpg)

测试一下
----

再次双击 TIFF 文件打开到 Photoshop。

![](https://pic3.zhimg.com/v2-60a2835c81caaf0f6737e4474cf65a0a_r.jpg)

现在 ITFF 文件在需要的版本中打开了。

![](https://pic1.zhimg.com/v2-15eed48db9d847604795b2179b3f2aa0_b.png)

以上就是解决问题的方法。我们这一大章的重点是如何在 Photoshop 中打开图像。但是最好不要在 Photoshop 中进行初始编辑工作，而是通过 Camera Raw 编辑。

**在下一教程中，我们将学习如何使用 Camera Raw 打开图像！**