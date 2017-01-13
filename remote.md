#Git 远程操作详解
###- `git clone`
###- `git remote`
###- `git fetch`
###- `git pull`
###- `git push`  
图  

##一、git clone
#####远程操作的第一步通常是从远程主机(Github)克隆一个版本库，这时候就要用到`git clone`命令。  
`git clone  <url>`  

#####该命令会在本地主机生成一个目录，与远程主机的版本库同名，如果要指定不同的目录名，将目录名作为`git clone`命令的第二个参数
`git clone <url> <local name>`  

#####git clone支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子:

`$ git clone http[s]://example.com/path/to/repo.git/`  
`$ git clone ssh://example.com/path/to/repo.git/`  
`$ git clone git://example.com/path/to/repo.git/`  
`$ git clone /opt/git/project.git`   
`$ git clone file:///opt/git/project.git`  
`$ git clone ftp[s]://example.com/path/to/repo.git/`  
`$ git clone rsync://example.com/path/to/repo.git/`

##二、git remote
#####`git remote` 命令用于管理主机名  
#####不带选项的时候，`git remote`命令列出所有远程主机。  
`$ git remote`  
`origin`  
#####使用-v选项，可以参看远程主机的网址
#####克隆版本库的时候，所使用的远程主机自动被Git命名为origin。如果想用其他的主机名，需要用git clone命令的-o选项指定。
#####`git remote show`命令加上主机名，可以查看该主机的详细信息。
#####`git remote add`命令用于添加远程主机。
#####`git remote rm`命令用于删除远程主机。
#####`git remote rename <old> <new>`命令用于远程主机的改名。

##三、git fetch
#####一旦远程主机的版本库有了更新，需要将这些更新取回本地，需要用到`git fetch`命令
`$ git fetch <remote name>`
#####上面命令将某个远程主机的更新，全部取回本地。
#####git fetch命令通常用来查看其他人的进程，因为它取回的代码对你本地的开发代码没有影响。
#####默认情况下，git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。
#####举例：取回origin主机的master分支。
`$ git fetch origin master`
#####`git branch`命令的-r选项，可以用来查看远程分支，-a选项查看所有分支。

	$ git branch -r
	origin/master

	$ git branch -a
    master
    remotes/origin/master  
#####上面命令表示，本地主机的当前分支是master，远程分支是origin/master。
#####取回远程主机的更新以后，可以在它的基础上，使用git checkout命令创建一个新的分支。   
`$ git checkout -b newBrach origin/master`  
#####上面命令表示，在origin/master的基础上，创建一个新分支。  
#####此外，也可以使用git merge命令或者git rebase命令，在本地分支上合并远程分支。   
	$ git merge origin/master  
	#或者
	$ git rebase origin/master  
#####上面命令表示在当前分支上，合并origin/master。


##四、git pull
#####git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。
#####比如，取回origin主机的next分支，与本地的master分支合并，需要写成下面这样。
`$ git pull origin next:master`  
#####如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
`$ git pull origin next`
#####上面命令表示，取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge。
	$ git fetch origin
    $ git merge origin/next
#####在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系（tracking）。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动"追踪"origin/master分支。
#####Git也允许手动建立追踪关系。

`git branch --set-upstream master origin/next`
#####上面命令指定master分支追踪origin/next分支。
#####如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。

`$ git pull origin`
#####上面命令表示，本地的当前分支自动与对应的origin主机"追踪分支"（remote-tracking branch）进行合并。
#####如果当前分支只有一个追踪分支，连远程主机名都可以省略。

`$ git pull`
#####上面命令表示，当前分支自动与唯一一个追踪分支进行合并。

##五、git push
#####`git push`命令用于将本地分支的更新，推送到远程主机。它的格式与`git pull`命令相仿。
`$ git push <remote> <local branch>:<remote branch>`
#####注意，分支推送顺序的写法是<来源地>:<目的地>，所以git pull是<远程分支>:<本地分支>，而git push是<本地分支>:<远程分支>。
#####如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
`$ git push origin master`
#####上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。
#####如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。
	$ git push origin :master
	# 等同于
	$ git push origin --delete master
#####上面命令表示删除origin主机的master分支。
#####如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。
`$ git push origin`
#####上面命令表示，将当前分支推送到origin主机的对应分支。
#####如果当前分支只有一个追踪分支那么主机名都可以省略。
`$ git push`
