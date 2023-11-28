> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/591091259?utm_id=0)

0. 摘要
-----

Conda 是一个在 Windows、macOS、Linux 和 z/OS 上运行的开源软件包管理系统和环境管理系统。Conda 快速安装、运行和更新软件包及其依赖项。Conda 可以在本地计算机上轻松创建、保存、加载和切换环境。它是为 Python 程序创建的，但它可以为任何语言打包和分发软件。

上面是从官网抄的. 人话来讲就是: 如果你是 Python, R, Ruby, Lua, Scala, Java, JavaScript, C/ C++, Fortran 等语言的程序员, 而且你已经受够了各种库 / 包 (libraries/package) 之间的乱七八糟的依赖关系和冲突, 那么 conda 适合你.

换而言之, conda 使得人类可以在一台计算机的一个操作系统中同时安装多个版本的解释器和各种库, 而在需要使用特定版本的时候可以单拎出来, 无需重新安装或者面临各种冲突.

虽然 conda 支持很多语言, 但是估计大家用的最多的就是使用 conda 的 Python 项目吧 (例如机器学习, 数据处理之类的). 所以本文将讲解关于运行 Python 程序的围绕 conda 安装方法与使用方法.

这只是我在安装时的一个记录, 可能有不正确的地方或者不够好的地方, 仅供参考 (以及作为我自己的备忘录).

*   **本教程可能更适合**非计算机专业的电脑用的很拉跨的人用来参考 (因为很详细), 同时计算机相关专业的同伙也可以参考参考, 并提出些许意见.
*   **本教程安装的是 miniconda,** 这是一个比 anaconda 小的 conda 版本, 轻量, 只包含 conda 的基础功能 (不包括 anaconda 的那个 IDE 一样的东西和其他乱七八糟的一大堆库.........anaconda 非常笨重, 而且自带的功能稍许臃肿, 大多数情况应该用不到这么多, 并且我有 vsc 作为编辑器, 所以要这么多干啥? 这个就很好用. 我曾经安装 anaconda 直接被它那一大堆工具给弄懵了......
*   **我用的是 VSC**, 但是如果你用 pycharm 或者其他的什么, 都可以, 这个无妨. 我感觉 vsc 带上插件的功能对于 Python 是够用的, 至少 pycharm 能干的它也基本能干, 而且 vsc 还能写其他代码.
*   操作里可能需要**管理员权限**, 请确保你有计算机的权限.
*   **教程基于 Windows.**
*   你的计算机至少要能比较方便的上网.

最后, 简要介绍几个 conda 的操作 (比如新建环境, 激活环境啥的), 然后简单安装个 PyTorch 的 cuda 版本.

如果你有地方和这里写的不同, 那么一些过程可能不同, 因为我只安装了一次, 所以我也不知道哪里不同会产生什么后果........ 最好跟着做吧.

开始.

> 别急, 我有话要说.......  
> 计算机技术是一个进步非常快的行业, 所以类似于本文的各种教程, 很多都会随着时间的改变而发生略微变化...  
> 我的建议是, 如果有些地方, 实际操作和教程对应不上, 那么可以稍微思考一下, 因为一般都是微调.  
> 比如后文关于初始化 conda 环境的地方, 之前是在安装目录下, 然而我发现新版似乎变为了安装目录 / condabin / 下. 像这种, 大家可以灵活处理.  
> 关于为什么有这个提示....  
> 因为太多的人是真的没有一点灵活处理问题的能力啊....

1. 卸载残余的 Python
---------------

这里假设你的计算机上已经有一个 Python 版本了. 如果你从未安装 Python, 请跳过.

理论上不卸载也可以, 但是为了避免后面可能遇见的各种冲突和不兼容, 同时为了节省宝贵的磁盘空间, 还是卸载了吧. 毕竟安装 conda 时会带一个 Python.

### 1.1. 在控制面板卸载

如图

![](https://pic4.zhimg.com/v2-4fe43aa97a727729b43bf5148202f803_r.jpg)![](https://pic2.zhimg.com/v2-a6b6a4fa8a5208949200f9baf9edbae5_r.jpg)![](https://pic3.zhimg.com/v2-3f5cd3bec382dadf9cd87acaa8879e96_r.jpg)

点击名称来按照字母排序, 在上面红圈 "P" 打头的地方找到你安装过的 Python, 右键卸载掉 (我已经卸载了, 所以请假装那里有一个 Python).

### 1.2. 清理门户

主要是清理环境变量和残留的包.

### 1.2.1. 删除残留的文件 (可以不做)

重点排查以下位置, 是否有`Python`以及一些有关系的文字? 如果有, 那么确认是 Python 的东西就可以删了 (如果一些东西是其他程序的依赖, 那么别轻易删除), 注意这里的路径可能有一些是隐藏文件, 需要开启隐藏文件显示, 或者直接在路径栏输入然后回车. 不会的话请善用搜索:

```
C:\Program Files
C:\Program Files (x86)
C:\
C:\Users\%这里替换成你的用户名%\AppData\Local
C:\Users\%这里替换成你的用户名%\AppData\Roaming

```

比如这个就是 Python 相关的

![](https://pic1.zhimg.com/v2-cc91d59a61d4d8fa8362e2113a710f04_r.jpg)

如果你的 Windows 是中文的, 那么系统可能贴心的把`users`给你汉化了, 如图

![](https://pic3.zhimg.com/v2-029d3fba81cd5ea76427968e7b7b4886_r.jpg)

然后就是这里几个文件夹, 一个是公用, 另一个大概率就是你的用户名了, 选择你的账户双击进去就行. 如果你不知道你什么名字............

### 1.2.2. 清理环境变量

之前的 Python 大概率是加入到系统的 path 的, 需要删了相关的路径.

![](https://pic3.zhimg.com/v2-64bb1353955fdff98f0667b48eabc8be_r.jpg)![](https://pic1.zhimg.com/v2-08f496353d32ccd1dbe237fa6e305d10_r.jpg)![](https://pic2.zhimg.com/v2-9e71df92bba23735c381ac649a759475_r.jpg)![](https://pic4.zhimg.com/v2-4c858115c9024adf413be9e7ff155fab_r.jpg)

类似于这种和 Python 沾边的可以删除了. (看路径中是否包含 Python, 然后确认下只有 Python 在用这个, 别删错了)

一般来说会有几个地方, 一个是`..../Python/`, 一个是`..../Python/bin`, 一个是上面圈起来的. 还有一些相关的......... 理论上只要包含 Python 关键字的删了应该都没啥事, 除非你把什么东西给顺路装到这里了.

由于 conda 的特殊性, 安装 conda 后不用设置环境变量. conda 使用 PowerShell 的加载项来实现虚拟环境加载.

到这里, 清理工作就差不多了.

![](https://pic4.zhimg.com/v2-8e8439b8e3cb03cf539a5789c8fd0607_r.jpg)

2. conda 的安装
------------

这里下载 miniconda, Miniconda 是 conda 的免费最小安装程序。它是 Anaconda 的一个小型引导版本，只包含 conda、Python、它们所依赖的包，以及少量其他有用的包，包括 pip、zlib 和其他一些包。使用 conda install 命令从 Anaconda 存储库安装 720 + 个额外的 conda 包。

当然你也可以下载 anaconda 并安装, 差不多的.

### 2.1. 下载

这是官网文档:

[Miniconda - conda documentation](https://docs.conda.io/en/latest/miniconda.html)

当然你不会看文档的, 所以这里**下载** (国内镜像, 快):

[Index of /anaconda/miniconda/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/)

找个最新版本就行了, 比如我在 2022 年 12 月 12 日用的这个:

![](https://pic3.zhimg.com/v2-d19025727187fe0d31c87dca14ba6cc6_r.jpg)

Windows 而且是 64 位 x86 处理器那么选择这个就行.

### 2.2. 安装

Windows 图形界面下, 双击, 安装就行. 相信大家都没啥问题.[[1]](#ref_1)

![](https://pic1.zhimg.com/v2-ed3d02adc8a5815369d2c624320e5594_r.jpg)

这里建议选给所有用户安装.

**安装地址的话,** 我是默认 c 盘的, 因为 conda 创建虚拟环境的位置可以设置的, 而我又喜欢把程序放到 c 盘 (有仪式感), 所以不妨设定一个`c:/miniconda/`即可. 注意路径不能有空格, 所以不能放在`c:/Program Files`, 之类的位置.

然后这里

![](https://pic3.zhimg.com/v2-eac62ce5734539a8c795e2e92e908622_r.jpg)

如果你选的为所有用户安装, 那么第一个对勾应该是不能选择的, 会告诉你稍后需要简单手动设置一个环境变量.

第二个勾上 (会安装你下载的 miniconda 那个版本的 Python).

安装成功后就完事了.

### 2.3. 初始化 conda 到全局 PowerShell

我习惯用 PowerShell 作为 shell 去操作. 这玩意更类似于 Linux 的操作逻辑, 比 cmd 不知道高到哪里去了. 而且 vsc 默认的也是 PowerShell.

首先移步到你安装 miniconda 的路径去打开其下的 condabin 文件夹, , **按住键盘 shift 然后右键单击文件夹空白部分**, 打开一个 PowerShell

![](https://pic4.zhimg.com/v2-f8aaa724fc145daf022033523a739367_r.jpg)

然后输入:

```
./conda init --all

```

conda 会运行一些东西, 把自己注册到 PowerShell 上, 下次你启动 PowerShell 就会自动加载环境了. 类似于这样:

![](https://pic1.zhimg.com/v2-363f60b6293d87ad15416928033e9b40_r.jpg)

然而这里可能有两个问题:

*   最后可能报错, 翻译过来大概是 "权限不够" 的意思. 此时你需要使用管理员权限, 启动一个管理员 PowerShell 窗口重试就行了.

![](https://pic2.zhimg.com/v2-8ea06ed958a99a3887deda3d36756271_r.jpg)

启动之后用`cd`命令移步过去, 例如`cd c:/miniconda/condabin/`这样, 只要到目的地就行, 可以利用 tab 键自动补全.

*   然后就是你会发现, conda init 后, 每次打开 PowerShell 都会慢大概 1~1.5s, 这是没办法的事情, conda init 的原理是运行一段脚本, 改变 PowerShell 的启动方式, 使其启动的时候运行加载虚拟环境的命令. 虽然会变慢, 但是其实无妨, 加载的时候仍旧可以输入你的命令, 只不过等待加载完了才一股脑显示出来. 所以无需担心计算机跟不上你的思维速度. (键盘输入到 stdin 缓冲区的). 同时, conda 的这个初始化不影响 PowerShell 正常使用. 而且这也是 vsc 兼容 conda 的唯一方式 [[2]](#ref_2)

### 2.4. 添加环境变量

最好把这个添加到 path 中:

![](https://pic1.zhimg.com/v2-ced50b9b6f8c936e97aff7cc368bfd20_r.jpg)

因为这个是 base(默认基础) 环境的 pip 安装的包的位置, 有时候一些工具会在这里, 这样以后使用包的时候方便些 (比如 pyuic5 之类的). 添加 path 的方法和前文介绍的反着来就行. 右边`新建`按钮.

**20230512 更新:**

注意, 在 base 环境中安装基本模块 (比如格式化代码用的 yapf 或者 autopep8) 时应该使用管理员权限来执行 pip install, 否则 pip 没有权限写入信息到 miniconda 的安装目录中, 会自动重定向到处于 %username%/AppData/local/python/script 下 (大概是这个目录, 我不知道我记忆正确否). 不方便管理.

如果你是在其他磁盘或位置安装的 miniconda 那么应该不会面临权限问题.

如果你是默认安装目录, 并且保持在 base 下使用 pip 时使用管理员权限的良好习惯 (实际上 base 环境应该不至于天天安装新东西), 那么再把下面 3 个环境变量加一下. 参考我的安装目录自己找找.

![](https://pic3.zhimg.com/v2-a3a70f7a784b5b96714107a4badda00e_r.jpg)

这个好处是, 如果你用 vsc 的话, 能自动找到 conda 环境并且可以很方便的激活了.

![](https://pic3.zhimg.com/v2-e8ba26e2942f73e27395f8bb2ab5f5b6_r.jpg)![](https://pic1.zhimg.com/v2-5ba35354d3cce6587318195a92e95fe0_r.jpg)

你看这是多么的方便.

3. conda 的使用
------------

安装完了, 如果没出什么幺蛾子的话, 你可以开始了.

不过在这之前, 最好做以下操作.

### 3.1. 切换源

众所周知, 我们中国大陆的国际出口带宽目前很低, 所以直接 pip install 或者 conda install 会很慢, 请做如下设置使用国内镜像加速下载:

*   编辑 `C:\Users\%你的用户名%\pip\pip.ini`, 如果没有就新建文件夹 / 文件, 搞出来一个就行了. 记得正确编辑扩展名`.ini`, 我觉得这不是问题.

![](https://pic4.zhimg.com/v2-02e35d0a57aa1b61c5b3ba1bcd47f32f_b.jpg)

双击编辑, 添加以下内容

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = pypi.tuna.tsinghua.edu.cn

```

这个设置了 pip 默认从清华源搞资源. 国内赛尔网络是很快的. 以后就可以快乐的 pip 了.

*   然后设置下 conda 的, 去编辑`C:\Users\ngc13\.condarc`这个文件, 没有就创建一个.

![](https://pic2.zhimg.com/v2-aebcb2007e42242f7c1e4285342e9755_r.jpg)

里面写入以下设置文字 (可以右键 - 其他方式打开 - 记事本), 注意我把大部分设置都注释掉了 (这样 conda 会使用默认值, 注释是每行开头的`#`符号, 你仔细看就会发现保留的地方是换源的操作). 当更改了这个文件之后, 下次就会自动使用这里的配置了.

```
# add_anaconda_token: True
# add_pip_as_python_dependency: True
# aggressive_update_packages:
#   - ca-certificates
#   - certifi
#   - openssl
# allow_conda_downgrades: False
# allow_cycles: True
# allow_non_channel_urls: False
# allow_softlinks: False
# always_copy: False
# always_softlink: False
# always_yes: None
# anaconda_upload: None
auto_activate_base: True
# auto_stack: 0
# auto_update_conda: True
# bld_path: 
# changeps1: True
# channel_alias: https://conda.anaconda.org
# channel_priority: flexible  # https://blog.csdn.net/egoyang123/article/details/106595117
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/fastai/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
# client_ssl_cert: None
# client_ssl_cert_key: None
# clobber: False
# conda_build: {}
# create_default_packages: []
# croot: C:\Users\ngc13\conda-bld
# custom_channels:
#   pkgs/main: https://repo.anaconda.com
#   pkgs/r: https://repo.anaconda.com
#   pkgs/msys2: https://repo.anaconda.com
#   pkgs/pro: https://repo.anaconda.com
# custom_multichannels:
#   defaults: 
#     - https://repo.anaconda.com/pkgs/main
#     - https://repo.anaconda.com/pkgs/r
#     - https://repo.anaconda.com/pkgs/msys2
#   local: 
# debug: False
# default_channels:
#   - https://repo.anaconda.com/pkgs/main
#   - https://repo.anaconda.com/pkgs/r
#   - https://repo.anaconda.com/pkgs/msys2
default_python: 3.9
#default_threads: None
# deps_modifier: not_set
# dev: False
# disallowed_packages: []
# download_only: False
# dry_run: False
# enable_private_envs: False
env_prompt: ({default_env}) 
envs_dirs:
  - E:\conda_env\envs
  - C:\Users\ngc13\.conda\envs
  - C:\Python\MiniConda\envs
  - C:\Users\ngc13\AppData\Local\conda\conda\envs
# error_upload_url: https://conda.io/conda-post/unexpected-error
# execute_threads: 1
# experimental_solver: classic
# extra_safety_checks: False
# force: False
# force_32bit: False
# force_reinstall: False
# force_remove: False
# ignore_pinned: False
# json: False
# local_repodata_ttl: 1
# migrated_channel_aliases: []
# migrated_custom_channels: {}
# non_admin_enabled: True
# notify_outdated_conda: True
# offline: False
# override_channels_enabled: True
# path_conflict: clobber
# pinned_packages: []
# pip_interop_enabled: False
pkgs_dirs:
  - E:\conda_env\pkgs
  - C:\Python\MiniConda\pkgs
  - C:\Users\ngc13\.conda\pkgs
  - C:\Users\ngc13\AppData\Local\conda\conda\pkgs
# proxy_servers: {}
# quiet: False
remote_backoff_factor: 1
remote_connect_timeout_secs: 9.15
remote_max_retries: 3
remote_read_timeout_secs: 60.0
# repodata_fns:
#   - current_repodata.json
#   - repodata.json
# repodata_threads: None
# report_errors: None
# restore_free_channel: False
# rollback_enabled: True
# root_prefix: C:\Python\MiniConda
# safety_checks: warn
# sat_solver: pycosat
# separate_format_cache: False
# shortcuts: True
show_channel_urls: True
# signing_metadata_url_base: None
# solver_ignore_timestamps: False
# ssl_verify: True
# subdir: win-64
# subdirs:
#   - win-64
#   - noarch
# target_prefix_override: 
# track_features: []
# unsatisfiable_hints: True
# unsatisfiable_hints_check_depth: 2
# update_modifier: update_specs
# use_index_cache: False
# use_local: False
# use_only_tar_bz2: False
# verbosity: 0
# verify_threads: 1
# whitelist_channels: []

```

**但是不要直接复制我这个!** 抄作业好歹得改一下, 大概要改以下的位置 (如果你有些安装不是默认的, 那么可能还要改的更多):

1.  我的用户名 ngc13 换成你的
2.  我的安装路径换成你的
3.  其他的路径最好也检查下
4.  里面`pkgs_dirs:`和`envs_dirs:`的第一项, 这个是我设置的, 你可以照猫画虎, 自己在其他磁盘新建一些文件夹, 然后设置为你创建的文件夹的路径, **这个操作会将新建的 conda 环境安装到你设置的位置**而不会浪费 c 盘空间. 说实话 conda 多建立几个环境后体积大的离谱, 所以最好把所谓的 "数据库" 一样的东西放到其他地方.

### 3.2. 设置创建新环境的默认位置

上面已经说了. 这里就不说了.

简要介绍下:

conda 有一个基础环境`base`环境, 是你启动 PowerShell 或者 conda 的终端后看到的, 这个也是系统环境, 其中你在这里使用 conda 安装的包会安装到你的 conda 的目录下, 而用 pip 安装的包会安装到你的用户目录下, 两个位置一般都在 c 盘.

而你新建的环境, 会默认新建到你设置的文件夹下 (没设置的话还在默认位置, 就是 c 盘), 比如我设置的是 E 盘的某几个文件夹. 激活你建立的环境后, pip 和 conda 安装的包的位置 (以及 conda 安装的你要求版本的 Python) 都在你设置的位置里. 不同环境下互不干扰. 这就是 conda 的工作原理. 实质就是使用 shell 的命令, 人为的在运行时构建了一个特殊的环境变量方案, 调用你当前环境下的相关包和特定版本的解释器.

比如我在 base 环境只安装了 PyQt5 和 pyinstaller, 还有少量的几个包, 然后建立了一个 py39 名称的环境用来当高强度负载环境, 用来安装 PyTorch 和乱七八糟的一大堆东西, 这样我的开发环境就不吃 C 盘了.

同时也可以按需新建新的环境, 并配置不同版本的 Python.

### 3.3. conda 基础命令

首先, 如果你用的是 vsc, 那么你在目录中启动后, 他可能提示你选择环境

![](https://pic4.zhimg.com/v2-5ff49276421684c8fe5786e9399e89eb_r.jpg)

点击, 然后选择就行

![](https://pic4.zhimg.com/v2-4bf6523b16e260be14460b8cb4adbafb_r.jpg)

很方便. (前提是你已经 conda init 过了)

然后就是, 怎么类似于 pip 一样操作 conda 呢? (注意, 下面的操作均需要 conda init 初始化后才行, 如果你没有进行这个操作请往前翻, 前文有写, 在 2.3. 章节)

首先打开一个 PowerShell, 然后 [[3]](#ref_3)

1.  创建环境示范 (--name 后的参数是你给他起的名字, 随便起名, 叫小帅都行)

```
conda create --name py39 python=3.8      # 注意这里虽然我给名字起的是"py39", 但是实际上安装的是Python3.8版本

```

2. 激活环境 (按名子激活)

```
conda activate py39

```

激活后会发现环境变了

![](https://pic4.zhimg.com/v2-faa87b63f8df81440922eacfa0d594d3_r.jpg)

3. 退出的方法就是取消激活的方法

```
conda deactivate py39

```

4. 删除环境

磁盘大可以不用删除, 不激活的时候是没有系统的负担的, 所以你大可建立很多很多个虚拟环境

```
conda remove --name py39 --all

```

5. 列出当前系统中的环境

```
conda info -e

```

6. conda 来安装相应的包

切换到你的目标环境下后, 键入 (这里拿 numpy 做举例)

```
conda install numpy

```

7. 列出当前环境下安装的包, 该操作还会显示包的安装方法 (比如哪些是 conda 安装的, 而哪些是 pip 安装的)

```
conda list

```

8. 查找当前环境下包的信息

```
conda search numpy

```

9. 更新当前环境下的包

```
conda update numpy
conda update --all     #升级全部
conda update conda     #升级conda自己

```

10. 删除当前环境下的包

```
conda remove numpy

```

11. 更新当前环境下的 Python. 注意这里更新 Python 指的是将 Python3.x.y 的 y 更新到最新, 而不会更改大版本.

```
conda update python

```

12. 当前环境下使用 pip

直接使用就行, 例如

```
pip install matplotlib
pip list
pip ...
...

```

但是建议 pip 仅在 conda 不能用的时候才使用. 因为 conda 的包管理与版本控制更严格, 更不容易出现依赖冲突. pip 用一时爽一时, 到后面冲突的时候就........ 不太好处理了.

pip 检查包的兼容性时, 仅安装的时候检查, 如果已经按照的包和要安装的包冲突, 则报错. 而 conda 在安装多个包的时候可以自动智能的选择兼容的一个版本方案, 然后处理好. 但是注意, conda 无法检查 pip 安装的包与自己将要安装的包的兼容性.

要是 pip 真的引起问题了, 请做好手工修理或者直接重建环境的觉悟.

4. 使用 conda 简单安装一个 PyTorch
--------------------------

### 4.1. 去官网

[PyTorch](https://pytorch.org/)

### 4.2. 选择版本

![](https://pic2.zhimg.com/v2-94ea2fad61441150c3812d9ebfcd222d_r.jpg)

然后得到命令

### 4.3. 命令行安装

复制底下给出的命令, 然后激活目标环境, 在自己要用的环境下, 运行即可

conda 会帮你安装好.

如果 conda 不行可以试试 pip 安装.

注意 PyTorch 这里给出的命令是自动安装 cudnn 的. (但是你仍然要先给显卡安装驱动和 cuda 运行库, 也可能在安装 cuda 的时候就安装了 cudnn 了, 反正不用专门安装了)

另外, 建议和我一样, 熬个夜, 在凌晨 4 点到 7 点下载, 这个时候国际链路比较通畅, 不卡 (清华源给的镜像似乎有问题).

或者使用科技上网方法.

更多详细信息可以参考我的这个教程:

[NGC13009：[PyTorch] 安装笔记, 基于 Windows10/cuda11.6](https://zhuanlan.zhihu.com/p/542729666)

[end]

参考
--

1.  [^](#ref_1_0) 这里截图是偷的, 原文在这里 [https://www.bilibili.com/read/cv10603513/](https://www.bilibili.com/read/cv10603513/)
2.  [^](#ref_2_0) 我没发现第二种
3.  [^](#ref_3_0) 这里参考了这个文章 [https://zhuanlan.zhihu.com/p/44398592](https://zhuanlan.zhihu.com/p/44398592)