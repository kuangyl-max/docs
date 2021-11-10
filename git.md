[TOC]



# Git

## git命令交互式学习

https://www.liaoxuefeng.com/wiki/896043488029600

https://blog.csdn.net/u014734886/article/details/79527710

<https://learngitbranching.js.org/?locale=zh_CN>

示例：
![](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-17-19-cbcb88da5f3b55ab6a6bb41c1019e995-image15-1fbb47.png){width="5.540972222222222in"
height="2.9277777777777776in"}

## Git ssh 配置：

<https://www.cnblogs.com/anyefrozen/p/6379046.html>

<https://blog.csdn.net/lqlqlq007/article/details/78983879>

https://blog.csdn.net/lilygg/article/details/97919376?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control



## 疑难

### git下载仓库内单个文件夹内容

> git学习之git clone 克隆或下载一个仓库单个文件夹有时候因为需要我们只想gitclone下仓库的单个或多个文件夹，而不是全部的仓库内容，这样就很省事，所以下面就开始教程啦
> 在Git1.7.0以前，这无法实现，但是幸运的是在Git1.7.0以后加入了Sparse Checkout模式，这使得CheckOut指定文件或者文件夹成为可能。

**现有一个test仓库https://github.com/mygithub/test**
**你要gitclone里面的 childfile 子目录：**
**在本地文件夹位置打开Git Bash 进行一下步骤**

###### 步骤：

代码直接复制即可用

```shell
#'childfile'替换为自己要下载的文件夹名称
git init test && cd test     #新建仓库并进入文件夹
git config core.sparsecheckout true #设置允许克隆子目录
echo 'childfile*' >> .git/info/sparse-checkout #设置要克隆的仓库的子目录路径   
git remote add origin git@github.com:mygithub/test.git  #这里换成你要克隆的项目和库
git pull origin master    #下载
```

### git clone 太慢

原有git链接

`https://github.com/someone/repo.git`

改为如下链接之一

- `https://hub.fastgit.org/someone/repo.git`

- `https://gitclone.com/github.com/someone/repo.git`

- `https://github.com.cnpmjs.org/someone/repo.git`

例如

```shell
git clone https://hub.fastgit.org/someone/repo.git
#或者-空白文件夹
git init 
git remote add origin https://hub.fastgit.org/someone/repo.git

#或者-git文件夹
git remote remove origin
git remote add origin https://hub.fastgit.org/someone/repo.git

#如果需要用完再改回到原来的git链接，可以先执行
git remote -v
#记录下git链接，之后恢复即可
```



### Github如何上传超过100M的大文件

https://jingyan.baidu.com/article/48b558e3eea2697f38c09a98.html

安装git - lfs到本机

![image-20201205180543710](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/typora-user-images/2020/12/05/18-05-51-79d11f189c72f852cb064dc6dc0668d8-image-20201205180543710-724945.png) 

![学习笔记-20201205180641-2020-12-05-18-06-43](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205180641-2020-12-05-18-06-43.png)

选择您希望Git LFS管理的文件类型（或直接编辑.gitattributes）。您可以随时配置其他文件扩展名。这一步成功后会生成一个gitattributes文件

![学习笔记-20201205180715-2020-12-05-18-07-16](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205180715-2020-12-05-18-07-16.png)
 添加并commit gitattributes文件

![学习笔记-20201205180740-2020-12-05-18-07-40](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205180740-2020-12-05-18-07-40.png)
然后再添加大文件到本地缓存区

![学习笔记-20201205180754-2020-12-05-18-07-55](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205180754-2020-12-05-18-07-55.png)
 这里要注意一点：以上是官网步骤，我没这样走。如果你按照以上步骤走的话会还是会出现push fail(如下图)的情况，可参考我的解决办法。

![学习笔记-20201205180805-2020-12-05-18-08-06](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205180805-2020-12-05-18-08-06.png)


参考解决办法：



1-2步没变，第3步我是生成.gitattributes后 add并且commit并且把.gitattributes文件push到远程分支，合并完成后，然后再add并且commit然后再push这个大文件.



简单说，就是我先把这个.gitattributes跟踪文件提交上传到远程，再把大文件提交并上传到远程的，这个要注意顺序。



有的同学已经把大文件提交了，但是.gitattributes还没有提交，这种情况需要回滚版本，具体操作可以参考廖雪峰 - 版本回退

### git lfs的使用
  https://www.cnblogs.com/mianbaoshu/p/10972254.html


#### 1.什么是git lfs

Git LFS（Large File Storage, 大文件存储）是可以把音乐、图片、视频等指定的任意文件存在 Git 仓库之外，而在 Git 仓库中用一个占用空间 1KB 不到的文本指针来代替的小工具。通过把大文件存储在 Git 仓库之外，可以减小 Git 仓库本身的体积，使克隆 Git 仓库的速度加快，也使得 Git 不会因为仓库中充满大文件而损失性能。

#### 2.优点是什么

git每次保存diff，一些大文件发生变化时，整个仓库就会增加很大的体积，导致clone和pull的数据量大增。对于`git lfs`来说，在使用`git lfs track`命令后，git push的时候，`git lfs`会截取要管理的大文件，并将其传至`git lfs`的服务器中，从而减小仓库的体积

#### 3.怎么安装

注意：git lfs 要求 git >= 1.8.2

Linux
```shell
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash

sudo apt-get install git-lfs

git lfs install
```

Mac
```shell
#安装HomeBrew /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install git-lfs

git lfs install
```

#### 4.怎么使用

1. 查看现有的文件追踪模式：`git lfs track`

2. 添加要管理的大文件的文件类型，比如gz文件

运行命令：`git lfs track *.gz`添加类型后，查看管理文件.gitattributes，可以发现.gitattributes中新增加一行：`*.gz filter=lfs diff=lfs merge=lfs -text`

3. 将管理文件.gitattributes提交至仓库. 它保存了文件的追踪记录

4. 获取git lfs管理的所有文件列表：git lfs ls-files 

5. 添加大文件到git仓库，和其它添加方式一样
```
  git add my.gz
  git commit -m "add gz file"
  git push
```

6. 将代码 push 到远程仓库后，LFS 跟踪的文件会以『Git LFS』的形式显示:
7. clone 时 使用'git clone' 或 `git lfs clone`均可
8. 查看Git LFS 的帮助：git lfs help
9. 下载被git lfs管理的文件

```shell
$ git lfs fetch
$ git lfs checkout
# 或
$ git lfs pull
```

10. 删除lfs里的文件

如果需要删除lfs里的文件，需要在gitee后台操作，先到后台里查看文件的oid

![删除lfs](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/abnerworks.Typora/2020/12/13/09-43-36-1e86b868bb36524bef9ae76be9b53dd3-watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RkZGQ2NjY2cXE=,size_16,color_FFFFFF,t_70-c7a109.png)

然后在本地通过下面命令判断是否是能删除的文件，然后在后台操作删除

```shell
$ git log --all -p -S 8a9c160e
```

**删除文件后本地分支上传时可能的报错**

```shell
Unable to find source for object a0ee616e6195bcb5f4136fb36b6b803566cec234f4468bda64e42a34a5f76697 (try running git lfs fetch --all)
Uploading LFS objects:   0% (0/20), 0 B | 0 B/s, done.
```

查了下这个文件是前面我删除的文件，我想要的结果是忽略这个文件接着上传，可以设置下面这个属性

```shell
$ git config lfs.allowincompletepush true
```

> git lfs track **/*.zip 任意子目录的zip文件

**参考文档**

- [Git LFS 操作指南](https://gitee.com/help/articles/4235#article-header0)

### 删除远程lfs大文件

一些时候由于开发初期经验不足和贪图方便, 会把一些不应该提交到 Git 的文件上传到 Github, 带来一系列安全问题, 更有可能是把一些大文件上传到 GitHub 上, 导致项目非常臃肿, 每次 pull、push 都要花费很多时间.

这时候就可以寻求一些特殊的工具的帮助, [BFG Repo-Cleaner by rtyley ](https://rtyley.github.io/bfg-repo-cleaner/)就是这样一款工具, 可以从 Git 项目中彻底删除某一个文件的历史记录.

**下载及运行**

[BFG Repo-Cleaner ](https://rtyley.github.io/bfg-repo-cleaner/)是由 Scala (一种JVM语言) 写成, 所以会被编译成 jar 包, 下载非常方便, 下载地址可在官网或直接点击 [bfg 下载地址 ](https://search.maven.org/classic/remote_content?g=com.madgag&a=bfg&v=LATEST).

但因此运行 `bfg.jar` 就需要 Java 环境, 关于 Java 环境的安装, macOS可以参考 [macOS 的 JDK 安装问题 ](https://www.cnblogs.com/imzhizi/p/macos-jdk-installation-homebrew.html), 而 Windows 已经有很多人提过, 不做赘述.

```shell
#使用brew安装配置
brew cask install oracle-jdk
brew install bfg
```

**让它完全消失**

1. 首先需要自行从项目中删除不想要的文件并提交, 这样能最大程度避免误删、误操作.

```bash
# 首先需要自行从项目中删除不想要的文件
rm file-to-delete

# 提交改动, 即最新分支是不包含要被删除的文件
git commit -m "删除 file-to-delete"
git push
```

2. 然后使用 `--mirror` 命令裸克隆(clone)整个项目.

```bash
git clone --mirror git@github.com:username/some-project.git

# 根据经验, 如果是包含大文件的项目, 使用 ssh 将会克隆的非常缓慢, 可以改用 https
git clone --mirror https://github.com/username/some-project.git

# 这个时候, 你的当前目录下就会产生一个名为 some-project.git 的文件夹
```

3. 接着开始删除文件历史.

```bash
#根据情况的不同, bfg 可选择根据文件大小删除
java -jar bfg.jar --strip-blobs-bigger-than 100M some-project.git

#根据情况的不同, bfg 可选择直接根据名字删除
java -jar bfg.jar --delete-files name-of-file  some-project.git
```

> 命令中java -jar bfg.jar 可以用bfg代替

4. 任选以上命令执行其中一个后, 执行 `git gc` 真正删除这些文件并提交.

```bash
cd some-project.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push
```

这时候那个文件就会消失了…



参考链接：

- https://rtyley.github.io/bfg-repo-cleaner/

- [git filter-branch：](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository)



### git clone大文件EOF错误

我们常用的`git clone https://XXX `下载大文件时，加上墙的问题。会出现中断

```shell
git clone https://gitlab.com/xhang/gitlab.git

正克隆到 'gitlab'...

remote: Counting objects: 451995, done.

remote: Compressing objects: 100% (96627/96627), done.

fatal: The remote end hung up unexpectedlyB | 34.00 KiB/s

fatal: 过早的文件结束符（EOF）

fatal: index-pack failed
```

**解决一：采用ssh方式**

```shell
git clone git@gitlab.com:xhang/gitlab.git
```

**解决二：加大https缓存（推荐）**

```shell
git init 
git config http.postBuffer 524288000
```

### 如何控制git库的膨胀？

根据 Git 的数据存储机制，只要通过命令 git add 将文件存储至暂存区，都会对版本库中的每一个文件，不论是图片、视频、源文件还是二进制文件生成相对应的 Blob 对象（即一段二进制数据。可以类比为**url编码，**通过加解码获得内容信息）。

如果你的项目中不小心打包进来了比较大的 word 文档或视频资源，Git 本身又识别不了该类型文件，只能当作二进制文件全量存储。所以，在其他人拉取该 word 文档更新完后再推远程分支的时候，则会使得 .git 下面的 objects 的文件夹大小迅速膨胀。

**注：如果是文本或代码等 Git 可以识别的文件，则只会存储有差异的文件。**

上面使用场景中表面上少了500M空间，实则增加了一次至少500M的历史提交记录，仓库容量反而变得更臃肿。

### github重置仓库

**执行之前本地要有备份！！！！**

1. 在你的仓库中点击setting

   ![image-20210107132654116](../../../../Library/Application Support/typora-user-images/image-20210107132654116.png)

1. 点击Delete this repository![image-20210107132756513](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/typora-user-images/2021/01/07/13-27-58-f6bfb78a8b4aac4ac07cefedd25bdc5c-image-20210107132756513-207804.png)

1. 重新创建个同名厂库

1. 本地执行

   ```
   rm -rf .git
   git init 
   git add .
   git commit -m "init repos"
   git remote addd origin https://hub.fastgit.org/yourname/your-repos.git
   git push -f origin master
   ```

注意，如果提示

```
error: RPC 失败。HTTP 413 curl 22 The requested URL returned error: 413
fatal: 远端意外挂断了
fatal: 远端意外挂断了
```

可以尝试以下步骤

1. 

```
#1.查看http.postbuffer （如果没有设置，默认值是1兆，确认目前值确实较小）
git config --list
#2.设置http.postbuffer ，单位byte
git config http.postBuffer 524288000 #（512MB）
#3.如果还是无法解决问题，将ssl验证禁止
git config http.sslVerify "false"
```

> 禁止ssl也可在克隆时执行`env GIT_SSL_NO_VERIFY=true git clone https://<host_name/git/project.git `

2. 或者更换为ssh链接

```
git remote rm origin
git remote add origin git@github.com:yourname/your-repos.git
```

参考

https://www.cnblogs.com/babysbreath/p/7118414.html

https://jingyan.baidu.com/article/6b97984d7582d75da2b0bf93.html

### 如何精简你的 Git 仓库？

**第一种方案：压缩 Git 仓库。**

例如，码云项目管理中会提供存储库 GC 功能，用于清理悬空文件，压缩存储库对象，减少存储库磁盘占用。

![img](https://pic1.zhimg.com/v2-fa1b0b20624cd7f8c31f2879e6c2820d_r.jpg?source=1940ef5c)



**第二种方案（推荐）：删除大文件提交记录。**

查看存储库中的大文件：

```text
git rev-list --objects --all | grep -E `git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -10 | awk '{print$1}' | sed ':a;N;$!ba;s/\n/|/g'`
```

改写历史，去除大文件

```text
git filter-branch --tree-filter 'rm -f path/to/large/files' --tag-name-filter cat -- --all
git push origin --tags --force
git push origin --all --force
```

并告知所有组员，push 代码前需要 pull rebase，而不是 merge，否则会从该组员的本地仓库再次引入到远程库中。

**.git文件过大，github仓库瘦身**

https://blog.csdn.net/luchengtao11/article/details/82531044?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

**查看git仓库大文件并删除**

https://blog.csdn.net/wenqibiao8/article/details/81263751

### git add详解

 一、前言
git add命令主要用于把我们要提交的文件的信息添加到索引库中。当我们使用git commit时，git将依据索引库中的内容来进行文件的提交。

查看git add 内容 git status
二、基本
`git add <path>`表示 add to index only files created or modified and not those deleted 
我通常是通过`git add <path>`的形式把我们`<path>`添加到索引库中，`<path>`可以是文件也可以是目录。
git不仅能判断出`<path>`中，修改（不包括已删除）的文件，还能判断出新添的文件，并把它们的信息添加到索引库中。
三、`git add -u`
`git add -u ` 表示 add to index only files modified or deleted and not those created 
`git add -u [<path>]`: 把<path>中所有tracked文件中被修改过或已删除文件的信息添加到索引库。它不会处理untracted的文件。
省略<path>表示.,即当前目录。
四、`git add -A`
`git add -A: [<path>]`表示把<path>中所有tracked文件中被修改过或已删除文件和所有untracted的文件信息添加到索引库。
省略<path>表示.,即当前目录。
五、`git add -i`
我们可以通过`git add -i [<path>]命`令查看<path>中被所有修改过或已删除文件但没有提交的文件，
并通过其revert子命令可以查看`<path>`中所有untracted的文件，同时进入一个子命令系统。
比如：
```
 git add -i
      staged   unstaged path
 1:    +0/-0   nothing branch/t.txt
 2:    +0/-0   nothing branch/t2.txt
 3:  unchanged    +1/-0 readme.txt
```

*** Commands ***
```
 1: [s]tatus   2: [u]pdate   3: [r]evert   4: [a]dd untracked
 5: [p]atch   6: [d]iff    7: [q]uit    8: [h]elp
```
What now>
这里的t.txt和t2.txt表示已经被执行了git add，待提交。即已经添加到索引库中。
readme.txt表示已经处于tracked下，它被修改了，但是还没有被执行了git add。即还没添加到索引库中。
5.1、revert子命令
可以通过`git add -i`的revert子命令（3: `[r]evert`）把已经添加到索引库中的文件从索引库中剔除。
（`3: [r]evert`）表示通过3或r或revert加回车执行该命令。执行该命令后，git会例出索引库中的文件列表.
然后通过数字来选择。输入"1"表示git会例出索引库中的文件列表中的第1个文件。
"1-15"表示git会例出索引库中的文件列表中的第1个文件到第15个文件.回车将执行。
如果我们不输入任何东西，直接回车，将结束revert子命令，返回git add -i的主命令行。
5.2、update子命令
可以通过update子命令（2: `[u]pdate`）把已经tracked的文件添加到索引库中。其操作和revert子命令类似。
5.3、add untracked子命令
通过add untracked子命令（4: `[a]dd untracked`）可以把还没被git管理的文件添加到索引库中。其操作和revert子命令类似。
5.4、diff子命令
可以通过diff子命令（6: `[d]iff`）可以比较索引库中文件和原版本的差异。其操作和revert子命令类似。
5.5、status子命令
status子命令(1: `[s]tatus`)功能上和git add -i相似
5.6、quit子命令
quit子命令（7: `[q]uit`）用于退出git add -i命令系统
六、帮助
我们可以通过`git add -h`命令来看git add命令的帮助文档。




### git移除已经add的文件

使用 git rm 命令即可，有两种选择,
一种是 `git rm --cached` “文件路径”，不删除物理文件，仅将该文件从缓存中删除；
一种是 `git rm --f “文件路径”`，不仅将该文件从缓存中删除，还会将物理文件删除（不会回收到垃圾桶）。
`[其他] `请问 `git rm --cache` 和 `git reset HEAD` 的区别到底在哪里呢？
如果要删除文件，最好用 `git rm file_name`，而不应该直接在工作区直接 `rm file_name`。
如果一个文件已经add到暂存区，还没有 commit，此时如果不想要这个文件了，有两种方法：
1，用版本库内容清空暂存区，`git reset HEAD` 但要慎重使用
2，只把特定文件从暂存区删除，`git rm --cached xxx`

### GIT撤销修改 restore

https://www.jianshu.com/p/dcef204dba74

GIT 撤销修改，主要利用 `git restore` 命令。现在，我们来假象一个使用场景。当我们大半夜战至性头时，一上头不小心在文件中写了句不该写的话`"老板是个大煞笔"`！并且已经 `git add` 到暂存区(staged) 中了！如果再继续`commit` 的话，第二天就面临失业的风险！



```ruby
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   READEME.md
```

从上面可以看到，有一个待提交文件，并且还有一个重要的提示：**use "git restore --staged <file>..." to unstage** ，翻译过来就是，使用 `git restore --staged <file>...` 可以使文件变成已修改(未执行 `add` 时  )状态。
 好的，是时候展现真正的技术了，命令敲起来ヾ(ﾟ∀ﾟゞ)：



```ruby
$ git restore --staged READEME.md
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   READEME.md
```

当我们执行 `store --staged` 命令后，再用 `status` 查看状态，会发现，文件已经变成 add 执行前的状态了。是的，这样咱们就彻底保住了工作。现在划重点，我们看下执行 `git restore --staged READEME.md` 到底发生了什么。

> **`git restore --staged [file]`** : 表示从暂存区将文件的状态修改成 unstage  状态。当然，也可以不指定确切的文件 ，例如：
>  `git restore --staged *.java` 表示将所有暂存区的java文件恢复状态
>  `git restore --staged .` 表示将当前目录所有暂存区文件恢复状态
>  **`--staged`** 参数就是表示仅仅恢复暂存区的

问题总结接踵而至，如果我不们不止执行了 `add` 命令，还执行了 `commit` 命令。是不是也可以利用 `restore` 命令返回呢？答案是肯定的。下面，我们介绍几个命令。


 我们又有错别字了，但是已经 `commit` 了，那么应该怎么办呢？

```cpp
$ git restore -s HEAD~1 READEME.md  // 该命名表示将版本回退到当前快照的前一个版本
$ git restore -s 91410eb9  READEME.md  // 改命令指定明确的 commit id ，回退到指定的快照中
$ git reset --soft HEAD^  // 该命令表示撤销 commit 至上一次 commit 的版本
```

#### 总结

本篇文章的所有重点都集中在一个命令上 `restore` ，该命令主要有三个参数，我重点介绍一下，`restore` 命令，默认是带着 `--worktree` 参数的

|                命令                |                        作用                         |     备注      |
| :--------------------------------: | :-------------------------------------------------: | :-----------: |
| `git restore --worktree README.md` |        表示撤销 README.md 文件工作区的的修改        | 参数等同于 -W |
|  `git restore --staged README.md`  | 表示撤销暂存区的修改，将文件状态恢复到未 `add` 之前 | 参数等同于 -S |
| `git restore -s HEAD~1 README.md`  |       表示将当前工作区切换到上个 commit 版本        |               |
| `git restore -s dbv213 README.md`  |     表示将当前工作区切换到指定 commit id 的版本     |               |



### 提交忽略某些文件

https://www.cnblogs.com/mafeng/p/7635228.html

#### 1.设置.gitignore

常用的规则：
1）/mtk/        过滤整个文件夹
2）*.zip         过滤所有.zip文件
3）/mtk/do.c     过滤某个具体文件

被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中：
1）!*.zip
2）!/mtk/one.txt

唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。
为什么要有两种规则呢？想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么我们就需要使用：
1）/mtk/
2）!/mtk/one.txt
假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！

最后需要强调的一点是，**如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用**，Git仍然会对所有文件进行版本管理。
简单来说，出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。因此一定要养成在项目开始就创建.gitignore文件的习惯，否则一旦push，处理起来会非常麻烦。


#### 2.使用命令

.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
正确的做法是在每个clone下来的仓库中手动设置不要检查特定文件的更改情况。
`git update-index --assume-unchanged FILE` 在FILE处输入要忽略的文件。
如果要还原的话，使用命令：
`git update-index --no-assume-unchanged FILE`

#### 3.使用.git/info/exclude

git 还提供了另一种 exclude 的方式来做同样的事情，不同的是 .gitignore 这个文件本身会提交到版本库中去。用来保存的是公共的需要排除的文件。而 .git/info/exclude 这里设置的则是你自己本地需要排除的文件。 他不会影响到其他人。也不会提交到版本库中去。

### git clean清除未跟踪的文件

有时做Build会引入很多之前没加入.gitignore的文件。这时你不可能每个目录每个文件地去删。`git clean -df `可帮你搞定一切。

举例：

```
git clean -dn #这个命令可以看看有哪此文件和目录会被删

git clean -f #只会删文件，不会删目录
```

### git删除指定commit

https://www.cnblogs.com/lwcode6/p/11809973.html

https://www.cnblogs.com/yuluoxingkong/p/9835368.html

或者采取以下方法
> https://www.cnblogs.com/lwcode6/p/11809973.html

1. 使用`git log `命令，查看已提交的记录。例如红色圈出的commit是本次要删除的commit。

![学习笔记-20201205182720-2020-12-05-18-27-25](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205182720-2020-12-05-18-27-25.png)

2. 先找到此次提交之前的一次提交的commit 1d6b81b138f89735265900b94fcd1ec39375e7b4

3. 执行`git rebase -i 1d6b81b138f89735265900b94fcd1ec39375e7b4`，弹出如下页面（不包含当前commit）

![学习笔记-20201205182904-2020-12-05-18-29-14](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205182904-2020-12-05-18-29-14.png)

按字母I键进入编辑模式，将需要删除的commit的pick改为drop，然后按esc退出编辑，：wq保存
![学习笔记-20201205183048-2020-12-05-18-30-50](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205183048-2020-12-05-18-30-50.png)

4. 再次执行git log命令，查看已提交记录，之前红色圈出的commit记录已被删除
    ![学习笔记-20201205183149-2020-12-05-18-31-52](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205183149-2020-12-05-18-31-52.png)

### git删除指定commit-续
**一、删除文件**
如果需要删除的 commit 是一个或多个文件，可以进行以下操作。
1. 被提交到仓库的某个文件需要删除，可以使用 git rm 命令：
 `git rm <file> `// 从工作区和暂存区删除某个文件2. `git commit -m ""` // 再次提交到仓库
    如果只想从暂存区删除文件，本地工作区不做出改变，可以：
    `git rm --cached <file>`
    如果在工作区不小心删错了某个文件，可以用 git checkout 将暂存区的文件覆盖工作区的文件，从而把误删的文件恢复：
    `git checkout -- <file>`
    用 `git rm `删除文件，同时还会将这个删除操作记录下来；
    用 `rm 删除文件`，删除的仅仅是本地物理文件，没有将其从 git 的记录中剔除。
2. `git add` 和 `git rm` 有相似的功能，
但 `git add` 仅能记录添加、改动的动作，删除的动作需靠 `git rm `来完成。
**二、GitHub 删除某次 commit**
如果需要删除的不只是某个文件，而是交错的代码，那么有以下三种方法可以删除 commit 。
* git reset
* git reset ：回滚到某次提交。
* git reset --soft：此次提交之后的修改会被退回到暂存区。
* git reset --hard：此次提交之后的修改不做任何保留，git status 查看工作区是没有记录的。
回滚代码

如果需要删除的 commit 是最新的，那么可以通过 `git reset `命令将代码回滚到之前某次提交的状态，但一定要将现有的代码做好备份，否则回滚之后这些变动都会消失。具体操作如下：
```
//回滚代码
git log // 查询要回滚的 commit_id
git reset --hard commit_id // HEAD 就会指向此次的提交记录
git push origin HEAD --force // 强制推送到远端
```
误删恢复

如果回滚代码之后发现复制错了 commit_id，或者误删了某次 commit 记录，也可以通过下方代码恢复：
```
//误删恢复
git relog // 复制要恢复操作的前面的 hash 值
git reset --hard hash // 将 hash 换成要恢复的历史记录的 hash 值
```
注意：删除中间某次提交时最好不要用` git reset` 回退远程库，因为之后其他人提交代码时用` git pull` 也会把自己的本地仓库回退到之前的版本，容易出现差错进而增加不必要的工作量。
### git rebase 合并多次commit

https://blog.csdn.net/csdlwzy/article/details/83379546?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control

**使用rebase命令**

想要合并前三个 commit ，使用下面的命令：

```
git rebase -i HEAD~3
```

进入编辑界面，把要保留的 commit 使用pick，其他的使用squash命令，或者根据命令提示选择自己想用的命令

![image-20210415110322574](../../../../Library/Application Support/typora-user-images/image-20210415110322574.png)

### git rebase Vs git revert

git rebase：当两个分支不在一条线上，需要执行 merge 操作时使用该命令。

**撤销提交**
如果中间的某次 commit 需要删除，可以通过 `git rebase `命令实现，方法如下：
```
//撤销提交
git log // 1.查找要删除的前一次提交的 commit_id
git rebase -i commit_id // 2.将 commit_id 替换成复制的值
//3.进入 Vim 编辑模式将要删除的 commit 前面的 `pick` 改成 `drop`
//4.保存并退出 Vim
```
这样就完成了。
**解决冲突**
该命令执行时极有可能出现 reabase 冲突，可以通过以下方法解决：
1. git diff // 查看冲突内容
2. // 手动解决冲突（冲突位置已在文件中标明）
3. git add <file> 或 git add -A // 添加
4. git rebase --continu // 继续 rebase
5. // 若还在 rebase 状态，则重复 2、3、4，直至 rebase 完成出现 applying 字样
6. git push
**git revert**
* git revert：放弃某次提交。
* git revert 之前的提交仍会保留在 git log 中，而此次撤销会做为一次新的提交。
* git revert -m：用于对 merge 节点的操作，-m 指定具体某个提交点。
**撤销提交**
要撤销中间某次提交时，使用 `git revert` 也是一个很好的选择：
 1. git log // 查找需要撤销的 commit_id
 2. git revert commit_id  // 撤销这次提交
撤销 merge 节点提交 如果这次提交是 merge 节点的话，则需要加上 -m 指令：git revert commit_id -m 1 // 第一个提交点
 3. // 手动解决冲突
 4. git add -A
 5. git commit -m ""
 6. git revert commit_id -m 2 // 第二个提交点
 7. // 重复 2，3，4
 8. git push

原文链接：
https://www.jianshu.com/p/c9f131e22a60

**附： git rebase**
https://blog.csdn.net/qq_41629756/article/details/100731258
1. git log先找到需要变基(rebase)的Hash ID的下一个ID(不是本身Hash值)
2. git rebase -i (Hash ID) 此时会出现两种情况
1）工作区有变更尚未提交
```
$ git rebase -i 121f508bc4ac7044c1dda188fc595e7029613f22
不能变基：您有未暂存的变更。
而且您的索引中包含未提交的变更。
请提交或贮藏修改。
```
遇到这种情况需要将变更缓存，输入git stash 存储变更后再进行第二步操作
2）工作区无变更
此时直接往下执行：
```
pick f60514c5 a
pick e52ec2e0 b
pick b2ee5bd4 c
pick 1e3b1ed8 d
pick ac231a7a e
pick 1ddd77c2 f
pick de41e172 g
pick bab63064 h
pick f898eacd i
```
```
# 变基 b0279a0c..f898eacd 到 b0279a0c（9 个提交）
#
# 命令:
# p, pick = 使用提交
# r, reword = 使用提交，但修改提交说明
# e, edit = 使用提交，但停止以便进行提交修补
# s, squash = 使用提交，但和前一个版本融合
# f, fixup = 类似于 "squash"，但丢弃提交说明日志
# x, exec = 使用 shell 运行命令（此行剩余部分）
# d, drop = 删除提交
#
# 这些行可以被重新排序；它们会被从上至下地执行。
#
# 如果您在这里删除一行，对应的提交将会丢失。
#
# 然而，如果您删除全部内容，变基操作将会终止。
```

3. 根据提示，将pick改为适应需求的关键词即可
4. 退出保存
5. 输入 git stash pop 释放之前保存的缓存然后正常操作即可

### 如何删除Git上的远程文件夹

**方法一**

这里以删除 test文件夹为案例

```shell
git rm -r --cached test //--cached不会把本地的test删除
git commit -m 'delete test dir'
git push -u origin master
```

**方法二**

如果误提交的文件夹比较多，方法一也较繁琐
直接修改.gitignore文件,将不需要的文件过滤掉，然后执行命令:

```shell
git rm -r --cached .
git add .
git commit
git push  -u origin master
```

**注：**

```shell
git rm -r -n --cached  */dirs/\*      #把dirs里的全部移除
# -n：加上这个参数，执行命令时，是不会删除任何文件，而是展示此命令要删除的文件列表预览。
```

### 清空commits历史记录

https://www.cnblogs.com/magic-wei/p/9919277.html

git是当前最常见的版本控制工具，但出现以下情况时，往往需要清空commits历史记录：

- commits记录占用空间过大甚至远远超过版本控制文件本身大小，进行云端代码管理时会受制于空间限制，无法继续更新
- 历史记录中存在敏感信息，需要清理

清理commits历史记录的核心思想是，直接删除本地的.git目录，重新建立git仓库并与远程仓库建立链接，采用强制提交的方式覆盖远程仓库的commits记录。下面是一段示例脚本。

参数说明：

- $REPO_DIR 表示需要处理的Git仓库本地目录
- git@github.com:xxxx/$REPO_DIR.git 表示远程仓库地址

则可以按照如下步骤处理：

#### 进入本地仓库，删除.git目录

```bash
cd $REPO_DIR
rm -rf .git
```

#### 重新git初始化并添加commit

```bash
git init
git add . # 重新添加所有的文件
git commit -m "restart git commit"
```

#### 添加远程仓库链接

在添加远程仓库时，需要设置远程仓库的代号，本教程记为**origin**.

```bash
git remote add origin git@github.com:xxxx/$REPO_DIR.git
```

此时，可以用`git remote -v`检查远程仓库的设置。

#### 强制提交，覆盖远程仓库的commits历史记录

假设提交到远程仓库的master分支，则强制提交脚本如下：

```bash
git push -f origin master # 或者 git push --force origin master
```

强制提交之后，再看远程仓库master分支的commits记录就变成1了。

如果需要与上游保持同步检测，可以使用指令`--set-upstream origin/master`，即

```bash
git push origin master --set-upstream origin/master # 如果指向其他分支，可以修改为 origin/${指定分支名}
```

至此，大功告成～

#### 后续讨论

细心的朋友可能会发现，上述操作之后，如果你还记得历史记录中某个commit的链接，你仍然可以通过链接访问到该commit下的文件，甚至可以基于这个commit重新创建新分支。为什么会出现这种情况呢？这其实和Git本身的设计机制有关，主要是为了提高容错率，防止你因为一些误操作弄丢了某些commits进而造成无法挽回的结果。

实际上，这些commits并没有马上被清理掉，仅仅是你的所有分支或标签无法访问到它们，这些commits被称为unreachable commits. 它们通常会被缓存一段时间，这个周期默认是30天，你也可以通过git命令行手动修改缓存周期或者手动清理。由于Github也是建立在Git这个版本管理工具上的网站，所以它也有这个机制。虽然它们在缓存期内仍然可以被访问到，但你clone到本地并不会包含它们，也就是说，你并不能在本地删除Github上已经存在的unreachable commits，因为本地根本访问不到它们（[存在于 GitHub 上但不存在于本地克隆中的提交](https://help.github.com/cn/github/committing-changes-to-your-project/commit-exists-on-github-but-not-in-my-local-clone)）。如果不着急的话，你可以等30天之后再试试看是否还能访问这些unreachable commits的链接；但如果你很着急，你可以联系[Github Support](https://support.github.com/)帮你清理这些你不想保留的commits。

所以，如果你只是维护个人的文件仓库的话，不需要担心这个问题，你在新机器上clone下来的仍然是缩减大小之后的仓库，而Github上的unreachable commit会在缓存期后被清理掉。如果是与他人协作的仓库，还是谨慎使用`git push --force`这种危险的操作吧，确实遇到需要这个操作的场景时，考虑用更安全的`git push --force-with-lease`. 如果你强制提交之后发现后悔了，找到想恢复的commit的链接并创建新分支就可以找回那个commit所在历史分支之前的内容啦。

感谢@绿静風 发现了这个问题，促使我进一步查阅资料去完善这篇博文，在此表示感谢！

后续讨论的主要参考内容如下：

- [Git Internals - Maintenance and Data Recovery](https://git-scm.com/book/en/v2/Git-Internals-Maintenance-and-Data-Recovery)
- [Stackoverflow - How to remove a dangling commit from GitHub?](https://stackoverflow.com/questions/4367977/how-to-remove-a-dangling-commit-from-github)

如果只是想删除历史记录中曾经存在（但现在并不需要）的大文件，可以参考这个Issue中的讨论：[Consider cleaning up the .git folder to reduce the large repo size](https://github.com/18F/C2/issues/439)git commit和git push的区别

git commit操作的是本地库，git push操作的是远程库。

* git commit是将本地修改过的文件提交到本地库中。
* git push是将本地库中的最新信息发送给远程库。

### 创建分支branch和使用Pull request

![](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-18-03-e0c1cd706c9becd959756c6b89e22b5f-image17-61c157.png){width="6.052777777777778in"
height="3.3958333333333335in"}\
重点看一下base和compare，Pull request将compare的分支的更新发送给base的分支，如上图所示。点击"Create pull request"，然后填写发送Pull request的原因和描述，再点击点击"Create pull request"，完成发送。


### GitHub 实现多人协同提交代码并且权限分组管理

<https://blog.csdn.net/weixin_34044273/article/details/86394095?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3.control>

### Git多分支平行发展（一个仓库包含多个不同的项目）

https://segmentfault.com/a/1190000015430066

<https://segmentfault.com/a/1190000015430066>

### Git中submodule的使用

**背景**

面对比较复杂的项目，我们有可能会将代码根据功能拆解成不同的子模块。主项目对子模块有依赖关系，却又并不关心子模块的内部开发流程细节。

这种情况下，通常不会把所有源码都放在同一个 Git 仓库中。

有一种比较简单的方式，是在当前工作目录下，将子模块文件夹加入到 .gitignore 文件内容中，这样主项目就能够无视子项目的存在。这样做有一个弊端就是，使用主项目的人需要有一个先验知识：需要在当前目录下放置一份某版本的子模块代码。

还有另外一种方式可供借鉴，可以使用 Git的 submodule 功能，也是这篇文章的主题。

实际上 Git
工具的 submodule 功能就是建立了当前项目与子模块之间的依赖关系：子模块路径、子模块的远程仓库、子模块的版本号。

<https://zhuanlan.zhihu.com/p/87053283>

### git clone移动本地厂库

```powerShell
git clone d:/SourceRepository d:/DestinationRepository
```
d:/SourceRepository:想克隆的本地仓库路径，
d:/DestinationRepository:想克隆去另一个地方的路径

例如 git clone d:/git e:/git11
是将d:/git的仓库（即包含隐藏文件.git的目录）克隆到 e:/git11目录下

![](学习笔记/media/image18.png){width="7.216666666666667in"
height="1.74375in"}

### git裸克隆

myIdea:**尤其是克隆含有超大文件的仓库时，由于工作区含有大文件的缓存，故要用`git clone --mirror`** 以下为--mirror后的：

![image-20201213105603140](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/typora-user-images/2020/12/13/10-56-05-d27dfd459ca4a4fc85609d8b0eb6f231-image-20201213105603140-0d55f1.png)

用法1：`git clone <repository> <directory>`

将`<repository>`指向的版本库创建一个克隆到`<directory>`目录。目录`<directory>`相当于克隆版本库的工作区，文件都会检出，版本库位于工作区的.git目录中

用法2：`git clone --bare <repository> <directory.git>`

用法3：`git clone --mirror <repository> <directory.git>`

用法2和用法3创建的克隆版本库都不包含工作区，直接就是版本库的内容，这样的版本库称为裸版本库。一般约定俗成裸版本库的目录名以.git做后缀，所以上面示例中将克隆出来的裸版本库目录名写作<directory.git>。区别在于用法3克隆出来的裸版本对上游版本库进行了注册，这样可以在裸版本库中使用git fetch命令和上游版本库进行持续同步。

不使用--bare或--mirror创建出来的克隆包含工作区，这样就会产生两个包含工作区的版本库，这两个版本库对等。这两个工作区本质上没有区别，往往提交在一个版本A中进行，另一个B作为备份。只能从B执行git pull命令从A中拉回新的提交实现版本库同步，而不能从版本库A向版本库B执行git push推送操作

还可以通过git init的方式创建裸版本库，需要加--bare参数。

当执行git push命令时，如果没有设定推送的分支，而且当前分支也没有注册到远程的某个分支，将检查远程分支是否有和本地相同的分支名（如master），如果有，则推送，否则报错。

### git pull和git fetch的区别

**前言**

在我们使用git的时候用的更新代码是git fetch，git
pull这两条指令。但是有没有小伙伴去思考过这两者的区别呢？有经验的人总是说最好用git
fetch+git merge，不建议用git pull。也有人说git pull=git fetch+git
merge，真的是这样吗？为什么呢？既然如此为什么git还要提供这两种方式呢？

原文链接

- <https://blog.csdn.net/weixin_41975655/article/details/82887273>

### fatal: does not appear to a git repository

几周没用git，今天一来托管就报错，下面记录一下解决办法。

```powerShell
$ git push -u origin master
fatal: 'git@github.com/zejun_web' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
这是报错信息，建立了文件夹用了

```powerShell
git init
```

后，也remote了，结果就是push不上去。

后面检查了一下remote内容
```powerShell
$ git remote -v
origin  git@github.com/zejun_web (fetch)
origin  git@github.com/zejun_web (push)
```
敢情是remote命令就错了，里面少了git账号:git-ze,应该是：

```PowerShell
git remote add origin git@github.com:git-ze/zejun_web.git
```

这样就知道怎么解决了，
先remove掉添加在远程的origin

```PowerShell
git remote rm origin
```

此时再用

```powerShell
git remote -v
```

就会发现没有origin了

再正确输入

```powerShell
git remote add origin git@github.com:git-ze/xxxx.git
```

就可以了。

然后
```powerShell
$ git push -u origin master
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (7/7), 545 bytes | 272.00 KiB/s, done.
Total 7 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/git-ze/zejun_web/pull/new/master
remote:
To github.com:git-ze/zejun_web.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```
到这里就成功啦。
网上查了一下还有的说要重新配置邮箱和姓名等信息的。。如果没有添加公钥的话确实还是要先在GitHub上添加公钥，如果已经添加过了，可以先用git remote
-v命令来检查一下添加的origin是不是代码写错了，写少了。

如果错了就先 git remote rm origin
然后最后就可以push了。

![](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-18-23-2e2011e3bb51a81ccbaa15e5a905487e-image19-b07eeb.png){width="7.141666666666667in"
height="2.248611111111111in"}

> 要注意的就是第一次push的话，要加上 -u
> 在语句里，把本地master分支和远程库的master分支关联起来。

原文链接

- https://blog.csdn.net/python_neophyte/article/details/83381936

### git fork与clone有什么区别及使用场景

#### git clone

git clone xx 是我们比较熟悉的操作,它类似于Download功能，可以理解为将云端代码下载到我们自己电脑的本地。

正常的话需要我们本机安装了git，然后使用git clone [仓库地址]
即可将制定仓库地址代码下载到我们本机。

#### git fork

我们在github上打开别人的项目，右上角会有一个fork及fork的人数。如下图：

- watch
  
  就类似于关注，后续项目有任何更新都会通知你，如果设置了邮件还会邮件通知。觉得比较好的项目可以通过star进行收藏，并且收藏的同时也点了一个赞，在github中，star越多的项目肯定是越牛逼的项目了。这个也是很多面试官比较在意的，你有没有github开源项目？star多少？就是指这个了

-  fork
  就是我们要讲的，我们将开源项目存储到我们自己的云端作为一个分支，我们可以进行一些bug修复或功能修改然后git pull到开源项目，如果开源项目认可，可以将你的修改合并到他们的分支。

根据上面的描述大约可以知道fork的作用了。我们fork完之后，代码存储到了云端并没有下载到本地。

fork之后我们可以通过github账号的repositories 里找到

**两者适用场景**

Git可以多人协作完成项目，或者我写完一个项目可以开源到GitHub上，看到的小伙伴fork我的代码之后发现有BUG或者有一个地方有更好的算法可以解决，他可以在他自己的仓库里面修改源码，修改好之后他可以pull request，这样我就可以看到什么地方修改了，如果我觉得他的算法可行就可以把他的代码Merge到我的项目里面，简单说就帮我修复bug了，不用我自己动手。

git clone 就是他们clone到本地进行修改，然后他可以提交到clone的源码中。

### git 推送本地分支到远程分支 git push origin

推送本地分支local_branch到远程分支 remote_branch并建立关联关系


a.远程已有remote_branch分支并且已经关联本地分支local_branch且本地已经切换到local_branch

```powerShell
git push
```
 b.远程已有remote_branch分支但未关联本地分支local_branch且本地已经切换到local_branch

```powerShell
git push -u origin/remote_branch
```
c.远程没有remote_branch分支并，本地已经切换到local_branch

```powerShell
git push origin local_branch:remote_branch
```

### git remote关联了两个或多个仓库
```shell
# 查看远程仓库的数量（简单信息）
git remote -v
 
# 查看某个远程仓库的具体信息，以origin为例：
git remote show origin

# 比如关联两个仓库: github 和码云
 
git remote add origin github-url
 
git remote add gitee gitee-url
 
# 分支有两个：master ，test-branch
```
原文链接
- <https://blog.csdn.net/weixin_41287260/article/details/89743120>

### git add外部文件
需要把外部文件复制到仓库目录下：
![](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-18-44-729f65c734788aa782d054c4bded528d-image20-dee2cb.png){width="8.770833333333334in"
height="2.45625in"}

### git add 文件

方法一 git add 添加多个文件，文件之间以空格隔开

```
git add file1 file2 file3
```

方法二 多次git add

```shell
git add file1

git add file2

git add file2
```

方法三 添加指定目录下的文件\
config目录下及子目录下所有文件，home目录下的所有.php文件

```shell
git config/*

git home/*.php

```
方法四 git add . 添加所有的文件， 或者 git add \--all 添加所有的文件

```shell
git add .

git add --all
```
方法五 添加所有子目录(**/)下的所有.zip文件
```shell
git add **/*.zip 

```

### git commit 提交到版本库

git add 目的是将修改文件由工作区提交到暂存区，可以多次提交\
然后commit操作，将文件从暂存区提交到版本库

git commit -m \"add new file\"

## git 廖雪峰学习文档

### 工作区和暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的`learngit`文件夹就是一个工作区：![working-dir](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/abnerworks.Typora/2020/12/05/15-30-06-2012268feac886848fd1c027c8329c5d--var-folders-84-tzfvcm9s5wlc1gcjq2qpqygw0000gn-T-abnerworks.Typora-0-f0ea7f.png)

#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![git-repo](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/abnerworks.Typora/2020/12/21/12-48-38-701e02bf0b2d71ab51b7e2b6aa973d52-0-9b8ebd.jpeg)

分支和`HEAD`的概念我们以后再讲。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。

先用`git status`查看一下状态：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```

Git非常清楚地告诉我们，`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   LICENSE
	modified:   readme.txt
```

现在，暂存区的状态就变成这样了：

![git-stage](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/abnerworks.Typora/2020/12/05/15-32-07-3140921b12cc7d9a949076b2bb80d637--var-folders-84-tzfvcm9s5wlc1gcjq2qpqygw0000gn-T-abnerworks.Typora-0-ec896c.jpeg)

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

```
$ git commit -m "understand how stage works"
[master e43a48b] understand how stage works
 2 files changed, 2 insertions(+)
 create mode 100644 LICENSE
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```
$ git status
On branch master
nothing to commit, working tree clean
```

现在版本库变成了这样，暂存区就没有任何内容了：

![git-stage-after-commit](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/abnerworks.Typora/2020/12/05/15-32-41-f6ddf40f921f9953b6f84d107a11f689--var-folders-84-tzfvcm9s5wlc1gcjq2qpqygw0000gn-T-abnerworks.Typora-0-20201205153241447-d86c8b.jpeg)

git-stage视频：

<video id="video" controls="" preload="none" poster="http://media.w3.org/2010/05/sintel/poster.png">   <source id="mp4" src="https://www.bilibili.com/video/av51227250?zw " type="video/mp4"> </video>

原文链接

- https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576

> 他人整理如下： https://blog.csdn.net/u014734886/article/details/79527710

## 一、git初始化本地仓库和配置

```
echo "想输入到文件的内容，一般为# 库名字" >> README.md

git init
```

如果没有配置需要配置

```
git config --list

git config --global user.email "abc@bupt.edu.cn"

git config --global user.name "xy"

git config --list

```
还可以配置git显示颜色

```
git config --global color.ui true

```
配置别名

```shell
git config --global alias.st status 使用git st 代替 git status

git config --global alias.co checkout 使用git co 代替 git checkout

git config --global alias.ci commit 使用git ci 代替 git commit

git config --global alias.br branch 使用git br 代替 git branch
```

有人丧心病狂地把lg配置成了：

```
git config --global alias.lg "log --color --graph
--pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)
%C(bold blue)<%an>%Creset' --abbrev-commit"

```
## 二、提交文件

```
git status  查看当前仓库的状态

git diff file_name

git add file2.txt file3.txt 想添加所有的文件git add .

git status

git commit -m "提交记录文字"

git status
```

举例：

```
git commit -m "Fixes bug"
```

如果发现commit信息写错了，

```
git commit --amend -m "Fixes bug #42"

```
## 三、回退

![学习笔记-20201205155858-2020-12-05-15-58-59](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-20201205155858-2020-12-05-15-58-59.png)




### 1.查看commit信息和命令信息

```
git log（查看当前状态下的commit信息，不能查看以后的信息）

git reflog（查看所有的命令信息）

git reflog

git log -p --graph
```

<https://www.jianshu.com/p/98c473fb0ee2>

通过 git pull更新后，会显示别人修改了哪些文件。此时你想要查看某个文件的具体修改的内容，可通过下面的命令去查看：

```
git log -p   + 文件名 （可查看该文件以前每一次push的修改内容）
git log - p -1   + 文件名 （只查看该文件当前这一次的push内容）

git log --graph 看到分支合并图

git log --graph --pretty=oneline --abbrev-commit

```
### 2.回退

```
git reset --hard commit_id 
```
除了--hard参数外，还有--soft，--mixed。

**下面详细介绍这三个参数：**

* add表示add操作之后的结果

* commit表示commit之后的结果

* push:表示进行push操作之后的结果

* (stash)表示在add前可能存在stash操作（即暂存工作区的操作）

假设某次提交过程如下

```
init--(stash1)--add1--commit1--push1--(stash2)--add2--commit2--push2--(stash3)--add3--commit3--push3
```
举例

* --hard 
  回退到某个版本commit之前的状态，进行1，2，3操作。如现在在commit2，或者add2，可以回到commit3或者commit1

* --soft
  回退到某次commit前的stage状态（即处于暂存状态），进行1操作。如现在在commit2，可以回到add1，或者add3

* --mixed
  回退到add前的状态（即处于工作区，如果有stash，需通过stash pop之后才能真的回到暂存的状态），执行1，2操作。\
  如现在在commit2，可以回退到init--(stash1)，或者commit1-push1--(stash2)，或者

### 3.HEAD介绍

HEAD指向的版本就是当前版本，`HEAD^`,前一个版本，`HEAD^^`前两个，`HEAD~100`，前100个版本

### 4.查看远程log

`git fetch --all `可以把远程的commit信息拉到本地更新到本部版本库的master
HEAD指针上，然后利用`git log`和`git reflog`进行查看操作

穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本，也可以用git reflog。

要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

建议都用`git reflog`

## 四、切换暂存区、工作区

```
git stash   #暂存工作现场

git stash list #会出现stash@{0}: WIP on dev: 6224937 add mergegit

git stash pop #将暂存区的环境恢复到工作区

git stash list  #此时暂存区已经没有数据了

git diff HEAD -- readme.txt 查看工作区和版本库里面最新版本的区别

git checkout -- readme.txt
把工作区的修改全部撤销,其中--不能省，否则就变成切换分支了。

git reset HEAD file_name
可以把暂存区的修改撤销掉（unstage），重新放回工作区
```

> 关于git checkout可以看一下这篇文章<https://www.cnblogs.com/kuyuecs/p/7111749.html>

**checkout命令用法如下：**

```
#1
git checkout [-q] [<commit>] [--] <paths> ...
#2
git checkout [<branch>]
#3
git checkout [-m] [ [-b | -- orphan ] <new_branch>]
 [start_point] 
```
用法2比用法1的区别在于，用法1包含了路径。为了避免路径和引用（或提交ID）同名而发生冲突，可以在\<paths\>前用两个连续的连字符作为分隔。用法1的\<commit\>是可选项，如果省略，则相当于从暂存区进行检出。

## 五、删除文件

### 1.删除本地文件

```
git rm file_name

git commit -m "删除信息"
```

### 2，误删

```
git checkout -- test.txt
```
用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以"一键还原"。

命令`git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

* 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

* 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。


### 3.删除远端文

```
git rm -r --cached --force .idea/ 
```
删除文件不需要加-r，删除文件夹需要-r， 该文件夹路径为本地文件夹所在路径
```
git commit -m "delete .idea/" 提交记录
git push origin master  推到远端
```


## 六、本地分支和远程分支

### 1.查看本地分支，带星号的表示当前所在本地分支

```
git branch
```

查看远程和本地分支

```
git branch -a
```

如果没有成功，先`git fetch origin`，然后我们在`git branch -a`

### 2.创建本地分支

```
git branch dev #创建分支dev

git checkout dev #切换分支（不要随意切分支，
#如果你在某个分支上面修改了一些东西，但没有stash，那么你切换分支后修改的东西就没有任何保存了，如果想切，请先git stash，然后git checkout dev) stash后没有stash pop，然后reset --hard

git checkout -b dev #创建并切换分支也可以用于切换已有分支
```
### 3.创建远程分支

 如果想把本地的test分支提交到远程仓库，并作为远程仓库的master分支，或者作为另外一个名叫test的分支。
```
#提本地test支作为远程的master分支
git push origin test:master

#提交本地test分支作为远程的test分支
git push origin test:test
```
也可以在github网站直接创建

![学习笔记-学习笔记mediaimage22.png-2020-12-05-16-32-09](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-学习笔记mediaimage22.png-2020-12-05-16-32-09.png)


### 4.合并本地分支

```
git merge dev
```
合并当前分支，一般先切换到需要被合并的分支，如切换到master，该命令在master分支上输入会将dev分支合并到master分支

```
git merge --no-ff -m "merge with no-ff" dev
```
--no-ff参数，表示禁用Fast
forward，用普通模式合并，合并后的历史有分支，能看出来曾经做过合并。

merge和rebase的区别:<https://blog.csdn.net/wh_19910525/article/details/7554489>

git merge b # 将b分支合并到当前分支

git rebase b，也是把 b分支合并到当前分支

假设目前分支：

![学习笔记-image23-2020-12-05-16-34-27](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-image23-2020-12-05-16-34-27.jpeg)

![学习笔记-image24-2020-12-05-16-34-46](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-image24-2020-12-05-16-34-46.jpeg)

![学习笔记-image25-2020-12-05-16-35-01](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-image25-2020-12-05-16-35-01.jpeg)

### 5.origin

<https://blog.csdn.net/tyyking/article/details/82909099>

git的服务器端(remote)端包含多个repository，每个repository可以理解为一个项目。而每个repository下有多个branch。"origin"就是指向某一个repository的指针。服务器端的"master"（强调服务器端是因为本地端也有master）就是指向某个repository的一个branch的指针。

这是服务器端(remote)的情况：

![学习笔记-image26-2020-12-05-16-35-44](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-image26-2020-12-05-16-35-44.png)

```
git remote add origin git@github.com:JasonDu1993/learngit.git
```
关联远程库，相当于让origin等于后面这个地址

### 6.git fetch 更新远程代码到本地仓库

<https://www.cnblogs.com/chenlogin/p/6592228.html>

理解 fetch 的关键, 是理解 FETCH_HEAD，FETCH_HEAD指的是:
某个branch在服务器上的最新状态

当前分支指向的FETCH_HEAD, 就是这个文件第一行对应的那个分支.

一般来说, 存在两种情况:

1）如果没有显式的指定远程分支, 则远程分支的master将作为默认的FETCH_HEAD.

2）如果指定了远程分支, 就将这个远程分支作为FETCH_HEAD.

命令1：`git fetch origin branch1`

设定当前分支的 FETCH_HEAD' 为远程服务器的branch1分支。这个操作是`git pull origin branch1`的第一步,
而对应的pull操作,并不会在本地创建新的branch。

同时这个命令还可以用来测试远程主机的远程分支branch1是否存在, 如果存在,
返回0, 如果不存在, 返回128, 抛出一个异常.

命令2：`git fetch origin branch1:branch2`

使用远程branch1分支在本地创建branch2(但不会切换到该分支),如果本地不存在branch2分支,
则会自动创建一个新的branch2分支,

如果本地存在branch2分支, 并且是`fast forward`, 则自动合并两个分支,
否则, 会阻止以上操作.

### 7.fetch更新本地仓库两种方式

方法一
```
git fetch origin master
//从远程的origin仓库的master分支下载代码到本地的master分支

git log -p master origin/master //比较本地的仓库和远程仓库的区别

git merge origin/master
//把远程下载下来的代码合并到本地仓库，远程的和本地的合并

```

方法二
```
git fetch origin master:temp
//从远程的origin仓库的master分支下载到本地并新建一个分支temp

git diff temp //比较本地master分支和本地temp分支的不同

git merge temp //合并本地temp分支到本地master分支

git branch -d temp //删除本地temp分支

```
### 8.合并远程分支

假设这两个分支是a和b，那么fetch a和b，checkout a，将b
merge(rebase)到a，push
a到远端。这样做，将b和a合到了一起，并且更新了本地和远端的a。如果b不需要了，可以删除远程b和本地b

```
git fetch origin a:a #将远程a分支拉到本地a(冒号后面的a表示本地分支a)

git fetch origin b:b #将远程b分支拉到本地b(冒号后面的b表示本地分支b)

git checkout a #切到本地a分支

git merge b   #将本地b分支合并到本地a分支上

git push origin a #将本地a分支推到远程a分支

git branch -d b  #删除本地分支

git push origin --delete b   #删除远程b分支
```

### 9.删除本地分支

```
git branch -d dev #删除分支
```

### 10.删除远程分支

```
git push origin --delete dev
```
### 11.创建本地新分支并将新分支和远程某个分支相关联

```
git branch -a #查看本地和远程所有分支

git checkout -b dev /origin/dev  #创建本地分支dev并和远程dev分支相关联同时切换到本地dev分支
```

### 12.修改commit信息

**(1)没有push到远端，修改本地分支commit信息**

a. 未执行git push
之前可以使用如下的命令进行操作(只能撤销最近一次的commit)

```
git  reset --soft commit_id # (commit_id可以git reflog查看)

git commit -m "fix commit"  #重新提交信息
```

b. 如果要修改前面多出提交的历史信息，可以采用(2)里面的方法，只是不需要执行git push

命令总结：

```
git checkout -b dev

git rebase -i HEAD~5
```

把需要修改的commit信息前的pick改成edit

```
git commit --amend

git rebase --continue
```

多次重复执行前面两个命令直到更新

**(2) 已经push到远端 ，修改本地分支commit信息和远程分支commit信息**

命令总结：

```
git checkout -b dev  #(切换到dev分支)

git rebase -i HEAD~5  #(对最近5个提交记录进行rebase操作)
```

把需要修改的commit信息前的pick改成edit 
(linux下一般通过vim进行操作，即输入i进入编辑模式，修改对应内容，然后esc，接着输入:wq保存退出)

```
git commit --amend  #(输入i进入修改模式，修改commit信息，修改完后使用esc退出修改模式，接着输入:wq保存修改)

git rebase --continue
```

多次重复执行前面两个命令直到更新

```
git push origin dev -f
```

**下面是详细介绍如何修改已经push 的commit 的信息**
原文链接：
<https://blog.csdn.net/qq_39956074/article/details/83992286> 

**如何修改已经push 的commit 的信息**
A. `git rebase -i HEAD~5`
最新提交的版本为倒数第一个版本，5表示倒数第5个版本，这个数字可以修改，如改成2

![学习笔记-学习笔记mediaimage27.png-2020-12-05-16-49-50](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/学习笔记-学习笔记mediaimage27.png-2020-12-05-16-49-50.png)

前5行即为`HEAD～5`所提交的信息，第一行为倒数第五个版本的commit信息，第五行为倒数第一个版本commit信息，每行开头是pick，然后是commit id， 然后是commit信息

B.输入i进入修改模式，将需要修改的commit信息前的pick改成edit，修改完后使用esc退出修改模式，接着输入:wq保存修改。

C.命令行输入 `git commit --amend`，输入i进入修改模式，修改commit信息，修改完后使用esc退出修改模式，接着输入:wq保存修改。

【注】保存之后 `git rebase --continue`还没有使用之前还可以使用`git commit --amend`继续修改这条commit信息，但如果提交了就只能从头再来了，即使用`git rebase -i HEAD~5 `把pick改成edit保存退出，然后`git commit --amend`，保存修改信息之后屏幕输出以下内容

保存修改后命令行会输出以下内容
```
[detached HEAD fbe9591] 20190716c, bs 16, lr 0.001, maxiter 60000, steps "(50000, 55000)", 8000
 

Date: Mon Jul 15 18:11:43 2019 +0800
 
1 file changed, 3 insertions(+), 3 deletions(-)

```
D.命令行输入`git rebase --continue`

```
(py3) jason@jason:~/workspace/mask-detection$ git rebase --continue
 
Stopped at 896acbdf7545b0e42ff761376a2cdbca899b445d... 20190715c, bs 8, lr 0.0025, maxiter 60000, steps "(50000, 55000)", 8000
 
You can amend the commit now, with
 
 
 
git commit --amend
 
 
 
Once you are satisfied with your changes, run
 
 
 
git rebase --continue

```
输出这些信息是因为我们把多个pick改成了edit，因此继续修改commit信息直到全部修改完成，如下所示

```
(py3) jason@jason:~/workspace/mask-detection$ git commit --amend
 
[detached HEAD 70929e1] 20190715e, bs 8, lr 0.0025, maxiter 60000, steps "(50000, 55000)", 8000
 
Date: Mon Jul 15 18:19:56 2019 +0800
 
1 file changed, 4 insertions(+), 4 deletions(-)
 
(py3) jason@jason:~/workspace/mask-detection$ git rebase --continue
 
Successfully rebased and updated refs/heads/jason.

```
E.`git push origin dev -f`
将本地更新推送到远程分支上，必须加上-f，否则我们edit的commit会添加到commit后面
```
(py3) jason@jason:~/workspace/mask-detection$ git push origin dev -f
 
Password for 'http://jason@git.sankuai.com': 输入密码
 
Counting objects: 40, done.
 
Delta compression using up to 12 threads.
 
Compressing objects: 100% (40/40), done.
 
Writing objects: 100% (40/40), 7.75 KiB | 0 bytes/s, done.
 
Total 40 (delta 31), reused 0 (delta 0)
 
remote:
 
remote: Create pull request for jason:
 
remote: http://git.sankuai.com/users/lvtingxun/repos/mask-detection/compare/commits?sourceBranch=refs/heads/dev
 
remote:
 
To http://jason@***.git
 
+ b26a84a...70929e1 dev -> dev (forced update)

```

### 13.删除commit信息

git 删除远程分支上的某次提交原文：
<https://blog.csdn.net/QQxiaoqiang1573/article/details/68074847> 

**(1) 没有push到远端，删除本地commit信息**

A.删除最后一次提交记录

git reflog能查看所有历史操作记录，如果只想看commit信息，可以使用git
log，两者都能查到commit id

![IMG_257](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-58-24-7d7b962a0e07f5d49418c4268577902f-image28-614ef5.png){width="5.854166666666667in"
height="1.21875in"}

```
 git revert HEAD 
```
将回到倒数第二次提交后的版本，但本次操作会生成commit信息进行提交（输入i进入编辑状态，编辑完信息后按ESC，接着输入:wq保存退出）

![IMG_258](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-58-49-1d7bb19fe4188d6de19a5120f330096e-image29-5332f5.png){width="5.822916666666667in"
height="3.53125in"}

保存退出后输出如下，此时已经回退到倒数第二次提交的时候：

![IMG_259](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-59-20-1deb9320af5a425d8e1e02ca5c9184e8-image30-40c5b0.png){width="5.09375in"
height="0.6354166666666666in"}

通过git
log查看提交的记录，发现会生成一次新的commit信息，但是内容已经更新到之前的了

![IMG_260](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-59-33-3d49d3ec358fcd726421df18e3439ff2-image31-e7bed9.png){width="5.875in"
height="3.5208333333333335in"}

或者
`git reset --hard HEAD^ `注意后面有个^表示将回到倒数第二次提交后的版本

![IMG_261](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-59-47-fc603198cc94a93c22b3c1a4cf86ae01-image32-05ae14.png){width="3.3125in"
height="0.3854166666666667in"}

操作前的提交记录

![IMG_262](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/16-59-55-db53e89c0d0421c1afd2dc1c9e257bec-image33-a0649c.png){width="5.802083333333333in"
height="3.4583333333333335in"}

操作后的提交记录

`git log`

![IMG_263](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-00-06-7192d4ded3c4a88a0a438d4c4ae50a64-image34-e57f36.png){width="5.84375in"
height="3.5104166666666665in"}

[注] revert会生成一次新的提交，之前commit的信息还在，reset
则不会保留之前的提交记录信息

B.删除历史提交中的某次或者多次提交记录

例子：删除最后一次和倒数第三次提交记录

1) `git log` 找到你要删除的最远的`commit id`，本次测试选择了红色框的commit信息进行删除，也可以通过`git reflog`查看`commit id`

`git log`

![IMG_264](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-00-16-7805d35ac338422bfca0392abf72374d-image35-79c71e.png){width="5.854166666666667in"
height="4.5in"}

2)` git rebase -i HEAD~5`
最新提交的版本为倒数第一个版本，5表示倒数第5个版本，这个数字可以修改，如改成3进入下面的编辑页面，或者git
rebase -i "commit id"^   注意后面有个^符号，加不加""都可以，

```
git rebase -i HEAD~3 
```
(输入i进入编辑状态，删除第一行的内容，编辑完信息后按ESC，接着输入:wq保存退出)

![IMG_265](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-00-29-3787014405122b6bab510595d1f67c8f-image36-58d7e9.png){width="5.8125in"
height="3.1979166666666665in"}

删除第一行内容和第三行内容，即删除倒数第三次提交和最后一次提交的内容

![IMG_266](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-00-46-907a7552e60ade951ac68fefd0ae0475-image37-5a4873.png){width="4.864583333333333in"
height="1.2083333333333333in"}

保存退出后输出如下，此时回到删除改提交之前的那次提交后的状态，即commit信息为"删除commit信息2"

![IMG_267](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-00-54-7861202049bf28c4e0b02a0e0cfb9646-image38-d2549a.png){width="5.854166666666667in"
height="1.6041666666666667in"}

此时`git log`，回到了要删除commit信息前一次提交的状态

![IMG_268](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-01-5f3dd4037789e1471433f7b4c6471dd8-image39-3701ae.png){width="5.822916666666667in"
height="3.3541666666666665in"}

但有冲突，需要解决，冲突的文件内容如下所示

![IMG_269](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-14-79701861ba33c16dd061af7ab8d9fdb2-image40-3604cf.png){width="5.875in"
height="0.9270833333333334in"}

a)，解决冲突文件后内容如下

![IMG_270](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-27-8d95fbbaac75e564a6e381a823963be1-image41-b9f423.png){width="3.1354166666666665in"
height="0.3541666666666667in"}

```
git add .

git rebase --continue  #（直接退出文件，通过:q退出）
```

![IMG_271](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-34-f3588fbd8ff4cc8f57fd7b52145b133d-image42-d1b4a6.png){width="5.84375in"
height="2.15625in"}

如果没有使用`git add . `而直接使用`git rebase --continue`会提示下面的信息

![IMG_272](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-45-0117a0f019fd2f1c5b58c3d84d94fa01-image43-0c7c1c.png){width="3.2083333333333335in"
height="0.6979166666666666in"}

此时输出如下：

![IMG_273](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-52-5e1c6ec87cd49947634dde35b1dbca61-image44-25d6d0.png){width="4.020833333333333in"
height="0.6458333333333334in"}

`git log`发现第三次和第五次提交的commit信息已经删除了

![IMG_274](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-01-58-1f3bf58e1d2102553824b87ab13bbd30-image45-3c423b.png){width="5.854166666666667in"
height="4.385416666666667in"}

b) 不解决冲突，通过`git rebase --skip`
跳过解决冲突，直接回退到第三次提交后的状态。类似于使用git reset回退

![IMG_275](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-21-14-1867d75af9c5dc305130349b6adcbd8f-image46-2d79c2.png){width="3.7604166666666665in"
height="0.375in"}

```
git log
```

![IMG_276](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-21-06-ca6d1ccb0acf2b7980d2193ccd72ddc7-image47-6c2615.png){width="5.854166666666667in"
height="2.65625in"}

文件中的内容:

![IMG_277](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-02-06-b5ddd5f3cf54db08d07746d951b5039f-image48-9450fb.png){width="5.885416666666667in"
height="0.4895833333333333in"}

c)，不解决冲突，通过`git rebase --abort`回到最新提交的状态，所有东西都回到rebase前，因此此时并没有删除commit信息，要想删除就得解决冲突。

![IMG_278](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-21-44-83545c1a9844f53a24e53f3b2bca1aa6-image49-eea995.png){width="4.1875in"
height="0.375in"}

`git log`

![IMG_279](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/19/13-20-53-4c5865f227274bbf92353bbd22b50d65-image50-2cb8e9.png){width="5.8125in"
height="4.197916666666667in"}

**(2) 已经push到远端，删除本地commit信息和远程commit信息**

在(1)完成的基础上，只需要加上`git push orgin master -f`
即可将master分支上的commit信息删除

![IMG_280](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-02-23-f398f7bb150853bc40db13154a57314a-image51-93b6f3.png){width="5.145833333333333in"
height="1.5104166666666667in"}

`git push orgin master -f`

![IMG_281](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-02-30-80bdcc06dbf6463f2baf0a7387760fb5-image52-dea17a.png){width="6.802083333333333in"
height="2.5416666666666665in"}

远程最新的文档内容：

![IMG_282](https://raw.githubusercontent.com/kuangyl-max/markdownMedia/master/img/fix-dir/media/2020/12/05/17-02-37-aebe80c876b2d1692544da5a0b26cf4c-image53-1fecda.png){width="6.697916666666667in"
height="2.9270833333333335in"}

## 七、分支策略

**1.在实际开发中，我们应该按照几个基本原则进行分支管理：**

1) master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

2) 干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

3) 每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了

**2.分支是否推送到远程**

1) master分支是主分支，因此要时刻与远程同步；

2) dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

3) bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

4) feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

 

## 八、bug分支和暂存工作现场

### 1.bug分支的用途

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成又不想commit时，先把工作现场暂存，然后去修复bug，修复后，再`git stash pop`，回到工作现场。

 

### 2.创建bug分支的流程

假设暂存现场在dev分支，总体流程如下：

1. git stash  # 暂存工作现场（去修bug，假设bug在master分支上）

2. git checkout master

3. 修改bug

4. git add .

5. git commit -m "fix bug on master"

6. git push origin master

7. git checkout dev  切到dev分支

8. git stash list 会出现stash@{0}: WIP on dev: 6224937 add mergegit

9. git stash pop 将之前本地dev分支暂存的环境恢复出来

10. (还可以通过 git stash apply stash@{0}进行恢复，再删除stask内容git stash drop)

11. git stash list  再次查看还有暂存现场没有

 

## 九、feature分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，用`git branch -d <name>`，若要强行删除使用-D

 

## 十、github远程仓库

### 1.使用ssh创建key

为了和远程库相关联需要添加key，如果不加好像每次需要输密码：

```
ssh-keygen -t rsa -C "***@qq.com" # 后面的邮箱根据自己的情况修改

```
该命令用于
创建id_rsa文件和id_rsa.pub文件，id_rsa是私钥，id_rsa.pub是公钥用于添加到github的ssh
key里面。文件位于用户目录下的.ssh文件里面

### 2.本地仓库和远程仓库关联

**第一种情况：远程只有仓库没有内容时，将本地已经写好的代码关联到远程：**

1. git init

2. git add .

3. git commit -m "first commit"

4. git remote add origin git@github.com:JasonDu1993/learngit.git
5. 关联远程库，相当于让origin等于后面这串地址

6. git push -u origin master
7. -u只在第一次推送分支时使用，将本地master推到远程master分支上

8. 关联完之后就可以切分支或者创建其他分支了

9. git checkout master

10. git push origin master  将到本地master分支内容推到远程master分支上

11. git checkout -b dev  创建本地dev分支并切换到本地dev分支

12. git push origin dev  将本地dev分支推到远程dev分支

一般master分支和dev分支都会推到远程


**第二种情况：远程仓库有内容，直接克隆到本地**

1. git clone git@github.com:JasonDu1993/gitskills.git

2. git branch -a 查看本地分支和远程分支

3. git checkout -b dev origin/dev  如果本地没有dev分支将会报错

4. git add file_name

5. git commit -m "记录提交信息"

6. git push origin dev

在GitHub上，可以任意Fork开源仓库，这样拥有fork后的仓库的读写权限，你就可以push到你fork之后的这个仓库了，当然也可以推送pull
request给官方仓库来贡献代码。

 

### 3.关联仓库出现问题解决办法

1）如果`git checkout -b dev origin/dev`迁出分支出现问题

```
fatal: Cannot update paths and switch to branch 'dev' at the same time.


Did you intend to checkout 'orgin/dev' which can not be resolved as
commit?
```
解决办法是先`git fetch`，再`git checkout -b dev origin/dev`

 

2）如果`git push`失败，先`git pull`

如果`git pull`失败，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：

`git branch --set-upstream dev origin/dev`，（现在好像改成`git branch --set-upstream-to=origin/dev dev`）

然后在`git pull`，`git push origin master`

 

3） `git error: RPC failed; result=22, HTTP code = 411`
<https://blog.csdn.net/love_rongrong/article/details/12557347>

解决办法：改一下git的传输字节限制

```
git config http.postBuffer  524288000
```

4）`error: RPC failed; result=22, HTTP code = 413`

fatal: The remote end hung up unexpectedly 

fatal: The remote end hung up unexpectedly

Everything up-to-date

这两个错误看上去相似，一个是411，一个是413

下面这个错误添加一下密钥就可以了

首先`ssh-keygen -t rsa -C "abc@bupt.edu.cn"`生成密钥

 

### 4.有时候不想解决冲突(建议还是解决冲突好）

1) 从远处拉取最新的东西到本地（不想解决冲突直接接受远程仓库内容）

```
  git fetch --all //至少下载到本地不进行合并

  git reset --hard origin/dev

  git pull
```

2)，将本地更新强制推到远程，不想解决和远程的冲突

```
git push --force origin dev 或者git push -f origin dev
```


### 5.删除分支

```
#删除远程分支
git push origin --delete dev

#删除本地分支
git branch -d dev
```

### 6.创建远程分支

 如果想把本地的test分支提交到远程仓库，并作为远程仓库的master分支，或者作为另外一个名叫test的分支。

```
git push origin test:master   #提交本地test分支作为远程的master分支

git push origin test:test  #提交本地test分支作为远程的test分支
```
### 7.查看远程分支commit信息用于回退到远程分支的某个版本

```
git fetch --all

git log

git reset --hard commit_id
```


### 8.修改远程仓库名称

1) 在本地仓库删除远程仓库：

```
git remote rm origin 1
```

2 )修改Github仓库名称： 

在Github页面中，进入要修改的仓库，在页面上方选择"Settings"，即可重命名远程仓库。

3) 添加新的远程仓库：

```
git remote add origin https://github.com/JasonDu1993/gitskill.git
```

### 9. fork别人的仓库后如何同原仓库保持同步更新


Github进行fork后如何与原仓库同步l原文链接：
<https://blog.csdn.net/matrix_google/article/details/80676034> 

1）git remote -v #查看远程目录地址

2）git branch -a  #查看所有分支情况

3）git remote add upstream 你fork之前的源仓库地址 #该操作将源仓库和上游代码库upstream相关联（重要1）

4）git remote -v #再次查看远程目录的地址

5）git stash  #暂存自己的工作状态（不是必须的，如果改了代码没有push则需要）

6）git fetch upstream  #抓取源仓库的修改文件（重要2）

7）git branch -a  #再次查看所有分支情况

8）git checkout master #切换到master分支

9）git merge upstream/master #将本地代码和源代码保持同步（最重要3）

10）git stash pop #将暂存区的环境恢复到工作区上传到远程仓库

11）git add .

12）git commit -m "update forked repository at 2019.06.05"

13）git push origin master #上传新的代码到自己的远程master分支

### 10. git pull can't update

```
No tracked branch configured for branch dev or the branch doesn't
exist. To make your branch track a remote branch call, for example, git
branch --set-upstream-to origin/dev dev
```

## 十一、多人合作流程

因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示"no tracking
information"，则说明本地分支和远程分支的链接关系没有创建，用命令`git
branch --set-upstream branch-name origin/branch-name`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

 

## 十二、版本标签

标签用于发布版本时使用，相当于给某次commit取个名字

**1，添加标签**

* `git tag <name> `用于新建一个标签一般取名name为v0.1等，默认为HEAD，也可以指定一个`commit id`

* `git tag -a <tagname> -m "blablabla..." `可以指定标签信息

* `git tag `可以查看所有标签

 

**2，删除标签**

* `git tag -d <tagname> `删除一个本地标签

* `git push origin :refs/tags/<tagname>` 删除一个远程标签

* `git push origin <tagname> `推送一个本地标签

* `git push origin --tags` 推送全部未推送过的本地标签

 

## 十三，忽略特特殊文件

在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件，同时提交这个文件到Git。

 

例子如下，.gitignore文件内容如下：
```config

# Windows:

Thumbs.db

ehthumbs.db

Desktop.ini

 

# Python:

*.py[cod]

*.so

*.egg

*.egg-info

dist

build

# iead

.idea

# My configurations:

db.ini

deploy_key_rsa

```

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；

2. 忽略编译生成的中间文件、可执行文件等，比如Java编译产生的.class文件；

3. 忽略敏感信息的配置文件，比如存放口令的配置文件。

 

## 十四、自定义Git服务器

假设你已经有sudo权限的用户账号并且该教程是在ubuntu下介绍的

1. 安装git：
```
sudo apt-get install git
```
2. 创建一个git用户，用来运行git服务：

```
sudo adduser git
```
3. 创建证书登录：
收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到`/home/git/.ssh/authorized_keys`文件里，一行一个。
4. 初始化Git仓库：

先选定一个目录作为Git仓库，假定是`/srv/sample.git`，在/srv目录下输入命令：
```
sudo git init --bare sample.git
```

Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：

```
sudo chown -R git:git sample.git
```

5. 禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

`git:x:1001:1001:,,,:/home/git:/bin/bash
`
改为：

`git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`

这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

6. 克隆远程仓库：

现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

```
git clone git@server:/srv/sample.git


Cloning into 'sample'...

warning: You appear to have cloned an empty repository.

```


**管理公钥**

如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。

**管理权限**

使用**Gitolite**就是这个工具管理权限

## 十五、git常见错误及解决办法

**1.git缓存太小下载不下来大文件**

解决：`git config --global http.postBuffer 524288000`

**2.有图片文件**

```
Cloning into 'survivors'...

remote: Counting objects: 124, done.

remote: Compressing objects: 100% (120/120), done.

error: RPC failed; curl 18 transfer closed with outstanding read data
remaining

fatal: The remote end hung up unexpectedly

fatal: early EOF

fatal: index-pack failed
```

解决：`git clone http://github.com/large-repository --depth 1`

**3.更完美的解决下载不下来方法**

```
error: RPC failed; curl 18 transfer closed with outstanding read data
remaining

fatal: The remote end hung up unexpectedly

fatal: early EOF

fatal: index-pack failed
```

解决：

方法一：`git config --global http.postBuffer 524288000`

如果不行

方法二：`git clone http://github.com/large-repository --depth 1`

如果还不行

方法三：一般clone http方式的容易产生此问题，改成SSH的方式也有效，即https://改为git://

**4.git remote: HTTP Basic: Access denied 错误解决办法**

来源：<https://www.cnblogs.com/lydiawork/p/10287797.html>

问题描述：
git push 报 HTTP Basic: Access denied 错误

原因：本地git配置的用户名、密码与gitlabs上注册的用户名、密码不一致。
**解决方案：**
1. 如果账号密码有变动 用这个命令 `git config --system --unset
credential.helper` 重新输入账号密码 应该就能解决了
2. 如果用了第一个命令 还不能解决问题那么 用这个命令：
`  git config --global http.emptyAuth true`
3.如果以上两个方法不起作用，那么采用以下方法：

进入控制面板》用户账号》凭据管理器？windows凭据》普通凭据，在里面找到git，点开编辑密码，更新为最新密码之后就可以正常操作了。

