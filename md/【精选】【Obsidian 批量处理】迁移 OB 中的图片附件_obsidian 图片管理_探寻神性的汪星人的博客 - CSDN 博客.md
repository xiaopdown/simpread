> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_59445434/article/details/128156844)

需求
--

我想要将旧的 [Obsidian](https://so.csdn.net/so/search?q=Obsidian&spm=1001.2101.3001.7020) 库中的笔记迁移到新的库中，简单的复制 markdown 文件是不够的，还需将笔记中的图片附件一起迁移过来才行，不过我的附件都统一放在一个文件夹中，当需要遇到大量的图片附件时，就不能简单手动复制粘贴了，所有我需要用 Python 来替我完成这件事。

熟悉 Obsidian 的人都知道库中没有的图片附件会在关系图谱中全部显示，如下图所示：  
![](https://img-blog.csdnimg.cn/2ca0e4f8057045c3befee370cf5047ea.png#pic_center)

分析
--

### 1. 需求分析

1.  首先需要知道迁移过来的笔记缺少什么图片附件。
2.  然后将缺少的图片从旧的库中复制到新的库目录下。

### 2. 流程图 [1](#fn1)

开始 结束 提取出笔记附件列表 旧库中的附件列表 取二者的交集 遍历集合 读取附件 复制附件

实现
--

### 代码

```
import re  
import os  
  
# 1. 提取笔记中的附件列表  
# 1.1 输入笔记的路径地址  
noteName = input('请输入笔记路径地址：')  
# noteName = r"D:\MyNote\immortal\📓笔记系统\02_Other\Spark\pandas 课件.md"  
# 1.2 读取笔记文本内容  
with open(file=noteName, mode='r+', encoding='utf-8') as f:  
    data = f.read()  
  
# 1.3 剔除笔记中代码块的内容  
pattern = re.compile('```.*?```', re.DOTALL)  
data_list = pattern.split(data)  
  
# 1.4 提取附件名  
reguler = '\[\[(.*?\.png)]\]'  
attachment_list = [j for i in data_list for j in re.findall(reguler, i)]  
  
# 2. 旧库附件目录下的附件列表  
fileName = 'D:\MyNote\FintechNote\附件'  
files = os.listdir(fileName)  
  
# 3. 取二者的交集  
a_set = set(attachment_list)  
inter = a_set.intersection(files)  
  
# 4. 遍历集合  
t = 'D:\MyNote\immortal\A附件'  
for i in inter:  
    # 读取文件  
    suorce = fileName + '\\' + i  
    with open(suorce, 'rb') as f:  
        data = f.read()  
  
    # 复制文件  
    target = t + '\\' + i  
    with open(target, 'wb') as f:  
        f.write(data)  
  
else:  
    print('附件迁移完毕')

```

** 执行结果：** 可以看到这个笔记已经不存在空的附件了  
![](https://img-blog.csdnimg.cn/036d73eb2b2e45b8a1b98679a6d0286b.png#pic_center)

### 技术要点

#### 1. 文件操作

**文件读取、复制：**

```
with open(文件路径,操作模式) as 文件对象:
    # 读操作
    data=f.read() # 返回一个字符串
    data=f.readline() # 返回一行数据
    data=f.readlines() # 返回每行数据的列表
    # 写操作
    f.write() # 要写入的数据


```

> [!warning] 注意事项  
> 读取文件数据要使用 `r` 操作模式，需要将返回的数据赋予一个变量。

**获取某个文件夹下的信息：**`os.listdir(路径)`返回一个 list

#### 2. 正则表达式

*   **re.DOTALL 标记：** 简写是 `re.S`，表示 `.`能匹配所有字符，通常它不能匹配到 `\n`。
*   **re.split()：** 更 Python 内置的 split 功能一样，另外有两个可选参数 `maxsplit` 和 `flags` 分别代表最大分割次数和正则标记。

#### 3. 列表推导式

使用 split 函数后返回的是一个列表，需要对里面每个字符串使用 findall 找出所有附件名，返回的也是一个列表，这样就可以直接使用 [[【数据容器】列表集合[字典推导式](https://so.csdn.net/so/search?q=%E5%AD%97%E5%85%B8%E6%8E%A8%E5%AF%BC%E5%BC%8F&spm=1001.2101.3001.7020)#列表集合字典推导式 | 列表推导式]] 直接将所有附件名整合到一个列表中。

```
reguler = '\[\[(.*?\.png)]\]'  
attachment = [j for i in data_list for j in re.findall(reguler, i)]  
print(attachment)
# ['image-20220123020412280.png', 'image-20220123021121835.png',……]

```

#### 4. 集合 - 交集

**语法：**

```
集合1.intersection(数据容器)
# 返回集合1 与数据容器中元素的交集

```

> [! note]  
> 只有集合有 `intersection()` 这个方法，但是输入的参数可以是任意一种数据容器

1.  mermaid 画流程图 TB 是从上往下、BT 相反。菱形是用 `(())` 绘制。 [↩︎](#fnref1)