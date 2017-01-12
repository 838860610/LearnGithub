# LearnGitHub
#Records for learning Git
Git 是一款免费、开源的分布式版本控制系统。     
GitHub 上面说了，主要提供基于 git 的版本托管服务。也就是说现在 GitHub 上托管的所有项目代码都是基于 Git 来进行版本控制的，
所以 Git 只是 GitHub 上用来管理项目的一个工具而已。

##Repository:
仓库的意思，即你的项目，你想在 GitHub 上开源一个项目，那就必须要新建一个 Repository ，如果你开源的项目多了，你就拥有了多个 Repositories 。

##Issue:
问题的意思，举个例子，就是你开源了一个项目，别人发现你的项目中有bug，或者哪些地方做的不够好，他就可以给你提个 Issue ，即问题，提的问题多了，也就是 Issues ，然后你看到了这些问题就可以去逐个修复，修复ok了就可以一个个的 Close 掉。

##Star:
给项目点赞。

##Fork:
授权拷贝

##Pull Request:
发起请求，这个其实是基于 Fork 的，还是上面那个例子，如果别人在你基础上做了改进，后来觉得改进的很不错，应该要把这些改进让更多的人收益，于是就想把自己的改进合并到原有项目里，这个时候他就可以发起一个 Pull Request（简称PR） ，原有项目创建人，也就是你，就可以收到这个请求，这个时候你会仔细review他的代码，并且测试觉得OK了，就会接受他的PR，这个时候他做的改进原有项目就会拥有了。

##Gist:
有些时候你没有项目可以开源，只是单纯的想分享一些代码片段，那这个时候 Gist 就派上用场了！

##Watch:
观察，如果你 Watch 了某个项目，那么以后只要这个项目有任何更新，你都会第一时间收到关于这个项目的通知提醒。    

##初始配置：
`$ git config --global user.name "Your Name"`    
`$ git config --global user.email "email@example.com"`    
git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

##创建版本库：
1. 选择一个合适的地方，创建一个空目录（如果已经有，直接进到该目录）
2. 进到该目录，通过git init命令把这个目录变成Git可以管理的仓库

##把文件添加到版本库：
1. 编写一个readme.txt文件（一定要放到版本库目录下，子目录也行，不然git找不到）
2. 用命令git add ，把文件添加到仓库
`$ git add readme.txt`
3. 用命令git commit，把文件提交到仓库
`git commit -m "wrote a readme file"`     
注：-m后面输入的是本次提交的说明

为什么Git添加文件需要add，commit一共两步的原因：   
因为commit可以一次提交很多文件，所以你可以多次add不同的文件

`git status`   
可以让我们时刻掌握仓库当前的状态

`git diff`    
顾名思义就是查看difference，显示的格式正是Unix通用的diff格式

`git log`==>提交历史   
在Git中，我们用git log命令查看历史记录，显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数

`commit id`   
一大串类似3628164...882e1e0的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

提交历史的时间线
每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线

在Git中，用HEAD表示当前版本，HEAD指向的版本就是当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

##回退版本
git reset命令可以回退版本。 --hard参数的作用：
git reset -hard [commit_id]或者是HEAD^等

git reflog==>命令历史
Git提供了一个命令git reflog用来记录你的每一次命令，

工作区（Working Directory）
就是你在电脑里能看到的目录


版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD

我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别


git checkout -- file可以丢弃工作区的修改：
$ git checkout -- readme.txt
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。
git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。(可以理解成删除也是修改的特殊一中)

用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区

远程仓库
本地Git仓库和GitHub仓库之间的传输是通过SSH加密的
1.创建SSH Key 在用户主目录下(git bash下的“~”的路径)，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
$ ssh-keygen -t rsa -C "youremail@example.com"
然后一路回车，使用默认值即可，无需设置密码
创建好后，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，
2.登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

添加远程库
1.，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库
2.在Repository name填入[项目名字]，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库
可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库

把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程
