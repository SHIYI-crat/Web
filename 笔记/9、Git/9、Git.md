﻿# Git

## 1、Git概念

### 1.1 关于版本控制

**文件的版本管理的问题**

* 操作麻烦：每次都需要复制→粘贴→重命名
* 命名不规范：无法通过文件名知道具体做了哪些修改
* 容易丢失：如果硬盘故障或不小心删除，文件很容易丢失
* 协作困难：需要手动合并每个人对项目文件的修改，合并时极易出错



**版本控制软件**

* 概念：**版本控制软件是一个用来记录文件变化，以便将来查阅特定版本修订情况的系统，因此有时也叫做“版本控制系统”**
* 解释：把**手工管理文件版本**的方式,改为由**软件管理文件的版本**;这个负责管理文件版本的软件，叫做“版本控制软件”。



**使用版本控制软件的好处**

* 操作简便：只需识记几组简单的终端命令，即可快速上手常见的版本控制软件
* 易于对比：基于版本控制软件提供的功能，能够方便地比较文件的变化细节，从而查找出导致问题的原因
* 易于回溯：可以将选定的文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态
* 不易丢失：在版本控制软件中，被用户误删除的文件，可以轻松的恢复回来
* 协作方便：基于版本控制软件提供的分支功能，可以轻松实现多人协作开发时的代码合并操作



**版本控制系统的分类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/2acb4f36d517415b80e6cdc3eaf61f06.png#pic_center)


1. 本地版本控制系统

![在这里插入图片描述](https://img-blog.csdnimg.cn/570a1876c48e42eeaa520575eec491cf.png#pic_center)


   * 优点：使用软件来记录文件的不同版本，提高了工作效率，降低了手动维护版本的出错率
   * 缺点：**单机运行，不支持多人协作开发；版本数据库故障后，所有历史更新记录会丢失**

2. 集中化的版本控制系统（SVN）

![在这里插入图片描述](https://img-blog.csdnimg.cn/619e06de61c640d99e1b747c5490522e.png#pic_center)


* 特点:基于服务器、客户端的运行模式
  * 服务器保存文件的所有更新记录
  * 客户端只保留最新的文件版本
* 优点:联网运行，支持多人协作开发
* 缺点:
  * **不支持离线提交版本更新**
  * **中心服务器崩溃后，所有人无法正常工作**
  * **版本数据库故障后，所有历史更新记录会丢失**

3. 分布式版本控制系统（Git）

![在这里插入图片描述](https://img-blog.csdnimg.cn/bdf4807a6f7e42888d8dbdf70a04965c.png#pic_center)


* 特点:基于服务器、客户端的运行模式

  * 服务器保存文件的所有更新版本

  * 客户端是服务器的完整备份，并不是只保留文件的最新版本

* 优点:
    * 联网运行，支持多人协作开发
    * 客户端断网后支持离线本地提交版本更新
    * 服务器故障或损坏后，可使用任何一个客户端的备份进行恢复



### 1.2 Git基础概念

**Git概念**

* Git是一个开源的分布式版本控制系统，是目前世界上最先进、最流行的版本控制系统。可以快速高效地处理从很小到非常大的项目版本管理
* 特点:项目越大越复杂，协同开发者越多，越能体现出Git的高性能和高可用性!



**Git特性**

* Git之所以快速和高效，主要依赖于它的如下两个特性:
  1. **直接记录快照，而非差异比较**
  2. **近乎所有操作都是本地执行**

* 传统的版本控制系统（例如SVN)是基于差异的版本控制，它们存储的是一组基本文件和每个文件随时间逐步累积的差异

![在这里插入图片描述](https://img-blog.csdnimg.cn/f8c06b47d7ed47c987d34cf67a8c701a.png#pic_center)


* 好处：节省磁盘空间
* 缺点：耗时、效率低、在每次切换版本的时候，都需要在基本文件的基础上，应用每个差异，从而生成目标版本对应的文件

* Git快照是在原有文件版本的基础上重新生成一份新的文件，类似于备份。为了效率，如果文件没有修改,Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/331f0a9ffe7b4f118f308579917e59dc.png#pic_center)


* 缺点:占用磁盘空间较大
* 优点:版本切换时非常快，因为每个版本都是完整的文件快照，切换版本时直接恢复目标版本的快照即可
* 特点:空间换时间

* 在Git 中的绝大多数操作都只需要访问本地文件和资源，一般不需要来自网络上其它计算机的信息
* 特性:
  1. 断网后依旧可以在本地对项目进行版本管理
  2. 联网后，把本地修改的记录同步到云端服务器即可



**Git中的三个区域**

* 使用Git 管理的项目，拥有三个区域，分别是：
  1. **工作区：处理工作的区域**
  2. **暂存区：已完成的工作的临时存放区域，等待被提交**
  3. **Git仓库：最终的存放区域**



**Git中的三种状态**

![在这里插入图片描述](https://img-blog.csdnimg.cn/5d74b3e15b6042b4afb2a893cba55a48.png#pic_center)


* 注意:
  * 工作区的文件被修改了，但还没有放到暂存区，就是已修改状态。
  * 如果文件已修改并放入暂存区，就属于已暂存状态。
  * 如果Git仓库中保存着特定版本的文件，就属于已提交状态。



**基本的Git工作流程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/aaa129261c854ecb9a7056c472f4fea0.png#pic_center)


* 基本的Git工作流程如下:
  1. 在工作区中修改文件
  2. 将你想要下次提交的更改进行暂存
  3. 提交更新，找到暂存区的文件，将快照永久性存储到Git 仓库



## 2、Git基础操作

### 2.1 安装并配置Git

**下载并安装**

* 下载地址：[Git - Downloads (git-scm.com)](https://git-scm.com/downloads)

![在这里插入图片描述](https://img-blog.csdnimg.cn/63ba339f57de4d5fabaf8a5d6267a23f.png#pic_center)




**配置用户信息**

* **安装完Git之后，要做的第一件事就是设置自己的用户名和邮件地址**。因为通过Git对项目进行版本管理的时候，Git需要使用这些基本信息，来记录是谁对项目进行了操作:

~~~markdown
git config --global user.name "xxxx"
git config --global user.email "xxxxxxxx"
~~~

* **注意:如果使用了--global选项，那么该命令只需要运行一次，即可永久生效**

* 通过git config --global user.name和git config --global user.email配置的用户名和邮箱地址，会被写入到C:/Users/用户名文件夹/.gitconfig文件中



**检查配置信息**

* 除了使用记事本查看全局的配置信息之外，还可以运行如下的终端命令，快速的查看Git的全局配置信息:

~~~markdown
# 查看所有的全局配置项
git config --list --global

# 查看指定的全局配置项
git config user.name
git config user.email
~~~



**获取帮助信息**

* 可以使用git help < verb >命令，无需联网即可在浏览器中打开帮助手册，例如:

~~~markdown
# 打开git config 命令的帮助手册
git help config
~~~

* 如果不想查看完整的手册，那么可以用-h选项获得更简明的"help" 输出:

~~~markdown
# 想要获取git config命令的快速参考
git config -h
~~~



### 2.2 Git的基本操作

**获取Git仓库的两种方式**

1. **将尚未进行版本控制的本地目录转换为Git 仓库**(git init)
2. **从其它服务器克隆一个已存在的Git 仓库**(git clone xxx)



**在现有目录中初始化仓库**

* 如果自己有一个尚未进行版本控制的项目目录，想要用Git.来控制它，需要执行如下两个步骤:
  1. 在项目目录中，通过鼠标右键打开“**Git Bash Here**"
  2. 执行**git init**命令将当前的目录转化为Git 仓库
* git init 命令会创建一个名为.git的隐藏目录，这个.git目录就是当前项目的Git仓库，里面包含了初始的必要文件，这些文件是Git仓库的必要组成部分。



**工作区文件的4种状态**

![在这里插入图片描述](https://img-blog.csdnimg.cn/5ce7fd306f194526aecb5e6766a4d0ce.png#pic_center)


* **git操作的终极结果：让工作区的文件都处于“未修改”的状态**



**检查文件的状态**

* 先创建一个文件夹，里面新建一个index.html文件，可以使用**git status**命令查看文件处于什么状态，例如:

![在这里插入图片描述](https://img-blog.csdnimg.cn/65422f21c10345779fa205bd27692c32.png#pic_center)


* 在状态报告中可以看到新建的index.html文件出现在Untracked files(未跟踪的文件）下面
* 未跟踪的文件意味着Git在之前的快照(提交）中没有这些文件;Git不会自动将之纳入跟踪范围除非明确地告诉它“我需要使用Git 跟踪管理该文件”

* 使用git status输出的状态报告很详细，但有些繁琐。如果希望以精简的方式显示文件的状态，可以使用如下两条完全等价的命令，其中-s是--short的简写形式:

~~~markdown
# 以精简的方式显示文件状态
git status -s
git status --short
~~~

* 未跟踪文件前面有红色的??标记，例如：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2da8bfccf494418dbd23eb63bdcc034b.png#pic_center)






**跟踪新文件**

* 使用命令git add开始跟踪一个文件。所以，要跟踪index.html文件，运行如下的命令即可:

~~~markdown
git add xxx(文件名)
~~~

* 此时再运行 git status 命令，会看到 index.html文件在Changes to be committed这行的下面，说明已被跟踪，并处于暂存状态:

![在这里插入图片描述](https://img-blog.csdnimg.cn/b821f6a7180749118c4290405b6c6b1c.png#pic_center)


* 以精简的方式显示文件的状态，新添加到暂存区中的文件前面有绿色的A标：

![在这里插入图片描述](https://img-blog.csdnimg.cn/6241e4c17e5a4f518f5df7a6aaecfbe1.png#pic_center)




**提交更新**

* 现在暂存区中有一个index.html文件等待被提交到Git仓库中进行保存。可以执行git commit命令进行提交,其中-m选项后面是本次的提交消息，用来对提交的内容做进一步的描述:

~~~markdown
git commit -m "新建了index.html文件"
~~~

* 提交成功后，显示如下信息：

![在这里插入图片描述](https://img-blog.csdnimg.cn/6605d0eb6596488d86b5252e6dff054c.png#pic_center)


* 提交成功之后，再次检查文件的状态，得到提示如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/6c095dcdf5d34a85ac944159e910a6db.png#pic_center)


* 证明工作区中所有的文件都处于“未修改”的状态，没有任何文件需要被提交

![在这里插入图片描述](https://img-blog.csdnimg.cn/08511fc4a8eb463bb34eef6761c04fdb.png#pic_center)






**对已提交的文件进行修改**

* 目前，index.html文件已经被Git跟踪，并且工作区和Git仓库中的 index.html文件内容保持一致。当我们修改了工作区中 index.html的内容之后，再次运行git status和 git status -s命令，会看到如下的内容

![在这里插入图片描述](https://img-blog.csdnimg.cn/4574466ac541440b887048ac957fbc8f.png#pic_center)


* 文件index.html出现在Changes not staged for commit这行下面，说明已跟踪文件的内容发生了变化，但还没有放到暂存区
* **注意:修改过的、没有放入暂存区的文件前面有红色的M标记**



**暂存已修改的文件**

* 目前，工作区中的 index.html文件已被修改，如果要暂存这次修改，需要再次运行**git add** 命令，这个命令是个多功能的命令，主要有如下3个功效:
  1. 可以用它开始跟踪新文件
  2. 把已跟踪的、且已修改的文件放到暂存区
  3. 把有冲突的文件标记为已解决状态

![在这里插入图片描述](https://img-blog.csdnimg.cn/6bbb49ca299c40afa9fbbddeedb9b013.png#pic_center)




**提交已暂存的文件**

* 再次运行**git commit -m "提交消息"**命令，即可将暂存区中记录的index.html 的快照，提交到Git仓库中进行保存:

![在这里插入图片描述](https://img-blog.csdnimg.cn/fa76e4c3396b4e8793aa090e51634b29.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/6b6d9ec3faef4e52860b047bf30bd138.png#pic_center)




**撤销对文件的修改**

* 撤销对文件的修改指的是:把对工作区中对应文件的修改，还原成Git仓库中所保存的版本
* 操作的结果:所有的修改会丢失，且无法恢复!危险性比较高，请慎重操作!

![在这里插入图片描述](https://img-blog.csdnimg.cn/3711f3b9440948da90895769fbf2bfed.png#pic_center)


* **撤销操作的本质:用Git仓库中保存的文件，覆盖工作区中指定的文件**



**向暂存区中一次性添加多个文件**

* 如果需要被暂存的文件个数比较多，可以使用如下的命令，一次性将所有的新增和修改过的文件加入暂存区

~~~markdown
git add .
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/9b51a282e5b345c1b6292b3d05ac12d8.png#pic_center)






**取消暂存的文件**

* 如果需要从暂存区中移除对应的文件，可以使用如下的命令:

~~~markdown
git reset HEAD 要移除的文件名
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/925600a78c2e4676b734108409b8e8dc.png#pic_center)


~~~markdown
# 批量移除
git reset HEAD .
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/844058a62a7e4662b07800ebb15f0bc4.png#pic_center)




**跳过使用暂存区域**

* Git标准的工作流程是工作区→暂存区→Git仓库，但有时候这么做略显繁琐，此时可以跳过暂存区，直接将工作区中的修改提交到Git仓库，这时候Git工作的流程简化为了工作区→Git仓库。
* Git提供了一个跳过使用暂存区域的方式，只要在提交的时候，给**git commit加上-a**选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过git add步骤:

~~~markdown
git commit -a -m "描述信息"
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/3362742b56444f46a56a1aaef8ada23a.png#pic_center)




**移除文件**

* 从Git仓库中移除文件的方式有两种:
  1. 从Git 仓库和工作区中同时移除对应的文件
  2. 只从Git仓库中移除指定的文件，但保留工作区中对应的文件

~~~markdown
# 从Git仓库和工作区中同时移除index.js 文件
git rm -f index.js

# 只从 Git仓库中移除index.css，但保留工作区中的 index.css文件
git rm --cached index.css
~~~



**忽略文件**

* 一般我们总会有些文件无需纳入Git的管理，也不希望它们总出现在未跟踪文件列表。在这种情况下，我们可以创建一个名为**.gitignore**的配置文件，列出要忽略的文件的匹配模式。
  文件.gitignore的格式规范如下:
  1. **以#开头的是注释**
  2. **以/结尾的是目录**
  3. **以/开头防止递归**
  4. **以!开头表示取反**
  5. **可以使用glob 模式进行文件和文件夹的匹配 (glob 指简化了的正则表达式)**

* 所谓的 glob模式是指简化了的正则表达式:
  1. 星号*匹配零个或多个任意字符
  2. [abc]匹配任何一个列在方括号中的字符（此案例匹配一个a或匹配一个 b或匹配一个c)
  3. 问号?只匹配一个任意字符
  4. 在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如[0-9]表示匹
     配所有0到9的数字)
  5. 两个星号* *表示匹配任意中间目录(比如a/ **/z可以匹配 a/z、 a/b/z或a/b/c/z等)

~~~markdown
# 忽略了所有的 .a文件
*.a

# 跟踪所有的lib.a，即便你在前面忽略了.a文件
!lab.a

# 只忽略当前目录下的TODO文件，而不忽略subdir/TODO
/TODO

# 忽略任何目录下名为build的文件夹
build/

# 忽略任何目录下名为build的文件夹
doc/*. txt

# 忽略doc/目录及其所有子目录下的.pdf文件
doc/**/*.pdf
~~~



**查看提交历史**

* 如果希望回顾项目的提交历史，可以使用git log这个简单且有效的命令

~~~markdown
# 按时间先后顺序列出所有的提交历史
git log

# 只展示最新的两条提交历史，数字可以按需进行填写
git log -2

# 在一行上展示最近两条提交历史的信息
git log -2 --pretty=oneline

# 在一行上展示最近两条提交历史的信息，并自定义输出的格式
# %h 提交的简写哈希值 %an 作者名字 %ar 作者修订日期，按多久以前的方式显示 %s 提交说明
git log -2 --pretty=format:"%h | %an | %ar | %s"
~~~



**回退到指定版本**

~~~markdown
# 在一行上展示所有的提交历史
git log --pretty=oneline

# 使用git reset --hard命令，根据指定的提交ID回退到指定版本
git reset --hard< CommitID >

# 在旧版本中使用git relog --pretty=online命令，查看命令操作的历史
git relog --pretty=oneline

# 再次根据最新的提交ID，跳转到最新的版本
git reset --hard< CommitID >
~~~



## 3、Github操作

### 3.1 关于开源



* 开源是指不仅提供程序还提供程序的源代码；闭源是只提供程序，不提供源代码

* 开源并不意味着完全没有限制，为了限制使用者的使用范围和保护作者的权利，每个开源项目都应该遵守开源许可协议（ Open Source License ) 

  1. BSD (Berkeley Software Distribution)

  2. Apache Licence 2.0

  3. GPL (GNU General Public License)

     * 具有传染性的一种开源协议，不允许修改后和衍生的代码做为闭源的商业软件发布和销售

     * 使用GPL的最著名的软件项目是:Linux

  4. LGPL (GNU Lesser General Public License)

  5. MIT(Massachusetts Institute of Technology, MIT)

     * 是目前限制最少的协议，唯一的条件:在修改后的代码或者发行包中，必须包含原作者的许可信息
     * 使用MIT的软件项目有: jquery、Node.js

* [各种开源协议介绍 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/open-source-license.html)

* 开源给使用者更多的控制权;开源让学习变得容易;开源才有真正的安全(我为人人，人人为我)

* 专门用于免费存放开源项目源代码的网站，叫做开源项目托管平台。目前世界上比较出名的开源项目托管平台主要有以下3个:
  * **Github(**全球最牛的开源项目托管平台，没有之一)
  * **Gitlab**(对代码私有性支持较好，因此企业用户较多)
  * **Gitee**(又叫做码云，是国产的开源项目托管平台。访问速度快、纯中文界面、使用友好)

* Github（Github≠Git）是全球最大的开源项目托管平台。因为只支持Git作为唯一的版本控制工具，故名GitHub。在Github中，你可以:
  * 关注自己喜欢的开源项目，为其点赞打call
  * 为自己喜欢的开源项目做贡献(Pull Request)
  * 和开源项目的作者讨论Bug和提需求(lssues)
  * 把喜欢的项目复制一份作为自己的项目进行修改(Fork)
  * 创建属于自己的开源项目
  * etc...



### 3.2 注册账号

* 访问Github 的官网首页https://github.com/
* 点击“**Sign up**”按钮跳转到注册页面
* 填写可用的**用户名、邮箱、密码**
* 通过点击箭头的形式，将验证图片摆正点击“**Create account**”按钮注册新用户
* 登录到第三步填写的邮箱中，**点击激活链接，完成注册**



### 3.3 远程仓库的使用

1. **新建空白远程仓库**

![在这里插入图片描述](https://img-blog.csdnimg.cn/3854e6113e424926a4eef29fa1061d51.png#pic_center)




2. **成功创建**

![在这里插入图片描述](https://img-blog.csdnimg.cn/ba3b8e5b3ad44da0b07dc376f314b5a5.png#pic_center)




3. **远程仓库的两种访问方式**

* Github 上的远程仓库，有两种访问方式，分别是HTTPS和SSH。它们的区别是:
  * **HTTPS:**零配置;但是每次访问仓库时，需要重复输入Github 的账号和密码才能访问成功
  * **SSH:**需要进行额外的配置;但是配置成功后，每次访问仓库时，不需重复输入Github的账号和密码
* 注意:在实际开发中，推荐使用SSH的方式访问远程仓库。



4. **使用HTTPS将本地仓库上传到Github**

![在这里插入图片描述](https://img-blog.csdnimg.cn/b64e638f97364a16b42d6906c62f55ca.png#pic_center)


* 修改本地文件暂存提交后想同步Github仓库直接 **git push**即可



5. **SSH key**

* SSH key的作用:实现本地仓库和Github之间免登录的加密数据传输

* SSH key的好处:免登录身份认证、数据加密传输

* SSH key由两部分组成，分别是:

  1. id_rsa(私钥文件，存放于客户端的电脑中即可)
  2. **id_rsa.pub**(公钥文件，需要配置到Github中)

  

6. **生成SSH key**

* 打开Git Bash
* 粘贴如下的命令，并将your_email@example.com替换为注册Github账号时填写的邮箱:
  * ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
* 连续敲击3次回车，即可在C\Users\用户名文件夹\.ssh目录中生成id_rsa和id_rsa.pub两个文件



7. **配置SSH key**

* 使用记事本打开id_rsa.pub文件，复制里面的文本内容
* 在浏览器中登录Github，点击头像-> Settings -> SSH and GPG Keys -> New SSH key
* 将id_rsa.pub文件中的内容，粘贴到Key对应的文本框中
* 在Title 文本框中任意填写一个名称，来标识这个Key 从何而来



8. **检测Github的SSH key是否配置成功**

* 打开Git Bash，输入如下命令并回车，输入yes看到如下信息，说明SSH key已经配置成功了：

![在这里插入图片描述](https://img-blog.csdnimg.cn/44b4231b7b314a07ad98f793ae1039be.png#pic_center)




9. **基于SSH将本地仓库上传到Github**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20734f1f66944cf19dc41b001c1554c5.png#pic_center)




10. **将远程仓库克隆到本地**

~~~mark
git clone 远程仓库的地址
~~~



## 4、Git分支操作

### 4.1 本地分支操作

**分支的概念**

* 相当于科幻电影的平行宇宙，在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发



**master(main)主分支**

* 在初始化本地Git仓库的时候，Git默认已经帮我们创建了一个名字叫做master(main)的分支。通常我们把这个master(main)分支叫做主分支。
* 在实际工作中，master(main)主分支的作用是:**用来保存和记录整个项目已完成的功能代码。**
* 因此，不允许程序员直接在master(main)分支上修改代码，因为这样做的风险太高，容易导致整个项目崩溃。



**功能分支**

* 由于程序员不能直接在master (main)分支上进行功能的开发，所以就有了功能分支的概念。
* 功能分支指的是专门用来开发新功能的分支，它是临时从master(main)主分支上分叉出来的，当新功能开发且测试完毕后，最终需要合并到master(main)主分支上，如图所示:

![在这里插入图片描述](https://img-blog.csdnimg.cn/451b759ac29d4d70b51cefdac8a46dfb.png#pic_center)




**查看分支列表**

~~~markdown
git branch
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/3115c556986848b9a52cb56053912c39.png#pic_center)


* 分支名字前面的*号表示**当前所处的分支**



**创建新分支**

* 使用如下的命令，可以**基于当前分支，创建一个新的分支**，此时，新分支中的代码和当前分支完全一样:

~~~markdown
git branch 分支名称
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/040bf8adc62e4144a501212dfa395210.png#pic_center)




**切换分支**

* 使用如下的命令，可以切换到指定的分支上进行开发:

~~~markdown
git checkout 分支名称
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/0f56a3c751464b239322e03f2b990077.png#pic_center)




**分支的快速创建和切换**

* 使用如下的命令，可以**创建指定名称的新分支**，并**立即切换到新分支**上:

~~~markdown
# -b 表示创建一个新分支
# checkout表示切换到刚才新建的分支上
git checkout -b 分支名称
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/a9dcb618cd274bdbac4837962e3d777d.png#pic_center)




**分支合并**

* 功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到master主分支上:

~~~markdown
# 1.切换到main分支
git checkout main

# 2.在main分支上运行git merge命令，将login分支的代码合并到main分支
git merge login
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/7852adb4c1594154b45e1ba36260de73.png#pic_center)


* 合并分支时的注意点:假设要把C分支的代码合并到A分支,则必须先切换到A分支上，再运行git merae命令，来合并C分支!



**删除分支**

* 当把功能分支的代码合并到 master主分支上以后，就可以使用如下的命令，删除对应的功能分支:

~~~markdown
git branch -d 分支名称
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/5b75f8a5a404491ebe8c21174b208d9f.png#pic_center)




**遇到冲突时的分支合并**

* 如果在两个不同的分支中，对同一个文件进行了不同的修改，Git就没法干净的合并它们。此时，我们需要打开这些包含冲突的文件然后手动解决冲突

~~~Markdown
# 假设：在把reg分支合并到main分支期间，代码发生了冲突
git checkout main
git merge reg

# 打开包含冲突的文件，手动解决冲突之后(vscode智能解决)，再执行下列命令
git add .
git commit -m "解决了分支合并冲突的问题"
~~~



### 4.2 远程分支操作

**将本地分支推送到远程仓库**

* 如果是第一次将本地分支推送到远程仓库，需要运行如下的命令:

~~~markdown
# -u表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带-u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例:
git push -u origin payment: pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化:
git push -u origin payment
~~~

* 注意:第一次推送分支需要带-u参数，此后可以直接使用git push 推送代码到远程分支。



**查看远程仓库中所有的分支列表**

* 通过如下的命令，可以查看远程仓库中，所有的分支列表的信息:

~~~markdown
git remote show 远程仓库名称
~~~



**跟踪分支**

* 跟踪分支指的是:从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下:

~~~markdown
# 从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
git checkout 远程分支的名称
# 示例:
git checkout pay

# 从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
git checkout -b 本地分支名称 远程仓库名称/远程分支名称
# 示例:
git checkout -b payment origin/pay

~~~



**拉取远程分支的最新的代码**

* 可以使用如下的命令，把远程分支最新的代码下载到本地对应的分支中:

~~~Markdown
# 从远程仓库，拉取当前分支最新的代码，保持当前分支的代码和远程分支代码一致
git pull
~~~



**删除远程分支**

* 可以使用如下的命令，删除远程仓库中指定的分支:

~~~Markdown
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称

# 示例:
git push origin --delete pay

~~~


