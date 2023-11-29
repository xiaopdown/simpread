> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [pkmer.cn](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E4%BD%BF%E7%94%A8%E6%8A%80%E5%B7%A7/pandoc-%E6%8F%92%E4%BB%B6%E5%AF%BC%E5%87%BA-word-%E6%A0%BC%E5%BC%8F-%E6%AD%A3%E7%A1%AE%E8%AF%86%E5%88%AB%E6%9C%AC%E5%9C%B0%E5%9B%BE%E7%89%87/)

> pandoc - 插件导出 - word - 格式 - 正确识别本地图片——pandoc 插件可以把 OB 的 md 格式导出各种格式，比如 Office 格式。

<div class="menu-toggle"> <SidebarToggle client:idle ></SidebarToggle> </div>

obsidian 使用技巧

* * *

pandoc 插件可以把 OB 的 md 格式导出各种格式，比如 Office 格式。

当导出 docx 格式时，本地插入的图片有时无法正确显示，有时却可以正确导出并显示。下面通过一系列实验，找出规律并进行总结，给在这方面有困惑的人参考。

插件安装并配置
-------

首先正确安装并设置 pandoc 插件，这点无需多说，只说重点几个点

1.  pandoc 需要下载客户端并安装，安装后在 ob 的 pandoc 插件中指定安装路径

![](https://cdn.pkmer.cn/images/202307031617567.png!pkmer)

```
如图，指定是 `C:\Program Files\Pandoc\pandoc.exe`
2 文档源格式是以 html 还是 markdown 格式导出，这里是能否正确显示图片的关键，下面会重点说

```

![](https://cdn.pkmer.cn/images/202307031618964.png!pkmer)

准备 md 文档 开始测试
-------------

1.  图片格式如果是图床形式，比如 http 或者 https 开头测试均可正常导出并识别。
2.  图片格式如果是本地图片。这里分两种情况

*   wiki 格式的图片 格式为 `![[XXXX.png]]` 这类的 需要 pandoc 中设置源格式 html 才可以正确识别。
*   md 格式的图片 格式为 `![](XXXXX.png)` 这种格式需要 pandoc 设置源格式为 markdown 才可以正确识别。

正确识别，不代表导出的 word 格式能正常显示图片，下面还有几个坑需要注意。

测试总结
----

为了表述问题更清楚，下面几个前提条件

1.  测试图片名称为 `202111241058704.png` 并位于库文件夹中的 “附件” 目录下
2.  Ob 库的物理路径为 `E:\Obsidian文档库\`

*   引用在线图床的图片，均正确导出。
*   引用图片如果是 file:/// 协议需要删除 file:/// 即可正确识别
*   pandoc 插件设置文件源格式为 **html**， 文档图片使用 `![[XX]]` 的形式，基于库的相对路径插入的图片才能正确识别。比如 `[[附件/202111241058704.png]]`
*   当设置文件源格式 **markdown**，文章引入图片的格式为 `![](XXXX.png)`。默认 pandoc 只去库根目录查找图片，如果图片存在其他目录需要使用参数指定，比如添加参数 `--resource-path="E:\Obsidian文档库\附件\"` mac 系统 应该是类似 `--resource-path=""/Users/xxx/Obsidian文档库/附件/"` 地址

![](https://cdn.pkmer.cn/images/202307031618173.png!pkmer)

*   当设置文件源格式 **markdown**，文章引入图片的格式为 `![](附件\XXXX.png)`。默认 pandoc 只去库根目录查找图片，需要添加参数 `--resource-path="E:\Obsidian文档库\"` mac 系统 应该是类似 `--resource-path=""/Users/xxx/Obsidian文档库/附件/"` 地址

目前 ob 中 pandoc 插件导出 word 格式并包含本地图片，只有以上这几种方式可以正确识别并导出。

下面用表格更清楚展示：

<table><thead><tr><th>插件设置的源格式</th><th>md 文档中的图片格式</th><th>导出结果</th></tr></thead><tbody><tr><td>html</td><td><code>![[附件/202111241058704.png]]</code></td><td>成功</td></tr><tr><td>html</td><td><code>![[202111241058704.png]]</code></td><td>失败</td></tr><tr><td>markdown</td><td><code>![](附件/202111241058704.png)</code></td><td>直接导出失败<br>添加参数 <code>--resource-path="E:\Obsidian文档库\"</code>&nbsp;成功</td></tr><tr><td>markdown</td><td><code>![[附件/202111241058704.png]]</code></td><td>导出成功，但 wiki 格式图片不识别</td></tr><tr><td>markdown</td><td><code>![](202111241058704.png)</code></td><td>直接导出失败<br>添加参数 <code>--resource-path="E:\Obsidian文档库\附件\"</code>&nbsp;成功</td></tr><tr><td>markdown</td><td><code>![](file:///E:/Obsidian/XX/202111241058704.png)</code></td><td>失败，删除 <code>file:///</code> 协议，导出成功</td></tr></tbody></table>

常见问题：

> **Info**
> 
> 介绍个简单的办法，不用手动改引用文件的路径：  
> 在 ob 的设置里，在 “文件与链接” 这一项里，把内部链接类型改成“基于仓库根目录的绝对路径”。然后 MD 就可以直接成功导出（html 为源格式）而不用另外设置了。  
> 其实就是对应的表格第一行的情况。

如果库名称包含空格会导出失败?

解决办法：用 %20 代替空格即可