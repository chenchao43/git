## 1.1 GitHub简介
GitHub是为开发者提供Git仓库的托管服务。这是一个让开发者与朋友、同事、同学以及陌生人共享代码的完美场所。
**社会化编程**
GitHub曾经的logo里面就有Social Coding这个概念，任何人都可以比从前更加容易地获得源代码，将其自由更改并加以公开。
在Github各个页面按下shift + /都可以打开键盘快捷键一览表。
**Explore**：最尖端的技术和软件
**Gist**：使用JavaScript编写的Ace编辑器，管理和发布一些没必要保存在仓库中的代码，如比较小的代码片段。
## 2.1 版本管理
**集中型**：以Subversion为代表，将所有数据存放在服务器中，有便于管理的优点，但是，一旦开发者所处的环境不能连接服务器，就无法获得最新的源代码。
**分散型**：以Git为代表，可以拥有多个仓库，开发者不必连接远程仓库就可以开发。
2.2 Git初始设置
**设置姓名和邮箱**
`$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "youremail@example.com"`

这个命令会在“.../User/.gitconfig”中输出设置文件，想要更改信息时，可以直接更改设置文件。
其他初始化操作
`$ git config -global core.editor <editor>  #设置默认文本编辑器
$ git config -global merge.tool <tool>  #设置解决合并冲突时差异分析工具
$ git config --list  #检查已有的配置信息`

创建新版本库
`$ git clone <url>  #克隆远程版本库
$ git init  #初始化本地版本库`

提高命令输出的可读性
`$ git config --global color.ui auto`

## 3.1 GitHub的前期准备

* 创建账户
* 设置头像（通过Gravatar服务器显示）
* 设置SSH Key

https 和 SSH 的区别

1. 前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。
2. https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

<u>在 github 上添加 SSH key 的步骤</u>

* 检查你电脑是否已经有 SSH key ，运行 git Bash 客户端，输入如下代码：

`$ cd ~/.ssh
$ ls`

这两个命令就是检查是否已经存在 id_rsa.pub 或 id_dsa.pub 文件，如果文件已经存在，那么你可以跳过步骤2，直接进入步骤3。

* 创建一个 SSH key

`
$ ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
# Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]
Enter passphrase (empty for no passphrase): 
# Enter same passphrase again:
`

如果结果为
```
Your identification has been saved in /c/Users/you/.ssh/id_rsa.
# Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com

```
SSH key 已经创建成功，你只需要添加到github的SSH key上就可以。

* SSH key 到 github上面去


1. 需要拷贝 id_rsa.pub 文件的内容，你可以用编辑器打开文件复制。
2. 登录你的github，从又上角的设置进入，然后点击菜单栏的 SSH key 进入页面添加 SSH key。
3. 点击 Add SSH key 按钮添加一个 SSH key 。把你复制的 SSH key 代码粘贴到 key 所对应的输入框中，记得 SSH key 代码的前后不要留有空格或者回车。


* 测试SSH Key

在Git Bash中输入
`$ ssh -T git@github.com`

或者
```
$ ssh -T -p 443 git@ssh.github.com
```

有一段警告
```
The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)?
```

输入 yes 回车，如果创建 SSH key 的时候设置了密码，接下来就会提示你输入密码，如：
```
Enter passphrase for key '/c/Users/Administrator/.ssh/id_rsa':
```

当然如果你密码输错了，会再要求你输入，直到对了为止。
注意：输入密码时如果输错一个字就会不正确，使用删除键是无法更正的。
密码正确后你会看到下面这段话，如：
```
Hi username! You've successfully authenticated, but GitHub does not
# provide shell access.
```

**查看分支间的差别**

* https://github.com/rails/rails/compare/4-0-stable...3-2-stable查看4-0和3-2的差别

* https://github.com/rails/rails/compare/master@{7.day.ago}...master查看master分支7天内的差别
* https://github.com/rails/rails/compare/master@{2013-01-01}...master查看master分支与指定日期间的差别

## 4.1 Git基本操作
**git init--初始化仓库**
用 git init 在目录中创建新的 Git 仓库。 你可以在任何时候、任何目录中这么做，完全是本地化的。
在目录中执行 git init，就可以创建一个 Git 仓库了。比如我们创建 runoob 项目：
```
$ mkdir runoob
$ cd runoob
$ git init
Initialized empty Git repository in /Users/tianqixin/www/runoob/.git/
# 在 /runoob/.git/ 目录初始化空 Git 仓库完毕。
```

在Git中我们称这个目录的内容为“附属于该仓库的工作树”，文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。如果需要恢复之前的状态，可以从仓库调取之前的快照。
**git status--查看仓库状态**
git status -s以获得简短的结果输出。
**git add --向暂存区添加文件**
git add . 命令来添加当前项目的所有文件
**git commit 保存仓库的历史记录**
```
$ git commit -m "First commit"
# -m 参数后面的"First commit称作提交信息
$ git commiy -am "Add something"
# 包含了git add 和 git commit
```

如果想要记录更加详细的信息，直接执行“git commit”命令即可，编辑器记录提交信息的格式为：

* 第一行：用一行文字简述提交的更改内容
* 第二行：空行
* 第三行：级数更改原因和详细内容

退出和保存操作参照Vim编辑器基本操作
git commit -a跳过git add 提交缓存的流程
**git log--查看提交日志**
```
$ git log --pretty=short
# 只让程序显示第一行简述信息
$ git log README.md
# 只显示指定文件的信息
$ git log -p
# 查看提交带来的改动
$ git log -p README.md
```
**git diff--查看当前工作树和暂存区的区别**
```
$ git diff HEAD
# 查看工作树与最新提交的区别，可以在git commit之前用
```


尚未缓存的改动：git diff
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动：git diff HEAD
显示摘要而非整个 diff：git diff --stat
## 4.2 推送远程仓库
需要在GitHub上建立与本地仓库一致的远程仓库，创建时不要生成README.md文件。
**git remote add--添加远程仓库**
```
$ git remote add origin git@github.com:WangYixin-Tom/Modern-Signal-Processing.git
```

这项指令可以直接从GitHub上拷贝。
**git push--推送至远程仓库**
```
$ git push -u origin master
```

本地仓库的master分支将会被推送到远程仓库中。
远程仓库也可以创建其他分支。例如分支feature-D，将它以同名形式push至远程仓库。
```
$ git checkout -b feature-D     #本地仓库建立分支
$ git push -u origin feature-D  #推送至远程仓库
```

如果提示： error setting certificate verify locations，需要重新定位整证书的位置，并再次推送。
```
git config --system http.sslcainfo "D:\Program Files\Git\mingw64\ssl\certs\ca-bundle.crt"
```
## 4.3 从远程仓库获取
```
$ git clone git@github.com:github-book/git-tutorrial.git    #注意不要与之前的仓库在同一个目录下
$ git branch -a     #查看分支信息
$ git checkout -b feature-D origin/feature-D        #将远程仓库中分支获取至本地仓库
$ git diff  #修改之后，查看修改
$ git commit -am "Add feature-D"
$ git push
```

如果需要获得最新的远程仓库分支
```
$ git pull origin feature-D
```

如果两人同时修改了同一部分的源代码，push时就很容易发生冲突。所以多名开发者在同一个分支作业时，建议频繁进行push和pull操作。
## 4.4 分支
不同的分支中，可以同时进行完全不同的作业，等该分支的作业完成之后再与master分支合并，可以实现多人高效地并行开发。

* git branch ：显示所有分支
* git checkout -b feature-A ：创建名为feature-A的分支
* git branch feature-A
* git checkout feature-A：和上面指令相同效果 
* git checkout -：切换至上一分支
* git merge --no-ff feature-A：合并分支
* git log--graph：以图表查看分支

## 4.5 更改操作

* git reset --hard 目标时间点哈希值：回溯到指定时间点，哈希值只要输入4位以上就可以执行。
* git reset HEAD:用于取消已缓存的内容。
* git reflog：查看当前仓库执行过的操作日记

merge分支的时候，可能会有冲突，这个时候需要手动查看冲突部分，在编辑器中修改成我们希望得到的样子。然后重新执行add和commit 命令。

* git commit amend：修改提交信息

在合并特性分支之前，如果发现已经提交的内容中有拼写错误等，可以提交一个修改，将修改压缩到一个历史记录中。

* git rebase -i HEAD~2

## 5.1 Pull Request

定义：自己修改源代码之后，请求对方仓库采纳该修改时采取的一种行为。在网络上也常常被简称为PR。
**Pull Request一般流程**

1. Fork源代码管理者的远程仓库，建立自己的远程仓库
2. pull需要修改的特性分支到自己本地仓库
3. 新建需要修改的特性分支，并做相应修改
4. push到自己的远程仓库
5. 发送PullRequest

clone
```
$ git clone git@github.com:hirocastest/first-pr.git
$ cd first-pr
```
**branch**
```
$ git branch -a #查看clone出的仓库分支
$ git checkout -b work gh-pages #创建work分支并自动切换
$ git branch -a #确认切换work分支
$ ls    #查看文件列表，并对相应文件做修改
```

**提交修改**
```
$ git diff  #查看修改是否正确进行
$ git add index.html 
$ git commit -m "Add my impression"
$ git push origin work #创建远程分支
$ git branch -a #查看远程分支
```
为了防止开发到一半的Pull Request被误合并，可以在标题前面加上[WIP]表示Work In Process。完成之后再去掉这个标记。
如果用户对该仓库拥有编辑权限，则可以直接创建分支，从分支发送Pull Request。可以免去Fork的麻烦。
## 6.1 仓库的维护
可以将原仓库设置为远程仓库，从该仓库fetch数据并与本地仓库进行合并，让本地仓库保持最新的状态。

* Fork与clone

```
$ git clone git@github.com:hirocastest/Spoon-Knife.git
$ cd Spoon-Knife
```


* 原仓库设置名称

```
$ git remote add upstream git://github.com/octocat/Spoon-knife.git #upstream作为原仓库的表示符
```


* 获取最新数据

```
$ git fetch upstream        #获取最新源代码
$ git merge upstream/master #合并
```

以后只要重复这一步骤即可。
## 6.2 Pull Request的接收
首先可以通过代码审查，进行评论和比较。
其次，可以在本地开发环境中反映Pull Request的内容变化

* 将接收方的本地仓库更新至最新状态

```
$ git clone git@github.com:ituring/first-pr.git
$ cd first-pr
```


* 获取发送方的远程仓库

```
$ git remote add PR发送者 git@github.com:PR发送者/first-pr.git
$ git fetch PR发送者
```


* 创建用于检查的分支

```
$ git checkout -b pr1
```


* 合并

```
$ git merge PR发送者/work
```

实际开发之中需要检查软件是否能正常运行

* 删除分支

```
$ git branch -D pr1
```

删除没有用的pr1分支
GitHub上点击Merge Pull Request自动合并至仓库或者利用CLI进行合并操作再push至GitHub

* 合并到主分支

```
$ git checkout gh-pages     # 切换至 gh-pages 分支
$ git merge PR发送者/work  #合并分支
$ git diff origin/gh-pages #查看两者区别，确认
# git push
```

用这种方法处理之后仓库的PR自动从open状态切换到close状态。
## 7.1 GitHub Flow的流程

* 令master分支时常保持可以部署的状态
* 可以进行新的作业时要从master分支创建新分支，新分支名称要具有描述性
* 在新建的本地仓库分支中进行提交
* 在GitHub端仓库创建同名分支，定期push
* 需要帮助或者反馈时，发送Pull Request
* 让其他开发者进行审查，确认作业后与master分支合并 

查看GitHub的分支列表页面（https://github.com/用户名/仓库名/branches）还可以轻松掌握各分支与master分支的差别。
# 附录
## Vim 编辑器基本操作
按下Esc; 进入命令模式，然后输入


* :q 离开 (short for :quit)
* 
* :q! 离开，不保存(short for :quit!)
* 
* :wq 保存并离开
* 
* :wq! 保存并离开，即使只有读取的权限。
* 
* :x 保存并离开(shorter than :wq)
* 
* :qa 离开全部 (short for :quitall)

或者可以按下(Esc Shift+Z Shift+Z)以写入/保存，同时离开。
Vim有帮助，只需要按下，输入，
Vim has extensive help, so type Esc:helpReturn and you will have all your answers and even a neat tutorial.
## Git资料

* Pro Git
* Learn Git Branching
* try Git

## Git托管的软件

* GitBucket
* GitLab
* Gitorious
* RhodeCode

**Git常用命令**
master : 默认开发分支； origin : 默认远程版本库
初始化操作
```
$ git config -global user.name <name>  #设置提交者名字
$ git config -global user.email <email>  #设置提交者邮箱
$ git config -global core.editor <editor>  #设置默认文本编辑器
$ git config -global merge.tool <tool>  #设置解决合并冲突时差异分析工具
$ git config -list  #检查已有的配置信息
```

创建新版本库
```
$ git clone <url>  #克隆远程版本库
$ git init  #初始化本地版本库
```

修改和提交
```
$ git add .  #添加所有改动过的文件
$ git add <file>  #添加指定的文件
$ git mv <old> <new> #文件重命名
$ git rm <file>  #从缓存区和硬盘中删除文件
$ git rm -cached <file>  #缓存区删除但硬盘不删除
$ git commit -m <file> #提交指定文件
$ git commit -m “commit message”  #提交所有更新过的文件
$ git commit -amend  #修改最后一次提交
$ git commit -C HEAD -a -amend  #增补提交（不会产生新的提交历史纪录）
```

查看提交历史
```
$ git log  #查看提交历史
$ git log -p <file>  #查看指定文件的提交历史
$ git blame <file>  #以列表方式查看指定文件
```
的提交历史
```
$ gitk  #查看当前分支历史纪录
$ gitk <branch> #查看某分支历史纪录
$ gitk --all  #查看所有分支历史纪录
$ git branch -v  #每个分支最后的提交
$ git status  #查看当前状态
$ git diff  #查看变更内容
```

撤消操作
```
$ git reset -hard HEAD  #撤消工作目录中所有未提交文件的修改内容
$ git checkout HEAD <file1> <file2>  #撤消指定的未提交文件的修改内容
$ git checkout HEAD. #撤消所有文件
$ git revert <commit>  #撤消指定的提交

```
分支与标签
```
$ git branch  #显示所有本地分支
$ git checkout <branch/tagname>  #切换到指定分支或标签
```
```
$ git branch <new-branch>  #创建新分支
$ git branch -d <branch>  #删除本地分支
$ git tag  #列出所有本地标签
$ git tag <tagname>  #基于最新提交创建标签
$ git tag -d <tagname>  #删除标签
```

合并与衍合
```
$ git merge <branch>  #合并指定分支到当前分支
$ git rebase <branch>  #衍合指定分支到当前分支
```

**远程操作**
```
$ git remote -v  #查看远程版本库信息
$ git remote show <remote>  #查看指定远程版本库信息
$ git remote add <remote> <url>  #添加远程版本库
$ git fetch <remote>  #从远程库获取代码
$ git pull <remote> <branch>  #下载代码及快速合并
$ git push <remote> <branch>  #上传代码及快速合并
$ git push <remote> : <branch>/<tagname>  #删除远程分支或标签
$ git push -tags  #上传所有标签
```
