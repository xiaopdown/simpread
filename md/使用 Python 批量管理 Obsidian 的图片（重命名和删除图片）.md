> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/654250338)

在 Obsidian 中，图片管理是个老大难的问题。

我们可以使用 `obsidian-paste-image-rename` 插件来为插入的图片重命名。

但是一来感觉这样比较麻烦，二来装太多插件也是我不希望看到的。尤其是装个插件只为给图片改名就觉得很不爽。

为此我写了一个 Python 脚本来完成以下几点需求。

1.  所有被引用图片都被更改为引用文件名 + 序号，如 markdown 文件名为 `A.md`，则该文件引用的所有 png 图片都更改为 `A_00.png`，`A_01.png`，`A_02.png` 等等这样的形式，对应的 markdown 文件里也做同样修改。
2.  如果图片目录里存在没有被任何 markdown 文件引用过的图片，则自动将其删除。
3.  如果 markdown 文件中出现了 `![[X.png]]` 这样的引用，但图片目录中根本没有 X.png 这张图，则自动在 markdown 文件中将这行文本删除。
4.  所有子文件夹及嵌套文件夹都要同时处理。

我的 Obsidian vault 名称是 Notes，图片被保存在 `Notes/!Attachment/Images` 中。在 `Notes/!Attachment/ObsidianSettings` 目录中新建一个 `organize_images.py` 文件，并写入以下内容:

```
import os
import re

def organize_images(notes_dir, images_dir):
    # 创建一个集合来存储所有被引用的图片文件名
    referenced_images = set()

    # 遍历 notes 文件夹中的所有子文件夹
    for subdir, _, files in os.walk(notes_dir):
        for file in files:
            # 只处理 .md 文件
            if not file.endswith('.md'):
                continue
            # 获取 .md 文件名（不带扩展名）
            file_name = os.path.splitext(file)[0]
            # 读取文件内容
            with open(os.path.join(subdir, file), 'r', encoding='utf-8') as f:
                content = f.read()
            # 查找所有 ![[...]] 标记
            matches = re.findall(r'!\[\[(.+?)\]\]', content)
            # 遍历所有匹配项
            for i, match in enumerate(matches):
                # 检查 match 是否表示一个图片文件
                if not match.lower().endswith(('.png', '.jpg', '.jpeg', '.gif', '.svg')):
                    continue
                # 检查图片文件是否存在
                if os.path.exists(os.path.join(images_dir, match)):
                    _, ext = os.path.splitext(match) # ! 获取文件的原始扩展名
                    new_name = f'{file_name}_{i:02d}{ext}' # ! 构造新文件名
                    referenced_images.add(new_name)
                    # 重命名图片文件
                    os.rename(os.path.join(images_dir, match), os.path.join(images_dir, new_name))
                    # 更新 markdown 文件中的 ![[...]] 标记
                    content = re.sub(rf'!\[\[{re.escape(match)}\]\]', rf'![[{new_name}]]', content)
                else:
                    # 如果图片文件不存在，则删除 markdown 文件中的 ![[...]] 标记
                    content = re.sub(rf'!\[\[{re.escape(match)}\]\]', '', content)
            # 将更新后的内容写回文件
            with open(os.path.join(subdir, file), 'w', encoding='utf-8') as f:
                f.write(content)

    # 遍历 Images 文件夹中的所有图片文件
    for image in os.listdir(images_dir):
        # 检查图片文件是否在 referenced_images 字典中
        if image not in referenced_images:
            # 如果图片文件没有被引用，则删除它
            os.remove(os.path.join(images_dir, image))

# 定义文件夹路径
notes_dir = '../../'
images_dir = os.path.join(notes_dir, '!Attachment', 'Images')
organize_images(notes_dir, images_dir)

```

运行该脚本，即可自动实现上述需求。

还可以在 Python 相同目录中新建一个 `organize_images.bat` 文件，写入以下内容:

```
@echo off
python organize_images.py
pause

```

这样以后每次有需求的时候，只用双击 bat 文件，就可以统一更新所有的图片文件了。