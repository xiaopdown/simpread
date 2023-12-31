> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/351606263)

更新
--

2021 年 10 月 28 日：推翻重写，不再使用 BitShelter，改用 Kopia 来备份。不再需要单独划分磁盘，并且设置非常好理解。

警告
--

千万不要用百度网盘自动备份或者坚果云同步之类的在线同步备份软件，很可能会搞错 SuperMemo 的文件版本，导致卡片丢失或者数据损坏。

**引入**
------

SuperMemo 只有手动备份功能，使用者难免会忘记及时备份，当自己误删后想要回滚，才发现上次备份已经是几个月前，这期间的工作全部木大。为了预防这种情况出现，我建议日常使用 SuperMemo 的朋友掌握一下自动备份的方法，以防不测。

**效果预览**
--------

![](https://pic2.zhimg.com/v2-b36b2bc5e89cd944c7bcd2ef701a174d_r.jpg)

**准备工作**
--------

下载 Kopia 并安装

[https://ghproxy.com/https://github.com/kopia/kopia/releases/download/v0.9.4/KopiaUI-Setup-0.9.4.exe](https://ghproxy.com/https://github.com/kopia/kopia/releases/download/v0.9.4/KopiaUI-Setup-0.9.4.exe)

打开 Kopia 并点击 Filesystem，我们这次就做本地备份。

![](https://pic3.zhimg.com/v2-2d1677aa654bbefa15f6119faba30f3a_r.jpg)

随手找一个**空文件夹（最好新建一个）**来当备份目录：

![](https://pic4.zhimg.com/v2-692a350bd6850d5b01dfcbc08936242b_r.jpg)

设置一下备份加密密码

![](https://pic4.zhimg.com/v2-71a50f5841cb1f58712fd1fff854dba3_r.jpg)

好了，接下来就可以开始设置备份计划了

备份设置
----

点 New Snapshot，开始设置

![](https://pic1.zhimg.com/v2-33b34ca8b74364d97919d843690cc668_r.jpg)

输入你的 sm18 路径，点一下 estimate 看看对不对。

![](https://pic1.zhimg.com/v2-a79481a0dde96e02032308b46d3f54cc_r.jpg)

然后点 snapshot now 就可以手动备份了。

![](https://pic1.zhimg.com/v2-cb9df5ab04136416255db28b7bf82ec0_r.jpg)

接下来我们改一下自动备份的设置，先到 Policies 点一下 edit

![](https://pic3.zhimg.com/v2-e31ccb355d33c1c111d2a130871dbc5e_r.jpg)

retention 这里我设置为 4 3 2 1，意思就是保持最新的 4 份，最近 3 小时的 3 份，最近两天的 2 份，最近一周的 1 份。

![](https://pic3.zhimg.com/v2-7721f10395116a77fecbdec658a7e52e_r.jpg)

Scheduling 这边的 interval 设置为 300，就是 5 分钟备份一次。

![](https://pic2.zhimg.com/v2-a84104d0bbfe5031fb4a6a2833d8077d_r.jpg)

最后点击 Save Policy 完成设置。

**恭喜**
------

我们已经完成了每 5 分钟备份一次的设置。Kopia 会保留最新的 4 份备份，也就是 5 分钟前、10 分钟前、15 分钟前、20 分钟前。还有最近 3 小时，1 小时前、2 小时前、3 小时前。还有 1 天前、2 天前和一周前。有这么多兜底，妈妈再也不怕我 SuperMemo 崩溃啦！

如何恢复备份？先点击路径

![](https://pic3.zhimg.com/v2-062493b48d1f3c4624c826898bd71df6_r.jpg)

再选择一份备份

![](https://pic2.zhimg.com/v2-38979ee3db8b4895ca652ec74e8f1391_r.jpg)

然后点 restore

![](https://pic4.zhimg.com/v2-9e338b109d11d2228ce1bbaf67d3605b_r.jpg)

填一下要恢复到哪个路径（建议先把你现在的 sm18 文件夹里面的东西都删掉），然后勾选一下 overwrite 覆盖，再 begin restore 即可。

![](https://pic1.zhimg.com/v2-2dbfd3cf1d2fd5f7474d0cd368d44340_r.jpg)

补充说明
----

SuperMemo 正在运行时，Kopia 可能会备份失败，所以如果你要进行高危操作，最好先关闭 SuperMemo，然后点击 Snapshot Now 手动备份。

![](https://pic1.zhimg.com/v2-754845629238a9b1d776e6a91e611c6c_r.jpg)

另外最好将 Kopia 设置为开机自动启动。可以参考：

[愿君学习狂热：如何设置让软件开机自启动？三步搞定！](https://zhuanlan.zhihu.com/p/265076894)

拓展阅读
----

默认设置下 kopia 无法在 supermemo 运行时进行备份，需要开启影子备份，感谢

@荆慢慢 2.2

提供的教程：

[荆慢慢 2.2：KOPIA 开启影子备份以及 SUPERMEMO 18 的数据修护方法](https://zhuanlan.zhihu.com/p/524574542)