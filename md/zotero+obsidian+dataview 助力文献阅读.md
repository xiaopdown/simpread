> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [mp.weixin.qq.com](https://mp.weixin.qq.com/s?__biz=Mzg5Njk3MDUyMQ==&mid=2247487410&idx=1&sn=087665f876e3accf69707feefe0828b5&source=41&poc_token=HJwVP2WjnDG1I_JygbxxDRbJaiNZiHPpn0wZ_GF-)

大家好，我是 BCS！

> 很早之前，分享了一篇 zotero 与 obsidian 联用的一个教程，但现在随着需求的增加，不得不更新了！

1 工作流简介
-------

关于我的文献阅读工作流，之前或多或少都提到了一些

👉 [Obsidian 模板插件有此一个足矣！](http://mp.weixin.qq.com/s?__biz=MzU4MzgxNjczMA==&mid=2247485198&idx=1&sn=1d14bed020377bc7c7f04d9c589c31a0&chksm=fda2047bcad58d6d19790e53c14da2d559b5fd6355a85cdf6fe32734d61fbbaea6f8ecdf8f83&scene=21#wechat_redirect)

👉[给 Obsidian 新手科研人的开箱即用库：BCS's Vault for Researchers V1.0](http://mp.weixin.qq.com/s?__biz=MzU4MzgxNjczMA==&mid=2247485402&idx=1&sn=6359f02137e7383693988a5f69288f21&chksm=fda204afcad58db97792ec968c60f076062bdb6bec3b588d81d4db4120faa8334f08767ae9e6&scene=21#wechat_redirect)

这次根据需要，又做了一些更新，部分流程参考了英文论坛的这个帖子 [1]~

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBXYBzJPqtcbpzlGBjSncrQibR3dFnWnRB7Z6EVcTYySibntvxcdWUiaQRQ/640?wx_fmt=png)

*   在 Google/CNKI/wof 等学术网站检索文献
    
*   利用 zotero connector 插件保存文献到 zotero library
    
*   文献阅读
    

*   建议在阅读之前，可先利用 mdnotes 插件生成文献模板笔记到 Obsidian
    
*   利用 zotero 内置的 PDF 阅读器也可使用第三方阅读器（推荐 PDF exchange editor）
    
*   边阅读边在 obsidian 中积累笔记和写作素材，通过设置好的快捷方式一键添加文献阅读随想和专业知识元笔记
    

*   新建一个文献阅读笔记汇总页，利用 dataview 将文献笔记和文献阅读随想汇总展示（可根据需要补充 / 修改笔记内容（这里主要利用悬浮编辑）& 回顾笔记 & 知识串联.......）
    

下图就是一个 Reading Notes 的汇总预览图，就类似于 Notion 中的数据库

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBNbTRNbuHfu9iad3ZZw9ov0H0Bykhomm1s48jSxHwDFEFnAHG1SghApA/640?wx_fmt=png)

一键随想（文献阅读随想）和补充新知（专业知识笔记）的演示，请看此推文👉  

[为 BCS's Vault for Researchers 开箱即用库加入了更便捷的思考环节和专业知识归纳环节](http://mp.weixin.qq.com/s?__biz=MzU4MzgxNjczMA==&mid=2247485442&idx=1&sn=430ed9aa5af99c759cee0eb2af0227b1&chksm=fda20b77cad582612ad2d9395f0882a454d1393b2a0550f69ee4bd7a85b383b221fd68824f9f&scene=21#wechat_redirect)

大致的流程就是这么多~

2 配置教程
------

对于文献检索与导入 zotero 的过程我就不再介绍了，研究生生存基本技能~

### 2.1 Mdnoteos 与 zotero 联用

这一部分之前也有介绍，貌似之前的前程略微繁琐，这次整个更简单的

👉[Zotero 与 Obsidian 交互 助力科研](http://mp.weixin.qq.com/s?__biz=MzU4MzgxNjczMA==&mid=2247484524&idx=1&sn=86176978f0401c48c78b97158421413b&chksm=fda20719cad58e0f0f9c045611a23bea4d981a8026931dfc675d013ee6789db3843900f44a4e&scene=21#wechat_redirect)  

#### 2.1.1 Mdnotes 和 Better Bibtex 插件安装

可在文末获取这俩插件，然后依次点击 zotero---Tools---Add-ons，即可弹出如下界面

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTByVJ7MkXcTUPc3FSIUXEib9ztKK7NNSbTTm8Akat9K1FPew0LQkavyWg/640?wx_fmt=png)

此刻你只需要将 mdnotes 和 better bibtex 插件拖入此界面，即可完成安装

> 对于 Better bibtex 插件，是否安装，主要看你自己需求，如果你使用 Latex 写论文的话还是很有必要安装的；如果只使用 word，那大可不必安装。

#### 2.1.2 配置 Mdnotes 占位符

为了能够利用 dataview 汇总文献笔记，我们需要在 zotero 中利用占位符对字段格式进行自定义，也就是能够让 dataview 识别到。这个在 mdnotes 说明文档 [2] 里也有详细说明。

dataview 能识别 Yaml 区内的字段，且字段后只需要跟一个冒号和一个空格；当然对此文献笔记占位符，我更推荐使用字段 + 双冒号 + 一个空格这种方式，emmm，对于 dataview 的基础知识，请自行了解，网上太多了，本推文不做介绍。

下面咱们就来更改 zotero 中 mdnotes 字段的占位符

*   依次点击 edit---preference---Advanced---General---config editor
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTB4QNGalpQGVZNgGWokx6pPSYib5HbSqafjEScYQ1aH5RCGTicTuV6rP3Q/640?wx_fmt=png)

*   在弹出的配置占位符的窗口中输入 mdnotes 检索一下，如下图
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBkQvXx82IRsHRiaI3gw4X2rJCH30dW6ISa86mKibMbRZ3SBBLsbkLe2GQ/640?wx_fmt=png)

> 我有必要说一下上图，一共有 4 列:
> 
> *   第一列就是占位符名称（也可理解为 ob 笔记模板的字段名称），注意看前面一大长串都是相同的，只有后面. url  .tags  .title 等有区别，也就是说你需要自定义一个这里没有的占位符，照抄上面的名称就行，第二、三列不用管
>     
> *   第四列就是占位符具体的格式，设置具体原理自己看说明文档，这里我只说你怎么改，而且改动非常小，也非常简单。就拿 url 这个来说吧，只需要将 Value 这一列，{{field_contents}} 前面的内容换为我上图的 \ nURL:: 即可，注意 URL 后是双冒号 + 一个空格。
>     
> *   另外 publicationTitle 就是我新建的，你把下面的名称和 value 复制粘贴过去就行，名称：extensions.mdnotes.placeholder.publicationTitle；值：{"content":"\npublicationTitle:: {{field_contents}}","zotero_field":"publicationTitle","link_style":"wiki"}
>     

当然，你可能不知道如何新建一个占位符？

右键标题栏（就是 preference name 那一栏）----New----String

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTB7sWqichrQur4YAITzLbwQhDeHydabnYicDdX97X8zb2XdAXNiceCJQmXw/640?wx_fmt=png)

然后就是输入名称和值

配置完之后，关闭即可。

#### 2.1.3 在 Obsidian 中新建文件夹和笔记模板

*   **新建文件夹。打开** Obsidian，新建一个文件夹 (名称自定义，例如 Reading Notes)，用于存放文献笔记，在我的开箱即用库中 **B - 科研笔记 / Reading Notes** 已新建此文件夹。
    
*   **新建笔记模板。**新建一条笔记，将其名称命名为 Mdnotes Default Template（必须是此名称，不可自定义），然后将此笔记（模板）放在模板文件夹下，当然你想放在任意文件夹下都是可以的。在本人分享的开箱即用库中，此模板存放于 **Z - 附件 /@Templates** 文件夹下。
    

> 关于 mdnotes 笔记模板，这里我需要强调一下，mdnotes 的模板有好几种：
> 
> 1.  Mdnotes Default Template.md
>     
> 2.  Standalone Note Template.md
>     
> 3.  Zotero Metadata Template.md
>     
> 4.  Zotero Note Template.md
>     
>     我采用的是第一种，这种会创建一条包含文献元数据的空白笔记文件（也就是说不会将你标注的内容提取出来）；如果你需要提取 PDF 标注内容，请使用 3 和 4，具体配置参见 mdnotes 说明文档 [2]
>     

emmm，我的最新文献笔记模板，在 V1.5 版本的开箱即用库中获取。

#### 2.1.4 Mdnotes 偏好设置

安装好插件之后，点击 Tools，便会看到 mdnotes preference，点击它

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBaPxCOjiaU9d5ibqHnAugYWlYOTc5TKenRQe0MO3yFnR3V4WgXSRX1PWg/640?wx_fmt=png)

在弹出窗口（见下图）中要设置模板文件和笔记存放文件夹路径

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBSp3A0N6vaVzjTyLOuREQsd4USUd4pCXZtZFsaukQEiczMW2QGicUpBmg/640?wx_fmt=png)

我不喜欢将 citekey 设置为标题，因为不方便我在 ob 中检索，我偏向于将笔记名称设置为年 + 文献 title。

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBFIfhFicwldtrC0kyCj2zhyO61G73R4CUl3wfibKkHgG4oSjTyLL63MCg/640?wx_fmt=png)

前缀设置为‘-’是为了在其前面输入年份，看个例子：

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBFe9MNia8slJsM7xScnT5XVoHze5Oa33m2Z3NKibarAlJRPELFCpuvuaA/640?wx_fmt=png)

mdnotes 的配置完成。

#### 2.1.5 Better BibTex 的配置

配置它的目的是将其导出的 Bib 引用格式设置为 google 学术导出的 bib 引用格式。

依次点击 Edit---preference--- 选中 Better BibTex，按下图配置

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBia0uUFUPKZalyaYSZqiblNXjk7L8sc58n9UNc9nyKsantGeUvMvoia1hg/640?wx_fmt=png)

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBGK9gAQU0BvjtJqGwBN5w5bBfbD2liaheyV42iajhoObfFssnvYAsESgA/640?wx_fmt=png)

配置完毕。

### 2.2 在 Ob 中设置一键随想和补充新知

在阅读文献的过程中，难免会遇到各种问题和产生各种想法，此时便需要方便快捷的记录它。当然你可以直接写在 obsidian 文献笔记里，但这样不适合引用和汇总。

另外，根据我自己的工作流，我希望将遇到的新知识（主要是概念，原理等）都添加到专业知识这个文件夹中，方便日后补充和引用。

下面说一下具体配置教程

用到的插件是 **QuickAdd** 和 **page header** 以及 **Ob 模板**

#### 2.2.1 设置模板

在模板文件夹新建两个模板，模板名称随意，在我的开箱即用库中就命名为文献阅读随想模板和专业知识模板，模板里的内容自定义，下面是我的模板（放在开箱即用库里了）

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBWmmedTSfHgltAfFPnudfRQIEgDdp0gbgSmvufN9dTibp5R8lF1n7dPA/640?wx_fmt=png)

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBcxSrNqDETJsKtz436ibr1AGHsBxFDTP5tZhicSFOR427x3ZojickXDjlQ/640?wx_fmt=png)

模板的内容根据自己的需要随便填。要强调的一点是，**为了能用 dataview 查询到不在 yaml 区的字段，在字段后要跟两个冒号和一个空格**。

#### 2.2.2 配置 QuickAdd

我就以一键随想为例，演示如何设置，【quickadd 的简介和原理我就不介绍了，帖子很多】

*   打开 Quickadd 选项页，按下图输入
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBhH3jhj0QNrA4EaPr8zmlwwsViaxkn7YvonLl9ylj85UokZBI1tIZDpQ/640?wx_fmt=png)

*   点击 add choice，然后点击右边的配置一键随想
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTB1Alia1kZkNbiaxTGxCFMWnxvkCyuzCY22cvHPLHeJPElGIYwJqJr0egQ/640?wx_fmt=png)

*   在弹出的窗口中，按下图配置
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBSXMlkGyPibylU0pfddynB1GLU3TvbzMIAUCYR70E06ibYyY3012Lqhww/640?wx_fmt=png)

按上图配置，当你运行一键随想命令，便会在 @Inbox/ZK Box 文件夹创建一条以日期 + 时间为名称的笔记，且此笔记的双链会被添加到当前文献笔记的光标处。此功能倒是与我之前分享的这篇推文类似👉

*   然后在 Quick 窗口，点击一下闪电形状的图标，为了将其添加到命令，按 ctrl+P 可以检索到它
    

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBSPtCopLzqBOpVcBMGOdkOdoEKvP09lUgnicfJtJUiaFLw9llSbPWTUFA/640?wx_fmt=png)

*   接下来就是利用 page header 插件将一键随想命令添加到文档标题栏，方便我们点击
    

打开 page header 选项，点击 Add Command，添加一键随想命令即可

![](https://mmbiz.qpic.cn/mmbiz_png/PR2BLDgtAWSzcWxj1J5paLnaQ5uB8ibTBu0r3cfLX0UZxeYeqmgl2jrdT364Owq3yfdNoDxy0gt7I7KyBEbTMoQ/640?wx_fmt=png)

补充新知（专业知识模板）也是按上述步骤配置，唯一不同的是，在点击命令后，会弹出一个输入窗口，我们可以直接输入问题，并将此问题会自动变为笔记名称，具体配置方式，在我的开箱即用库里，打开 quickadd 选项即可看到，这里我就不多说了。

### 2.3 DataView 汇总文献笔记和一键随想

前面配置好了，这个就很简单了。安装好 dataview，然后设置好语句，就可以汇总了，最简单的语句如下，直接复制粘贴过去就能用。

*   文献笔记汇总
    

```
``` dataview
table 一句话描述,tags,publicationTitle,authors,topics,PDFAttachments,DOI
from "B-科研笔记/Reading Notes"
```

```

这个在开箱即用库 V1.5 的 Home 笔记中都配置好了，只要 Reading Notes 文件夹中有笔记，就会被检索汇总到 Home 笔记中。

*   一键随想汇总
    

```
``` dataview
table tags, aliases, source, Notes
from "@Inbox/ZK Box"
```

```

这个是在 @Inbox/ZK Box 文件夹，已配置好，开箱即用。

3 写在最后
------

拿到开箱即用库 V1.5 版，文末获取。

开箱方式（Ob 新手指南）👉

https://flowus.cn/hust1037/share/1c977c13-d3eb-4c52-a93f-d77f56e4923e

实现上述工作流，只需要做下面两件事  

*   安装 mdnotes 插件，配置 mdnotes，就是 2.1.4，设置模板和笔记存放路径等
    
*   修改占位符 2.1.2 和 2.1.5
    

有问题，欢迎加入维客笔记交流群交流，特别欢迎你分享好玩且有趣的工具等，入群方式在公众号后台右下角（群人数大于 200 人，只能通过邀请入群），

![](https://mmbiz.qpic.cn/mmbiz_gif/PR2BLDgtAWRGRVlcvBD32A0CiaLCElMgDpOnfTVs4tCH0KwNtfqXx320nfYb56PEaHAjiau71SmjxYuLtrx7sECQ/640?wx_fmt=gif)

4 Reference
-----------

[1] 英文论坛帖子：

https://forum.obsidian.md/t/zotero-zotfile-mdnotes-obsidian-dataview-workflow/15536

[2] mdnotes 说明文档:

https://argentinaos.com/zotero-mdnotes/docs/quick-start-guide

插件与开箱即用库获取方式：关注**维客笔记**微信公众号，后台回复 **20220626**