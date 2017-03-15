title: Git的安装和配置
date: 2014-01-02 09:06:03
tags: git安装,git配置

------
使用Git的第一步肯定是安装Git，因为在多数平台上Git是没有预装的。我平时主要的工作环境是windows和Linux（ubuntu），我想看这篇文章的同学多半也是在这两个平台下工作；下面我讲一下如何在这两个平台下安装和配置Git。BTW：如果是苹果平台的用户的安装可以参看一下这里(1，2)，配置和命令行的使用与windows、Linux（*nix）平台差别不大。
Linux (*nix) 平台

Linus开发Git的最初目的就是为了开发Linux内核服务的，自然它对Linux的平台支持也是最棒的。在Linux下安装Git大约有几种方法：从源代码开始(这种方法也适合于多数*nix平台)从Git官网的下载页面下载它最新稳定版的源代码，就可以从源代码开始编译、安装：
    $ wget http://kernel.org/pub/software/scm/git/git-1.7.3.5.tar.bz2
    $ tar -xjvf git-1.7.3.5.tar.bz2
    $ cd git-1.7.3.5``
    $ make prefix=/usr all ;# prefix设置你的Git安装目录
    $ sudo make prefix=/usr install ;# 以root权限运行
为了编译Git的源代码，我们还需要一些库: expat、curl、 zlib 和 openssl； 除了expat 外，其它的库可能在你的机器上都安装了。使用安装包管理器（apt 或 yum）在 fedora 等系统下用yum ：
    $ yum install git-core
    在debian, ubuntu等系统下用apt ：
    $ apt-get install git-core
有时候，你系统里的安装包管理器出现了问题，或是要安装Git的机器不能上网、没有编译器的话，你可以从下面的站点去下载 “.deb” 或 “.rpm”的安装包：
RPM Packages
Stable Debs
Windows平台

windows平台有两个模拟*nix like运行环境的工具：cygwin，msys；Git在cygwin，msys下都有相应的移植版本。我个人觉得msys平台下的msysGit最好用，现在我在windows下也是用的这个版本。很多同学可能要问，现在windows下有那多Git用户，为什么Git不直接出一个windows native版。俺当年翻看了一下Git的源代码，它里面使用了大量的*nix平台的native api，而这些api在windows下是没有的，所以必须要用cygwin、msys这样的一个中间层来满足软件移植的要求。下面我“啰嗦”一下如何在windows下安装msysGit。
下载

到它的下载页面去下载一个最新的完整安装包，笔者在撰写本文时下载的是这个。
安装

安装的过程没有什么好说的，一般是开始安装后，一路的点击“下一步”。由于windows平台的换行符（CRLF）和Linux(*nix)平台的换行符（LF）不同，那么在windows下开发其它平台软件的朋友有一个地方要注意（见下图)：在这里一最好选“Checkout as-is, commit as-is”这个选项，这样，Git就不会修改你代码的换行符风格。以前有个朋友因为选错了这个选项，以致他在windows平台下的一签出（checkout）其它平台的代码，就会显示”已修改“（modified），不过后来可能msysGit也认识到这个问题了，就把默认选项改成了这个选项。BTW: 其实前面两项也是有用的，如果对windows和Linux(*nix)平台如何处理换行符很熟悉的话，也可以尝试一下前面两个选项：）
配置Git

在Linux下和windows下配置Git的方法差不多，只是在Linux下，可以在命令行里直接使用git config进行配置, 而在windows下则要先打开“Git Bash”，进入msysGit命令行界面，再用git config命令进行相应的配置操作。好了，前面安装好了Git，现在我们开始配置：第一个需要配置的就是用户的用户名和email，因为这些内容会出现在你的每一个提交（commit）里面的，像下面这样：
    $ git log #我们用git log查看当前仓库的提交（commit）日志
    commit 71948005382ff8e02dd8d5e8d2b4834428eece24
    Author: author <author@corpmail.com>
    Date: Thu Jan 20 12:58:05 2011 +0800
    Project init
下面的这两行命令就是设置用户名和email：
    $ git config --global user.name author #将用户名设为author
    $ git config --global user.email author@corpmail.com #将用户邮箱设为author@corpmail.com
Git的配置信息分为全局和项目两种，上面命令中带了“--global"参数，这就意味是在进行全局配置，它会影响本机上的每个一个Git项目。大家看到，上面我们用的是@corpmail（公司邮箱）；但是有时候我们可能也参与了一些开源项目，那么就需要新的用户名和自己的私人邮箱，Git 可以为每个项目设定不同的配置信息。在命令行环境，进入Git项目所在目录，执行下面的命令：
    $ git config　user.name nickname#将用户名设为nickname
    $ git config　user.email nickname@gmail.com #将用户邮箱设为nickname@gmail.com
Git的设计哲学和Linux（*nix）一样，尽量的使用“文本化”（Textuality）；它里面尽量用文本化的形式存储信息，对于配置信息也更是如此，用户的这些配置信息全部是存储在文本文件中。Git的全局配置文件是存放在"~/.gitconfig"（用户目录下的.gitconfig）文件中：我们用cat、head命令查看全局配置信息文件，并假设相关配置信息存储在文件的前3行（当然也有可能不在前3行，这里只是为了方便表示）
    $ cat ~/.gitconfig | head -3
    [user]
    name = author
    email = author@corpmail.com
而项目配置文件是存放在Git项目所在目录的".git/config"文件中，这里也像上面一样用cat、head命令查看一下：
    $ cat .git/config | head -3
    [user]
    name = nickname
    email = nickname@gmail.com
如果大家对于Git熟悉后，可以直修改”~/.gitconfig”,”.git/config”这两个文件进行配置。Git里还有很多可以配置的地方，大家可以参考一下git config 和 定制git。
这一篇写起来有点平淡无奇，但这是一个Git用户迈出的第一步。后面我还会有一系列的文章出来，都是我个人使用过程中的感悟。有朋友问我：“为什么把文章叫作：‘Git历险记’”。这是因为在使用Git的历程中，我碰到过N多的问题；同时也觉得它有点小复杂。但是当这些问题解开后，就有时不得不赞叹它设计的巧妙之处。如果大家对于我的文章有什么问题和建议，欢迎给我写邮件：之前我建立了一个 git中文用户组 ，如果大家在使用Git的过程中碰到什么麻烦事，欢迎你在这个用户组里提问。参考资料：
GitCommunityBook 中文版
ProGit 中文版
git config
