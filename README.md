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
2. 用命令`git add` ，把文件添加到仓库
`$ git add readme.txt`
3. 用命令`git commit`，把文件提交到仓库
`git commit -m "wrote a readme file"`     
注：-m后面输入的是本次提交的说明

为什么Git添加文件需要add，commit一共两步的原因：   
因为commit可以一次提交很多文件，所以你可以多次add不同的文件

`git status`   
可以让我们时刻掌握仓库当前的状态

`git diff`    
顾名思义就是查看difference，显示的格式正是Unix通用的diff格式

`git log`==>提交历史   
在Git中，我们用`git log`命令查看历史记录，显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上**--pretty=oneline**参数

`commit id`   
一大串类似3628164...882e1e0的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

##提交历史的时间线
每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线

在Git中，用**HEAD**表示**当前版本**，HEAD指向的版本就是当前版本，上一个版本就是**HEAD^**，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

##回退版本
`git reset`命令可以回退版本。 --hard参数的作用：
`git reset -hard [commit_id]`或者是`HEAD^`等

`git reflog`==>命令历史
Git提供了一个命令`git reflog`用来记录你的每一次命令，

##工作区（Working Directory）
就是你在电脑里能看到的目录


##版本库（Repository）
工作区有一个**隐藏目录.git**，这个不算工作区，而是Git的**版本库**。
Git的版本库里存了很多东西，其中最重要的就是称为**stage（或者叫index）的暂存区**，还有Git为我们自动创建的第一个分支**master**，以及指向master的一个指针叫**HEAD**   
![stages](https://github.com/838860610/LearnGitHub/blob/master/img/git_stage.jpg?raw=true)    

我们**把文件往Git版本库里添加**的时候，是分两步执行的    
1. 用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区    
2. 用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

##查看工作区和版本库里面最新版本的区别
用`git diff HEAD -- readme.txt`命令可以

##丢弃工作区的修改
用`git checkout -- file`丢弃工作区的修改  
`$ git checkout -- readme.txt`   
解释：命令`git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：  
1. 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；   
2. 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。   
总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。  
`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。(可以理解成删除也是修改的特殊一中)

##撤销暂存区的修改
用命令`git reset HEAD file`可以把**暂存区的修改撤销掉（unstage），重新放回工作区**

##远程仓库
本地Git仓库和GitHub仓库之间的传输是通过SSH加密的    
1. 创建SSH Key 在用户主目录下(git bash下的“~”的路径)，看看有没有.ssh目录，如果有，再看看这个目录下
有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，
打开Shell（Windows下打开Git Bash），创建SSH Key：
`$ ssh-keygen -t rsa -C "youremail@example.com"`
然后一路回车，使用默认值即可，无需设置密码
创建好后，可以在用户主目录里找到.ssh目录，里面有**id_rsa**和**id_rsa.pub**两个文件，
这两个就是SSH Key的秘钥对，**id_rsa是私钥**，不能泄露出去，**id_rsa.pub是公钥**，   
2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

##添加远程库   
1. 登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库   
2. 在Repository name填入[项目名字]，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库
注意：可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库

##推送
把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程

##创建与合并分支
**HEAD**严格来说并不是指向提交，而是指向**`maseter`**，**`maseter`**指向**提交**。**HEAD**指向的是**当前分支**。   
1. 当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上。Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！   
2. 我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并。    
3. 合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支。  

`git branch`命令会列出所有分支，当前分支前面会标一个*号。   
`git merge`命令用于合并指定分支到当前分支   
注意到会有`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。
####小结
    查看分支：git branch   
    创建分支：git branch <name>
    切换分支：git checkout <name> 
	git checkout命令加上-b参数表示创建并切换   
    创建+切换分支：git checkout -b <name>   
    合并某分支到当前分支：git merge <name>   
    删除分支：git branch -d <name>

##分支管理策略
通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，**删除分支后，会丢掉分支信息**。
如果要强制禁用`Fast forward`模式，Git就会**在merge时生成一个新的commit**，这样，从分支历史上就可以看出分支信息。   
**`--no-ff`参数，表示禁用`Fast forward`**


##Bug分支
Git还提供了一个**`stash`**功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作   
`git stash list`命令查看stash，存放的工作现场   
恢复的方法
1. `git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除
2. `git stash pop`，恢复的同时把stash内容也删了  
在可以多次stash的情况下，恢复的时候，先用`git stash list`查看，然后恢复指定的stash：   
`$ git stash apply stash@{0}`

##Feature分支
开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过**`git branch -D <name>`**强行删除。

##多人协作
查看远程库信息，用`git remote`  
`git remote -v`显示更详细信息 

##推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上
`$ git push origin master  `    
如果要推送其他分支，比如dev，就改成：
`$ git push origin dev `


##抓取分支
多人协作时，大家都会往`master`和`dev`分支上推送各自的修改。
`git pull`

###小结
从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交  
在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致  
建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name ` 
从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突


##创建标签
1.  切换到需要打标签的分支上
2. `git tag <name>`就可以打标签，默认标签打在最新提交的commit上。
3. 要打以前commit的标签，方法是找到历史提交的commit id `git tag <tag name> <commit id>`    
`git show <tagname>`查看标签信息   
还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

##删除标签
删除本地标签`git tag -d <tagname>`   
推送标签到远程`git push origin <tagname>`或者一次性推送全部尚未推送的本地标签`git push origin --tags`   
删除远程标签
1. 先删除本地标签
2. 从远程删除`git push origin :refs/tags/<tagname>`

##自定义Git
让Git显示颜色，会让命令输出看起来更醒目：
`$ git config --global color.ui true`

##忽略特殊文件
在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件
当然检验.gitignore的标准是`git status`命令是不是说`working directory clean`   
如果你确实想添加该文件，可以用-f强制添加到Git
`$ git add -f App.class`   
需要找出来到底哪个规则写错了，可以用`git check-ignore`命令检查：
`$ git check-ignore -v App.class`Git会显示，哪一行的规则忽略了该文件。





