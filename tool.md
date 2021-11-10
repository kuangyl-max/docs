#  Window 终端配置

## Scoop配置

[Windows下Scoop安装、配置与使用_luoyooi的博客-CSDN博客_scoop](https://blog.csdn.net/luoyooi/article/details/102990113)

### 安装

在PowerShell中运行以下命令，将scoop安装到其默认位置(`C:\Users\<user>\scoop`)

```
Invoke-Expression (New-Object
System.Net.WebClient).DownloadString('https://get.scoop.sh')
```
**或**

```
iwr -useb get.scoop.sh | iex
```

安装完成后，输入`scoop help`验证是否成功（常见的命令可以通过此方法来查看）。

用户安装的程序和scoop本身位于C:Users\<user\>scoop。全局安装的程序（--global）位于C:\ProgramData\scoop。可以通过环境变量更改这些设置。具体步骤如下：

### 将Scoop安装到自定义目录(命令行方式)

```
$env:SCOOP='D:Applications\Scoop'

[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP,'User')
```


### 将Scoop配置为将全局程序安装到自定义目录 SCOOP_GLOBAL(命令行方式)

```
$env:SCOOP_GLOBAL='F:\GlobalScoopApps'

[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL',
$env:SCOOP_GLOBAL, 'Machine')

```

### 上面两句运行的结果(环境变量)

![在这里插入图片描述](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-38-45-69d072a8079102da338071daa6fa4c10-image55-d2410c.png){width="5.768055555555556in"
height="4.741666666666666in"}
如果不想运行命令行，直接添加环境变量也可。设置完安装位置后，建议将默认目录下的所有文件复制到新目录（**不是剪切！！**）

参考链接：
* [scoop------强大的Windows命令行包管理工具 - 简书(jianshu.com)](https://www.jianshu.com/p/50993df76b1c)

* 配色 如何保存更改 ：[zsh自定义命令提示符_如何使用Microsoft的ColorTool自定义命令提示符的配色方案_cum44153的博客-CSDN博客](https://blog.csdn.net/cum44153/article/details/109043040)


* [像MAC一样使用win10的Terminal - 简书(jianshu.com)](https://www.jianshu.com/p/4b2b7074d9e2)
* [使用Oh-My-Posh美化FluentTerminal_罗伯特祥的博客-CSDN博客](https://blog.csdn.net/weixin_43455581/article/details/105565970)

## 注意

### oh-my-posh 中文乱码

可以更改字体，如Fira Code Retina

或者[oh-my-posh3及oh-my-zsh提示prompt出现乱码的原因及使用Nerd字体的解决方法_yihuajack的博客-CSDN博客](https://blog.csdn.net/yihuajack/article/details/111405007)

## scoop工具安装

```powershell
scoop install 7zip
scoop install aria2
scoop install bfg
scoop install cacert
scoop install colortool
scoop install curl
scoop install cygwin
scoop install gawk
scoop install grep
scoop install Installed
scoop install maven
scoop install ntop
scoop install redis
scoop install sed
scoop install unzip
scoop install vim
scoop install wget

#cygwin 相当于虚拟Linux环境；内部可安装apt-cyg
#之后安装如下包
apt-cyg install tree 
```

> 若下载不了，则开启VPN

## 配置右键菜单栏

HKEY_CLASSES_ROOT\Directory\Background\shell新建PowershellMenu

空白处右键菜单

```
[HKEY_CLASSES_ROOT\Directory\Background\shell\PowershellMenu]
@="Open PowerShell Here"
"Icon"="C:\\\\Windows\\\\SysWOW64\\\\WindowsPowerShell\\\\v1.0\\\\powershell.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\PowershellMenu\command]
@="C:\\\\Windows\\\\SysWOW64\\\\WindowsPowerShell\\\\v1.0\\\\powershell.exe -NoExit -Command Set-Location -LiteralPath '%v'"
```

HKEY_CLASSES_ROOT\Directory\shell新建PowershellMenu

文件夹右键菜单

```reg
[HKEY_CLASSES_ROOT\Directory\shell\PowershellMenu]
@="Open PowerShell Here"
"Icon"="C:\\\\Windows\\\\SysWOW64\\\\WindowsPowerShell\\\\v1.0\\\\powershell.exe"

[HKEY_CLASSES_ROOT\Directory\shell\PowershellMenu\command]
@="C:\\\\Windows\\\\SysWOW64\\\\WindowsPowerShell\\\\v1.0\\\\powershell.exe -NoExit -Command Set-Location -LiteralPath '%L'"
```

## 终端工具

### terminus

全平台通用。功能强大。

```
#安装
#方法1： https://github.com/Eugeny/tabby
#方法2
scoop install terminus -g 
```



### fluentTerminal

### Xshell



# Onedriver

## 同步任意文件夹

```cmd
#需在cmd内执行
mklink /j "onedrive文件夹地址\需要同步的文件夹名" "需要同步的文件夹地址"
mklink /j "H:\OneDriver\OneDrive - stu.suda.edu.cn\研究生\算法" "H:\算法"
```



# Hexo

## Brew 安装报错

当我们用Homebrew安装应用时，会出现此问题，显示Homebrew无法访问这些位置并添加在OS
X上为您安装软件所需的文件

对于上面问题，我们应尝试回收权限，解决方案如下：
首先打开终端，然后输入：

```shell
sudo chown -R `whoami`:admin /usr/local/bin
```

接着系统会提醒你输入密码,输入密码回车之后接着输入：

```shell
sudo chown -R `whoami`:admin /usr/local/share
```

之后就能在终端中用brew install 安装文件了

## 利用Hexo在多台电脑上提交和更新github pages博客

<https://hexo.io/zh-cn/docs/configuration.html>

[[https://www.jianshu.com/p/0b1fccce74e0?tdsourcetag=s_pcqq_aiomsg]{.ul}](https://www.jianshu.com/p/0b1fccce74e0?tdsourcetag=s_pcqq_aiomsg)

[hexo史上最全搭建教程_Fangzh的技术博客-CSDN博客_hexo](https://blog.csdn.net/sinat_37781304/article/details/82729029)

[[https://www.jianshu.com/p/4bcf2848b3fc]{.ul}](https://www.jianshu.com/p/4bcf2848b3fc)

## 写文章

[[https://blog.csdn.net/weixin_44815733/article/details/88786480]{.ul}](https://blog.csdn.net/weixin_44815733/article/details/88786480)



# docsify

**有了docsify神器，从此爱上看文档**

https://www.jianshu.com/p/4883e95aa903

[官方中文文档](https://docsify.js.org/#/zh-cn/)



# Markdown

## vscode插件

**1.markdown-all-in-one----基础功能+快捷键。
2.markdown toc---生成目录
3.markdown+math--编辑公式
4.Markdown PDF--转为PDF和其他格式
5.Markdown Preview Enhanced-----所以这款是增强显示的。
6.Markdown Shortcuts-----解决复制表格的问题。**

## markdown互转word

### 一键将 Word 转换为 Markdown

<https://www.jianshu.com/p/df6a136d06d8>

### Writage + Pandoc 

1.  下载并安装 Writage，下载地址：http://www.writage.com/

 打开 Writage网页，点击Download，再点击Download Now完成下载
运行安装程序，一般按照默认选项安装就好啦

2. 安装后重启电脑，新建或打开任一 Word 文档，在 文件 菜单栏下选 另存为，查看 **【保存类型】** 中是否有 Markdown 格式。
>如果插件安装成功，就会自动出现Markdown选项；否则，重新安装一遍吧~）


### Word to Markdown Converter在线转换

1.  **设置word文档中的标准样式，如一级、二级标题，项目符号或编号等，如此才能与markdown的格式对应**

（稍微有点繁琐的前期准备，如果文档一开始就是按照标准样式排版，就没有这个烦恼啦）

设置

1. 打开网页Word to Markdown

    > Converter：https://word-to-markdown.herokuapp.com/

2. 选择需要转换的Word文件,点击Convert

3. 大功告成啦！
页面左边显示的是Markdown文档的内容，右边显示的是预览出来的样子

**但还需要进一步手动编辑整理完善表格**

（如果，Word文档本身不包括表格，Word to Markdown
Converter使用体验可谓相当便捷稳妥啦！）

**图片的下载与存储**

除了标准格式设置与表格调整问题，
**图片的下载与存储**也会是我们可能会遇到的问题

-   **Markdown转换为Word**
在Markdown文档中，图片以网络超链接的形式保存,如果markdown文档中有这一类图片，那么需要在网络连接的情况下，才能正常输出有图片的word文档。否则，图片处显示空白

-   **Word转换为Markdown**
Word转换为Markdown文档之后，文档中的图片输出到本地文件夹下，将该文件夹与输出的Markdown文档在同一目录下，在Markdown文档中图片引用本地相对路径，也就是说，必须保证Markdown文档与存放图片的本地文件夹在一起，才能完整的在markdown编辑器中显示图片

### 在线版word2markdown
[https://word2md.com/](https://word2md.com/)

### Ulysses mac支持 纯文本 Markdown2Word ，但付费

目前只研究了Mac下的方案：

1. word-to-markdown，google用word to

markdown搜出来第一个，看来这个名字起得好。用这个的话得装个LibreOffice

1. pandoc，这个就比较大名鼎鼎了

2. unoconv，介绍


链接：https://www.jianshu.com/p/b0be43b03015

## Markdown如何存放图片


### 七牛云

配置

1.  申请七牛云做免费图床

    <https://www.zhihu.com/question/335783774/answer/756830851>

存储空间名称markdown-source-of-bayes

2.  配置插件

    <https://www.codingyang.com/2020/03/getQiniu.html#%E8%8E%B7%E5%8F%96%E5%AF%86%E9%92%A5>

Sm_ms,picGo

### pandoc

```
pandoc -s $infile -t markdown -o $outfile --extract-media=$filename#导出图片到目录下
```

pandoc是文档转换利器。在将docx文档转为md文档过程中，如果直接输入`pandoc
-o f.md f.docx`,会丢失word文档中的图片。输入`pandoc -o f.md f.docx
---extract-media=f `则不会丢失图片。

pandoc语法<https://www.jianshu.com/p/fd761fc43753>

**示例**

```shell
foo $ cat word2md.sh
#!/bin/bash
infile=$1
# echo $infile
filename=$(echo $infile | awk -F '.' '{print $1}')
outfile=${filename}.md
pandoc -s $infile -t markdown -o $outfile --extract-media=$filename
echo "convert success, $outfile "

foo $ bash ./word2md.sh mydoc.docx 

```



### draw.io

draw.io 绘图可以导出成 HTML，而 markdown 是支持直接嵌入 HTML 的

点击图形中的全屏按钮，再点击编辑，居然还可以直接修改原图的副本。厉害了！

具体插入的方法是，打开 draw.io 导出的 HTML
文件，将其中的 <body> 中的内容复制出来即可（不包含` <body>`标签）。**github不支持解析**

### picGo+GitHub 上传图片

Typora批量上传图片

<https://www.cnblogs.com/zenglintao/p/12876725.html>

图床配置

<https://blog.csdn.net/qq_43367829/article/details/104882071>

注意 创建的GitHub图床默认分支为main,没有master分支，


# 开发养成
编程中最难的事：如何优雅地为程序中的变量和函数命名
命名不一致解决思路：
https://www.zhihu.com/question/395223359
https://www.douban.com/note/571297448/
(创建中间层，添加注解@)
工具
https://graphql.org/，TypeScrip


python – 解析一个.py文件,读取AST,修改它,然后回写修改后的源代码http://www.voidcn.com/article/p-mvtnzhha-bsk.html


统一纠正变量名
读取各项目ast，对每个变量计算编辑距离，编辑距离为0~len(word) 为一类
批量更正变量并写回去

# 工具

## 科学上网

[2021年最新Clash For Windows 详细使用教程 - 笨猫博客 (nbmao.com)](https://www.nbmao.com/archives/4463)

[登录 — GW树洞 (hello-shudong.com)](https://hello-shudong.com/auth/login)

## 电脑维护

- CCleaner
- SpaceSniffer
- Geek
- Snipaste



## 数据标注

1. labelImg

https://github.com/tzutalin/labelImg

使用

```shell
#1.环境配置
brew install qt  # Install qt-5.x.x by Homebrew
brew install libxml2
#or using pip
pip3 install pyqt5 lxml # Install qt and lxml by pip

#2.配置labelimg
git clone https://hub.fastgit.org/tzutalin/labelImg.git
cd labelImg
make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```



2. **Yolo_mark**

**Windows**和**Linux** GUI，用于在图像中标记对象的边界框，以训练Yolo v3和v2

https://github.com/AlexeyAB/Yolo_mark

其他

深度学习图像标注工具汇总

https://blog.csdn.net/chaipp0607/article/details/79036312



浏览器 PDF 预览及打印（效果很棒）

https://www.printfriendly.com/

Send Anywhere

Send Anywhere官方版是款支持多种平台的文件传输共享工具。

Send Anywhere最新版主打网络传输文件，支持安卓、iOS、windows、macOS、Linux以及Windows Phon。Send Anywhere几乎能可以将你所有的电子设备全部打通!你甚至在电脑上无需安装任何APP，直接通过Chrome、Firefox、Safari或IE浏览器即可与手机收发文件。

1、bandzip（解压 window）
2、ditto（复制剪贴板window）
3、shareX（截图window）

https://getsharex.com/

4、everthing（找文件）
5、uTools（百宝箱）
6、IDM（下载）
7、RST（硬盘优化）
8、VS Code（编辑器）
9、天翼云盘（网盘）
10、chrome（浏览器）
11、quicker（鼠标党助手 window,chrome插件）

https://getquicker.net/Download

FilePane for Mac 是一款轻量级，多功能的文件快速复制粘贴工具，功能上同之前分享过的 [PopClip](https://www.macsky.net/22701.html) 类似，可用于快速管理文件。它适用于系统中任何应用程序的几乎任何可选择和可拖动内容，并根据您提供的数据建议各种快速操作。您可以轻松复制/移动/创建文件和文件夹，编辑/共享/转换图像等等。

Chrome插件

① 百度药丸

使用更纯净的百度 1.屏蔽百度广告推广 2.阻止百度追踪 3.支持居中显示治愈偏头痛

②onetab

能把所有打开的网页/标签页一键「全部关闭」并「保存成列表」，你随后可以一个个 (或一次性全部) 恢复它们。这样不仅变相实现了释放和回收浏览器占用的内存、解决 CPU 资源占用问题、让系统和浏览器的速度恢复正常，而且还能将打开的网页全部保存下来备用。

**Session Buddy**插件功能介绍

很多人应该都知道，Chrome 虽然也有内置的Session Manager，但是功能什么的简单。Session Buddy 扩展提供的功能为暂存标签，会自动记录已经关闭的标签，当然你可以手动点击保存，下次需要时调用。至于节省内存开销，这事还是交给 Google 来做吧。

当然具有类似功能的插件，我们网站之前也有介绍过一些：

> 2.[TAb Hibernation](http://www.cnplugins.com/fuzhu/tab-hibernation/):可以将我们目前未使用到的网页进入休眠，让这些分页暂时不占用内存，但我们需要使用时，按一下就可以唤醒，解决内存不足的问题.
> 3.[The Great Suspender](http://www.cnplugins.com/office/the-great-suspender/):可以让你把不需要的标签进入睡眠模式以节省内存，保证流畅的浏览体验。不同于其他类似扩展，The Great Suspender 提供两种休眠方式： 手动休眠、或者一段时间不使用自动休眠。扩展还支持白名单，无论自动休眠还是手动休眠，白名单中的网站是不会休眠的.

③喵喵折

购物助手

④搜图助手

奇妙加速器，免费https://www.qimiao.com/

网页版文件快传

https://snapdrop.net/

快传 ：Feem和AirDroid

**Linux远程拷贝工具(WinSCP)**

https://blog.csdn.net/dengjin20104042056/article/details/97378487

## 论文工具

LaTeX新手入门以及TeXlive和TeXstudio的安装使用https://blog.csdn.net/zywhehe/article/details/83113214
TeX Live 下载及安装说明(mac 和window)
https://www.latexstudio.net/archives/10208.html
https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/mac/mactex/

VS Code + LaTeX
https://zhuanlan.zhihu.com/p/144729565

一般来讲，LaTeX装好后默认的编译方式是pdflatex，但是这种方式不能编译中文源码。对于中文源码，采用的是xelatex的编译方式。对于编译中文文档有两种方式，第一种：在中文源文件首行添加：% !TEX program = xelatex，如果有参考文献，可以再添加% !BIB options = "%DOCFILE%"。显然，这个操作不够智能，因此，我们第一步是，添加xelatex的编译方式(2.3节)。

[AUCTeX+Emacs 是目前我见过的能最大限度提高 LaTeX 编辑效率的编辑器 （转）_芝兰生于深谷，不以无人而不芳-CSDN博客](https://blog.csdn.net/wdkirchhoff/article/details/41707157)

Mendeley－一款免费好用的文献管理软件
https://zhuanlan.zhihu.com/p/28762628
自动插入参考文献，史上最简Endnote教程！！#论文写作+Endnote X8安装文件http://www.xszydq.com/17326.html

翻译狗：[登录-Word翻译,Pdf翻译,文献论文翻译-翻译狗 (fanyigou.com)](https://www.fanyigou.com/trans/login.html?code=6ZH3PQVY0F)





### 论文查询

1. **[谷歌学术](https://link.zhihu.com/?target=https%3A//scholar.google.com.hk/%3Fhl%3Dzh-CN)**：谷歌大概是最友好的一个平台了，尤其是在国外的校内网中使用谷歌学术。
2. **[百度学术](https://link.zhihu.com/?target=https%3A//xueshu.baidu.com/)**：这大概是百度产品中，算是非常良心的一个了，不能用谷歌的话，百度顶上吧。
3. **[中国知网](https://link.zhihu.com/?target=http%3A//www.cnki.net/)**：知网是国内比较不错的平台，可在境外的话，会遇到IP限制，大概是超过国内许可范围了。
4. **[Sci-Hub](https://zhuanlan.zhihu.com/p/24299207)**：这个比较有趣，大家可以配合知网来使用，从知网搜寻论文，然后在Sci-Hub中下载。但你懂的，Sci-Hub的地址经常变动，所以需要的时候直接用搜索引擎吧。
5. **[喵咪论文 - 简单自由的论文下载平台](https://link.zhihu.com/?target=https%3A//lunwen.im/)**：亲自试了一下，使用起来还是很方便的，但是随手测试了一下，论文查找到的概率也不是太大。
6. [国家哲学社会科学文献中心](https://link.zhihu.com/?target=http%3A//www.ncpssd.org/index.aspx): 如果是中文的论文，那用这个查看也还行，主要是界面比知网要人性化一些。
7. https://papers.labml.ai/papers/monthly/
8. [Google 学术搜索](https://scholar.google.com.hk/schhp?hl=zh-CN)
9. [大木虫学术导航 (4243.net)](http://www.4243.net/)：<font color=red>功能极其强悍</font>

另外就是一些不错的期刊：

1. **[Science官网](https://link.zhihu.com/?target=https%3A//www.sciencemag.org)**
2. **[Science | AAAS](https://link.zhihu.com/?target=https%3A//www.sciencemag.org)**

### 论文撰写

officeTab：模仿WPS多个文章同时显示

word小恐龙： http://gw.xkonglong.com/

word精灵

grammarly ：语法纠正

[Paraphrasing Tool | QuillBot AI](https://quillbot.com/)：句子重构，降低查重

[Academic Phrasebank | The University of Manchester](https://www.phrasebank.manchester.ac.uk/)：论文例句

[论文查重软件_论文检测软件_笔杆网 (bigan.net)](https://www.bigan.net/check/)

[写个论文 - 论文降重神器，写论文更简单 (xiegelunwen.com)](https://www.xiegelunwen.com/#/zhllc)

### 论文管理

**Readcube**：这是一个付费的管理软件，这里有一篇介绍Readcube的文章，[高效率科研神器——驾驭文献洪流](https://link.zhihu.com/?target=https%3A//www.jianshu.com/p/6bf14803dc99)，有需要可以继续了解一下。

EndNote 是SCI（Thomson Scientific 公司）的官方软件，自身具有强大的功能，**是一款集文献检索、文摘及全文管理、文献共享等功能于一身的老牌软件**

Citavi有**全功能免费版（支持每个项目插入不多于100篇文献）**，具有**强大的参考文献编辑功能，**可以从各个方面实现对参考文献的编辑需求。

Citavi很大一个特点是**支持PDF阅读功能，且可以支持多种批注格式**

Mendeley是一款Elsevier公司旗下的**免费文献管理软件，**所有人都可以在Mendeley上搜索到世界各地的学术文献，这些学术文件都是由用户自己上传到Mendeley“library”进行编辑管理，**这款软件拥有整理组织文献、PDF标记和文件分享、网络备份的强大功能。**（其余工具见[研究生必备文献整理工具 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/105066833)）

noteexpress：对中文支持更全面，但对英文文献不太靠谱

Zotero：最大特点是浏览器的抓取功能异常强大。



**总结：首推citavi**

### 开题相关工具

如果要快速了解某个领域，那需要大量阅读该领域的相关文献，才能了解到以下：

1. 这个领域的研究热点、主要研究内容、权威的学者等
2. 研究存在的不足
3. 对自己而言，该从哪个领域进行切入才有研究意义等

这里我直接根据知乎的回答来推荐工具：

**[CiteSpace](https://link.zhihu.com/?target=http%3A//cluster.ischool.drexel.edu/~cchen/citespace/download/)**：这是一个可视化软件，可以将下载的论文进行CiteSpace分析，让你能够尽快地了解领域的发展情况。

**[Histcite](https://zhuanlan.zhihu.com/p/20902898)**：这是一款非常强大的引文分析工具，可以快速绘制出某个研究领域的发展脉络，快速锁定某个研究方向的重要文献和学术大牛，还可以找到某些具有开创性成果的无指定关键词的论文。

**[百度开题](https://link.zhihu.com/?target=http%3A//xueshu.baidu.com/u/biye%3Ffr%3Dkaiti301)**：这里必须隆重介绍一下这个百度开题，其使用简单，效果也比较炫酷，是开题不可多得的工具。

### 英文文献翻译

这里要推荐一个网站，叫tongtianta.site，[网站](https://link.zhihu.com/?target=http%3A//www.tongtianta.site/)功能很简单： 对论文进行翻译，中英文对照阅读

## 中国计算机学会推荐国际学术期刊 

**(**数据库**/**数据挖掘**/**内容检索**)**

一、**A** 类 

| 序号 | 刊物简称 | 刊物全称                                             | 出版社   | 网址                                       |
| ---- | -------- | ---------------------------------------------------- | -------- | ------------------------------------------ |
| 1    | TODS     | ACM  Transactions on Database Systems                | ACM      | http://dblp.uni-trier.de/db/journals/tods/ |
| 2    | TOIS     | ACM  Transactions on Information Systems             | ACM      | http://dblp.uni-trier.de/db/journals/tois/ |
| 3    | TKDE     | IEEE  Transactions on Knowledge and Data Engineering | IEEE     | http://dblp.uni-trier.de/db/journals/tkde/ |
| 4    | VLDBJ    | The  VLDB Journal                                    | Springer | http://dblp.uni-trier.de/db/journals/vldb/ |

https://icde2021.gr/accepted-papers/
http://vldb.org/pvldb/vol14-volume-info/

https://kdd.org/kdd2021/accepted-papers/index
https://sigir.org/sigir2021/accepted-papers/

二、**B** 类 

| 序号 | 刊物简称                                              | 刊物全称                                                     | 出版社                                                       | 网址                                                 |
| ---- | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------------------- |
| 1    | TKDD                                                  | ACM  Transactions on Knowledge   Discovery  from Data        | ACM                                                          | http://dblp.uni-trier.de/db/journals/tkdd/           |
| 2    | TWEB                                                  | ACM  Transactions on the Web                                 | ACM                                                          | http://dblp.uni-trier.de/db/journals/tweb/           |
| 3    | AEI                                                   | Advanced  Engineering Informatics                            | Elsevier                                                     | http://dblp.uni-trier.de/db/journals/aei/            |
| 4    | DKE                                                   | Data  and Knowledge Engineering                              | Elsevier                                                     | http://dblp.uni-trier.de/db/journals/dke/            |
| 5    | DMKD                                                  | Data Mining and Knowledge Discovery                          | Springer                                                     | http://dblp.uni-trier.de/db/journals/datamine/       |
| 6    | EJIS                                                  | European  Journal of Information   Systems                   | Springer                                                     | http://dblp.uni-trier.de/db/journals/ejis/           |
| 7    |                                                       | GeoInformatica                                               | Springer                                                     | http://dblp.uni-trier.de/db/journals/geoinformatica/ |
| 8    | IPM                                                   | Information  Processing and Management                       | Elsevier                                                     | http://dblp.uni-trier.de/db/journals/ipm/            |
| 9    |                                                       | Information  Sciences                                        | Elsevier                                                     | http://dblp.uni-trier.de/db/journals/isci/           |
| 10   | [IS](http://www.dimva.org/)[ ](http://www.dimva.org/) | Information  Systems                                         | [Elsevier](http://www.gi-fg-sidar.de/)[ ](http://www.gi-fg-sidar.de/) | http://dblp.uni-trier.de/db/journals/is/             |
| 11   | JASIST                                                | Journal  of the American Society for Information Science and Technology | American  Society for   Information  Science and Technology  | http://dblp.uni-trier.de/db/journals/jasis/          |
| 12   | JWS                                                   | Journal  of Web Semantics                                    | Elsevier                                                     | http://dblp.uni-trier.de/db/journals/ws/             |
| 13   | KAIS                                                  | Knowledge  and Information Systems                           | Springer                                                     | http://dblp.uni-trier.de/db/journals/kais/           |

## 其他

https://www.zhihu.com/question/22867411

- Dash

  官网地址 ：https://kapeli.com/dash
  Dash for mac是使用与Mac OS平台的软件编程文档管理工具，可以浏览API文档，以及管理代码片段工具。Dash自带了丰富的API文档，涉及各种主流的编程语言和框架。（190元）

- mathpix

  https://mathpix.com/

  图片转LaTeX公式，适用于Markdown,word等文档

- tmux/tmuxp。比screen好用，可以用来分屏，托管进程等，服务器端必备神器，ubuntu下基本就不用使用terminator之类的分屏工具了。最近看youtube视频还发现有人在服务器上使用tmux和vim结对编程，两个人同时attach到一个session里，基情四射。

- wemux: tmux 共享，[https://github.com/zolrath/wemux](https://link.zhihu.com/?target=https%3A//github.com/zolrath/wemux)

- sshfs: 本地挂在服务器文件夹

- tmate: [https://tmate.io](https://link.zhihu.com/?target=https%3A//tmate.io/) 终端共享工具，结对编程。很多现代化编辑器 vscode, atom 提供结对编程的插件。

- asciinema: 终端会话记录工具。[https://asciinema.org/](https://link.zhihu.com/?target=https%3A//asciinema.org/)

- oh-my-zsh。替代原生的bash shell，提供了好多方便的特性和漂亮主题，支持插件。linux/mac下vim+tmux+zsh简直是绝配，甚至可以直接在服务器上方便地撸代码，跟本地开发体验没区别。

- item2(mac)。替代原生的终端。[https://medium.com/@RyanDavidson/make-your-terminal-more-colourful-and-productive-with-iterm2-and-zsh-11b91607b98c](https://link.zhihu.com/?target=https%3A//medium.com/%40RyanDavidson/make-your-terminal-more-colourful-and-productive-with-iterm2-and-zsh-11b91607b98c)

- brew(mac)。类似ubuntu下的apt-get，可以方便安转各种软件和工具。

- Alfred(mac): mac 下一款功能强大的工具，不过我一般只用它快速打开软件。可以用 python 编写一些自己的 workflow 提高效率([https://github.com/deanishe/alfred-workflow](https://link.zhihu.com/?target=https%3A//github.com/deanishe/alfred-workflow))，比如把时间戳转成日期等。 [https://github.com/derimagia/awesome-alfred-workflows](https://link.zhihu.com/?target=https%3A//github.com/derimagia/awesome-alfred-workflows)

- Dash(mac,全英): 强悍的文档查询工具。支持非常多编程语言和框架

- devdocs.io: 文档查询工具

- Zeal——好用的离线 API 文档大全！(支持window，Linux，https://www.cnblogs.com/souldee/p/9523497.html，feed：[Zeal User Contributions & Cheat Sheets](https://zealusercontributions.vercel.app/))

- Karabiner-Elements(mac): 改键工具 [https://github.com/tekezo/Karabiner-Elements](https://link.zhihu.com/?target=https%3A//github.com/tekezo/Karabiner-Elements)

- autojump。方便在命令行里来回跳转目录。

- gitx(mac):方便查看代码提交历史，便于了解整个代码仓库是怎样一步步构建的。[http://gitx.frim.nl/user_manual.html](https://link.zhihu.com/?target=http%3A//gitx.frim.nl/user_manual.html)

- tig: text-mode interface for git. 喜欢命令行的可以尝试下。 [https://github.com/jonas/tig](https://link.zhihu.com/?target=https%3A//github.com/jonas/tig)

- tldr: 更好的man手册

- YouCompleteMe: vim 代码补全https://blog.csdn.net/weixin_44638957/article/details/91985270

- EditorConfig: [http://editorconfig.org/](https://link.zhihu.com/?target=http%3A//editorconfig.org/) 用来统一编辑器配置。如果成员用不同的操作系统和编辑器，建议使用。尤其是对于 python 这种使用缩进的语言

- mac-setup: [https://github.com/sb2nov/mac-setup](https://link.zhihu.com/?target=https%3A//github.com/sb2nov/mac-setup) mac 下各种编程语言开发环境配置指引

- pdf2go网址：https://www.pdf2go.com/zh 免费PDF工具

- ilovePDF网址：https://www.ilovepdf.com/zh-cn 免费PDF工具

- temp-mail网址：https://temp-mail.org/ 临时邮箱，避免垃圾广告

# 机器学习
## 课程&资料
【链接】最值得看的十大机器学习公开课
https://blog.csdn.net/yushupan/article/details/78582630

【链接】计算机视觉有哪些比较好的公开课？补充计
https://www.zhihu.com/question/35831904

机器学习与生成对抗网络https://my.oschina.net/u/4579551/blog/4350931

分类机器学习中，某一标签占比太大（标签稀疏），如何学习？https://my.oschina.net/u/4579551/blog/4750226

使用深度学习的图像分类-Koko.PDF
https://max.book118.com/html/2018/1016/7123041051001153.shtm

pandas官方中文文档-草鸡详细！！！！https://www.pypandas.cn/deep/basics/image_classification.html#%E8%83%8C%E6%99%AF%E4%BB%8B%E7%BB%8D

汇总】CV 图像分类常见的 36 个模型
https://my.oschina.net/u/4579551/blog/4701954

超详细！！！
http://www.feiguyunai.com/

Jupyter Notebook介绍、安装及使用教程
https://www.jianshu.com/p/91365f343585
https://blog.csdn.net/u013709332/article/details/105029123/


Python深度学习 基于TensorFlow 在线版
http://www.feiguyunai.com/index.php/2018/05/26/python-ml-tf-01/

机器学习 几百篇文章
https://blog.csdn.net/GarfieldEr007/category_5619819.html

零基础学习-深度学习核心-梯度下降与最优化
http://www.feiguyunai.com/index.php/2017/11/08/pythonai-dl-grade01/

给大家再分享几个好用的知识文章检索工具哦：[OK]
1、https://www.cn-ki.net/ 仿知网
2、https://www.jiumodiary.com/ 鸠摩搜索

实在不行就用这个狗屁不通文章生成器[doge]
https://suulnnka.github.io/BullshitGenerator/index.html

**神经网络与深度学习**

https://nndl.github.io/

# C++入门教程

http://www.weixueyuan.net/cpp/rumen//e
