> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [forum-zh.obsidian.md](https://forum-zh.obsidian.md/t/topic/9014/5) ![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/铅笔小明/96/3380_2.png)

大家好我是铅笔小明，今天给大家分享一个我在 obsidian 经常使用的一套自动化方案，这个功能我是从油管主播 Pamela Wang 的 ob 库里学到的，它可以让你在笔记中新建双链后，点击双链自动跳出选择套用的模板，还可以进一步选择要把笔记移动到指定文件夹。  
比较直观的功能入下方 gif 所示：  

![](https://forum-zh.obsidian.md/uploads/default/original/2X/f/facaed62aec474209da97005bdcc5717221f0f2e.gif)

#### 目前这个功能只需要一个插件：Templater

进行前先确保已经安装了 **Templater 插件**。  
我觉得也不需要一步步带着大家做，我会把代码和库都分享出来，方便大家下载直接修改使用。这里我只要去分析代码部分的修改代表的意义就可以方便大家去 DIY 对于自己独有的功能。

*   首先在选项里的文件与链接中指定一个新建笔记的存放位置，我这里就设置为 “00 - 临时” 这样我新建一个笔记，笔记就会自动移动到这个文件夹。
    
    ![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/8/858e7f11c86e423227cc5e8d3cd4f38204971b9d_2_690x495.jpeg)
    
*   然后把 **getTitleSnippet.js** 复制到库内的文件夹。我这里是复制到 templater 下的 script 里。
    
*   然后向下继续设置，把 script 文件夹设置到对应的文件夹。这样可以读取到我们复制过来的 js 脚本功能。  
    
    ![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/6/6556096cd19e2bc9c3ef43eafdcc8cd9d6be06a4_2_690x405.jpeg)
    
*   我们先建立一个模板文件我命名为 “01 自动选择模板”，这个可以随意命名，只要后面和 templater 里设置的对应上就行。
    
    *   这个模板里写入对应的 tp 语法。（会在最后分享）  
        ![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/6/6f1a308603b76dd406f4159d06cd9cf4a0b63b85_2_690x322.png)
    *   最上面的代码是调取我们之前复制的 getTitleSnippet.js 这个功能。这个脚本的功能是获取文件名中 “-” 前的文字来供下方的判断做选择。这个自动选择模板的功能是直接在写笔记的时候在 “-” 前写入关键词来让 ob 帮你判断这个笔记套用哪个模板，这样就不需要自己选择，可以设立多个关键词来对应同一个模板，比如我这里就设置了 “人物” 和“人”两个关键词，这样当我输入 [[人物 - 张山]] 或者[[人 - 李四]]。然后点击双链创建新笔记的话就会自动套用对应的人物模板。
*   再建立一个手动选择模板。
    
    *   如图所示。![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/c/c04b62d2cde1527be9f238957b74021d7269ed30_2_690x315.png)
    *   手动选择模板的功能是为了当没有在笔记中写入 “-” 和特定的关键词时新建笔记会自动弹出一些模板供你选择出你希望这个笔记用到的模板。方便快速调用。
*   最后建一个模板算一个补充功能，可以帮助你把模板分类。比如在手动选择模板的时候你想只出现三个大领域的选项 “工作”“生活”“其他” 然后在每一个领域点进去以后再有对应的一些模板选项。
    
    *   我这里建的是 “选择学习相关模板”![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/e/ea032b75801f92ce550d1e042cc1244d6d60f77e_2_689x364.jpeg)这个模板在自动选择模板中也出现过，也就是说如果我输入 [[学习 - 学点东西]] 然后点击双链建立新的笔记，那么它就会弹出几个学习模板选项供我选择。这样可能对模板多的人不会显得很杂乱。
*   接下来看一下 tp 的模板里需要如何设置和一些设置的具体功能
    
    *   大部分设置我是喜欢放在 yaml 区，这样预览模式的时候看不到。
    *   先看一下需要选择路径的模板设置。这种模板适用于主文件夹里还有一些子文件夹，会涉及到路径的选择语法。![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/9/92c532263d694121fc3ea4bd0114592bbdcf3a26_2_690x378.jpeg)最上面的部分是调用 js 脚本来改笔记的名字，去掉 “-” 和之前的内容。下面部分就是路径选择的脚本功能。
    *   第二个类型就是不需要选择路径，只需要放到特定的文件夹就行。![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/f/fc974a8d412d3234371b9163d9dabc5d19588b59_2_690x372.png)这里就取消了选择语句，只要填入路径即可。
*   在 Templater 设置中。先打开 Enable Folder Templates，这个功能是自动让加入到某个文件夹中的笔记套用对应的模板。现在这个设置就是让所有新建的模板先过一遍自动选择模板。
    
    ![](https://forum-zh.obsidian.md/uploads/default/optimized/2X/8/858e7f11c86e423227cc5e8d3cd4f38204971b9d_2_690x495.jpeg)
    
*   设置结束以后，就可以正常使用这个功能了。我会放出这个功能的事例库，和用到的脚本。大家可以自行选择下载。
    

功能库下载链接：  
[getTitleSnippet.js 132](https://www.yuelili.com/wp-content/uploads/2022/07/20220722111905-91.zip "getTitleSnippet.js")  
[功能库 109](https://www.yuelili.com/wp-content/uploads/2022/07/20220722103951-19.zip "功能库")  
链接: [百度网盘 请输入提取码 78](https://pan.baidu.com/s/1NTe_m8SI1sZHASyAD-xtPw?pwd=1c84) 提取码: 1c84