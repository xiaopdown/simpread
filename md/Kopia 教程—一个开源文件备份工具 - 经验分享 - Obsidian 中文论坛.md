> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [forum-zh.obsidian.md](https://forum-zh.obsidian.md/t/topic/3944/20) ![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

Kopia 是开源文件备份恢复工具，可以为本地任意数量文件夹建立快照，可以保存文件夹不同时刻的状态（每小时、每天或自定义时间保存快照）。该软件有安全、快速、低资源占用的特点。开源软件且采用高强度加密，保证了数据安全。算法合理，占用资源很少，可常驻后台无感知运行。对文件采用分块保存技术，相同块会共用，极大减小数据库占用空间（保存多个快照的数据库有可能比源文件夹占用空间小）。目前中文教程较少，因此随便写一下我安装方法与使用的经验。（220123_132240）

相关中文文章 ：

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/c/7cd45c/40.png) [使用 Kopia 来备份 obsidian](https://forum-zh.obsidian.md/t/topic/3929) [经验分享](/c/8-category/8)

> 今天发现可以参考叶峻峣的文章 “SuperMemo 自动备份”， （ [SuperMemo 自动备份 - 知乎](https://zhuanlan.zhihu.com/p/351606263) ），使用 Kopia 给 ob 做自动备份。 因为叶峻峣在文中已经叙述清楚，本文不再细说。 Kopia： [https://kopia.io/](https://kopia.io/) 或 [GitHub - kopia/kopia: Cross-platform backup tool for Windows, macOS & Linu…](https://github.com/kopia/kopia)

[SuperMemo 自动备份 - 知乎 (zhihu.com) 55](https://zhuanlan.zhihu.com/p/351606263)

### 为什么要保留文件夹快照

我使用本软件的目的是记录文件夹状态，在必要的时候恢复文件夹为某时刻状态。我曾经几次特别需要此类软件，一次是 Mendeley(一个论文管理软件)bug，把我的所有文献全改成了相同的名字（后面加序号）。一次是我自己写程序 bug，把文件夹内改了部分软件，我自己也不知道改了哪些。还有一次是被小孩拿去玩，搞的乱七八糟。没有此类软件，会头疼无比，如果保留了快照，那就可以轻松的恢复任意正常的状态了。除了我遇到的情况，前几年勒索病毒时，如果受害有类似工具，可以把文件夹还原回原来的时刻，情况会好很多。保留快照是保障数据安全很有效的一个办法。

### Kopia 的特点

除了 Kopia 之外，还有很多工具可以保存快照。比如 seafile 网盘、苹果 os 的时光机器、windows 的快照，git 的 LFS。seafile 网盘大部分人用不了，苹果听说不错，但只有 os 有。windows 的快照占用空间过大，git 的 LFS 无法很好处理大文件，空间占用也极大。

Kopia 开源免费，各平台都可使用，自定义能力很强，占用计算资源、存储资源均很小，目前看满分。

### 下文内容

二楼，软件下载安装、库的建立、文件夹快照的建立。

三楼，历史版本查看与文件历史版本下载，历史快照挂载到文件管理器，历史版本恢复，**比对两个快照文件变化**。

四楼，以问答形式总结其它问题。

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

### Kopia 安装与新建库

Kopia 有两种安装方式，一个是无界面，一个是有界面，大部分人建议安装有界面的版本。Kopia 的库地址为 [Releases · kopia/kopia · GitHub 197](https://github.com/kopia/kopia/releases)，下载的时候找带 UI 字样的，如下图。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/9/9e23ac791f47487492cb79a0da3a9186d05b36fb_2_500x331.png)

正常安装，过程略~

打开之后长这样

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/2/2dc5102a7003f57c9de7279867f8792fdcf0822d_2_500x331.png)

这是让选择库的位置，可以选择本地 (Filesystem)、谷歌 (Google colud storage)，Amazon S3 等云存储、SFTP、WebDAV 等。我选择的是存在本地，点击 filesystem。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/7/784dc26f1e9201ae70daa8894a7bdf723fdbd286_2_500x331.png)

选择一个存放库的文件夹，对位置没有要求。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/3/398745805b7531f2d4044ad8263191e522c1a42a_2_500x331.png)

然后点 Next.

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/e/ed6099cb1ddbad4b4e4774379f035fd52f8a5103_2_500x331.png)

输入密码，确认密码，点 Create Repository。这里密码要记牢，忘了无法找回。

至此，库已经建立完成。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/a/ad9f686e468e485f9290e4d3c91cd98387324bef_2_500x331.png)

### 添加要建立快照的文件夹

建立库后，啥也没有，需要指定要为哪些文件夹建立快照，这样才能保存这些文件夹的历史记录。

①点击 New Snapshot

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/1/157cb6e59f54395282ba5c22925378ad8f77e076_2_500x331.png)

②选择文件夹，此处可输入，也可直接用图形界面。检查文件夹是否正确。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/0/0379f4b08275c1accd10328b8d1089bcfc7cca8c_2_500x331.png)

③选择快照间隔，之后点击 Snapshot Now(选择文件后面那个绿色按钮)。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/6/6642ddde10e30cd6c7d3aac4b08b263d7b4cf09e_2_500x331.png)

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/d/d88430e267e3edb2a739764acff9aabb10c293e7_2_500x331.png)

④等待完成，新建同步文件夹结束。可以把软件关掉了，让它在后台运行即可。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/1/130d2e47b0941150672e432c9abe94796e8d4a35_2_500x331.png)

完成长这样：

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/3/37fd349b5a7408650423c570120d5a3722169406_2_500x331.png)

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

### 历史版本查看

很多时候只需要查看某个文件 / 夹的某个历史版本，此时用历史版本查看即可。

①点击要查看的快照。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/1/1cd6854ed57dfcf2ba2be8aad32fb1a698cf0c68_2_500x331.png)

②会显示所有的快照，其中第一列是快照时间，点击想要查看的时间。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/7/76a36976407122ca2b65eea79c678a6e39c656d1_2_500x331.png)

③之后就要是一个文件浏览器，可以查看那个时刻的文件夹状态，并可以下载下来想要的文件。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/e/ed90716f419be4451d518b952987349e4cd83786_2_500x331.png)

### 将某个历史版本像 U 盘一样挂载

为了更方便的查看过去某个时刻的文件夹，可以把那个时刻的文件夹像 U 盘一样挂载到系统上，例如 Z 盘。

①接上一项第 3 步，点击 Mount.

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/3/32f2f453caa8d9790748f99b002f2c291c7e32e1_2_500x331.png)

②点击 Browse 即可以浏览

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/f/fd63955686602e9071fd90d4444aa3ea57ce7680_2_500x331.png)

下图为 win 文件管理器中快照文件，可以像操作 U 盘一样操作。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/f/f0bca6c67840105ba34dce2f5c151bddae683c5c_2_603x500.jpeg)

查看之后点击上上图中的 Unmount 即可，相当于拔出 U 盘。

_此外，还可以只挂载特定的子文件夹。_

### 库、子文件夹的恢复 / 回滚

如果库或某个文件夹乱了，想要恢复某个时刻的样子，可以使用恢复 / 回滚。接上上图，点击 restore，之后选择位置即可。（我还没试，先留着）

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/3/31820406c68fef267835615625c741edd73d2edf_2_500x331.png)

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/8/80ca2f9f5fe4fb980a3e3f7eecd393491ff880ba_2_500x331.png)

### 快照对比

有时我们想知道两个快照之间修改了哪些文件，这个时候可以用快照对比。

从此位置开始~

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/4/4941c7120482e3ed89e2af3c2865886b09406daf_2_500x331.png)

可以看到我们有三个快照，我想知道最新的快照和最老的快照之间，我修改了哪些文件。

①点击下图黄色图标，后面会出来一堆很难看的命令，复制前半截，到 exe 为止。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/d/d8845843b292d30a9e0012df27a704e34e91a526_2_500x331.png)

`C:\Users\vkss\AppData\Local\Programs\KopiaUI\resources\server\kopia.exe`

②复制要比较的两个快照的 root，就那串乱码。

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/0/0b5a335343a51a2439c36323735f442c6c193805_2_500x331.png)

③第①步的命令，diff , 两个快递 root，拼装在一块，用空格分开。

组装结果为，`C:\Users\vkss\AppData\Local\Programs\KopiaUI\resources\server\kopia.exe diff k164bb1ee8b40cbf40368cc40e19fe3eb k6f4534223bb087a5e14f6bf983e6b97b`

④在 powershell 或 cmd 窗口粘贴上述命令，按回车即可。

 [![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/4/42c4a8d663bbdbc27fd7e4b9eb5e848819132bf6_2_300x150.png) image799×420 18.7 KB](https://forum-zh.obsidian.md/uploads/default/original/2X/4/42c4a8d663bbdbc27fd7e4b9eb5e848819132bf6.png "image")

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/9/9f9d987657b42eecb98d5bd2d254c37a6f69255b_2_600x270.png)

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/2/2231b6adfc1e2e18aaec4173fd47b23ad8217d27_2_500x468.png)

会展示哪些文件夹与文件有修改。文件

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

以问答形式讨论几个问题。

Q：库文件夹能否在其它设备上打开？

可以打开。可以通过网盘将库传递给远方电脑，电脑爆炸后，硬盘如果没坏，也能恢复库文件。库文件夹包含快照的所有数据。

Q：只能建立一个库么？

可以建立多个库，每个库对应上个库文件夹，对于不同的文件夹，分开放有利于备份。

Q：一个库只能为一个文件夹建议快照么？

一个库可以为多个文件夹建立快照，每个文件夹可以有多个快照。在同一个库里建立的所有文件夹的所有快照，文件都在库文件夹中。

Q：Kopia 安全性如何？密码丢了怎么办？

Kopia 安全性我认为还行。从实现逻辑上看，数据是高强度加密的，如果密码强度足够高（10 位以上简单密码或 8 位以上复杂密码），目前无破解可能。Kopia 密码丢失库无法打开，只能删掉。

Q：保留版本数怎么设置？

以后再写~

Q：以后再补充

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

5 楼我先占上，慢慢写。这里讨论没啥用的 Kopia 算法、加密、压缩等底层问题。

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

6 楼我也占上，慢慢写，差不多够用了。这里仅占坑

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/r/51bf81/96.png)正需要这个功能。多谢。多谢。 ![](https://forum-zh.obsidian.md/images/emoji/twitter/grin.png?v=12) ![](https://forum-zh.obsidian.md/images/emoji/twitter/grin.png?v=12) ![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/autumn_1992/96/837_2.png)

谢谢推荐，我之前一直在用 Duplicati，也不错。今天试用了下 Kopia，感觉各有千秋。Kopia 对于备份文件的可视化展示、虚拟磁盘挂载功能，非常赞！

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/lyon/96/4968_2.png)

老哥，kopia 怎么连 sftp 呀？我在 windows 文件浏览器添加网络位置成功连上了 ftp，kopia 这个不知道怎么填 host file 什么的  

![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/f/f3986cb0efb75660474cc44b8e5707d97bedc9a8_2_690x445.png)

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

我没使用网络存储，建议看看官方文档。

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/carrrrot/96/3716_2.png)

感谢，一直为备份苦恼，现在多了一项不错的选择

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/h/ee7513/96.png)

感谢楼主分享！请问有没有方法可以将 Kopia 的备份和版本控制的优势和 syncthing 的多端同步的优势结合起来呢。

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

kopia 的库直接用 syncthing 同步到其它设备就可以了

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/shaosen/96/88_2.png)

不过为了安全，我倾向于 syncthing 同步原文件，各地分别用 kopia 保存快照。

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/一叶知秋/96/536_2.png)

好东西啊，还可以用来备份其他东西。感谢分享

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/a/22d042/96.png)

请问下，CLI 的配置文件可以放在程序所在目录吗？  
GUI 是不是不支持 Win7 了？

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/2/ee7513/96.png)

你可以下载 gui 版本，里面就包含了 cli 程序（server 文件夹里）。配置后就会在目录下生成配置文件，这个文件就可以给 cli 用

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/a/22d042/96.png)谢谢，问题是 GUI 不支持 Win7 ![](https://forum-zh.obsidian.md/images/emoji/twitter/rofl.png?v=12) ![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/2/ee7513/96.png)

没有系统来测试，不过官方文档是写支持 win7 的，真的不行就应该去 github 问问作者了

![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/却能火里种金莲/96/9612_2.png)

感谢 Shaosen 的分享