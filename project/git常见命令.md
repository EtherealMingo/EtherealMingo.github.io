### 1.创建仓库

- mkdir git
- cd git  ——创建/home/XXX/git空目录



### 2.通过git init命令把这个目录变成Git可以管理的仓库:

- git init ——初始化Git仓库



### 3.用命令git add告诉Git，把文件添加到仓库(实际上就是把文件修改添加到暂存区)：

- git add ***filename\*** 



### 4.用命令git commit告诉Git，把文件提交到仓库(实际上就是把暂存区的所有内容提交到当前分支)：

- git commit -m "有意义的附加说明"



### 5.随时掌握工作区的状态

- git status



### 6.查看文件被修改的内容

- git diff



### 7.查看代码的历史版本号

- git log

- git log --pretty=oneline  ——要求版本信息只能在一行中显示



### 8.HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭

- git reset --hard commit_id

- 或git reset --hard HEAD^(HEAD^^等等)



### 9.查看命令历史，以便确定要回到未来的哪个版本

- git reflog



### 10.弄明白Git的工作区(当前分区)和暂存区



### 11.理解Git是如何跟踪修改的，每次修改，如果不add到暂存区，那就不会加入到commit中



### 12.撤销修改

命令**git checkout -- filename**意思就是，把filename文件在工作区的修改全部撤销，这里有两种情况：

- 一种是filename自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

- 一种是filename已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令**git checkout -- file**。

***git checkout\*其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。**

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令**git reset HEAD file**，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，版本回退，不过前提是没有推送到远程库。



### 13.删除文件

命令**git rm**用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。



### 14.将本地仓库与github仓库关联起来

往里面添加文件：

1. touch README.md
2. git init
3. git add README.md
4. git commit -m "first commit"
5. git remote add origin git@github.com:sysublackbear/Learmgitfirst.git
6. git push -u origin master

将本地仓库同步github仓库：

1. git remote add origin git@github.com:sysublackbear/Learmgitfirst.git
2. git push -u origin master

然后，从现在起，只要本地作了提交，就可以通过命令：

- git push origin master

把本地master分支的最新修改推送至GitHub



### 15.多人协作一个项目的时候，我们每个人可以通过从远程仓库克隆一份来作为己用。

- git  clone git@github,com:sysublackbear/XXXX.git



### 16.创建分支并且切换到分支

1. git checkout -b dev
2. Switched to a new branch 'dev'

等价于：

1. git branch dev
2. git checkout dev
3. Switched to branch 'dev'

查看分支：

- git branch

将次分支合并到主分支上面：

- git merge dev

删除分支：

1. git branch -d dev
2. Deleted branch dev (was fec145a).



### 17.解决冲突

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

用*git log --graph*命令可以看到分支合并图。



### 18.Bug修复

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场*git stash*一下，然后去修复bug，修复后，再*git stash pop*，回到工作现场



### 19.开发新功能

开发一个新功能，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过**git branch -D name**强行删除。



### 20.参与开源项目先要克隆一份到本地

- git clone git@github.com:michaelliao/bootstrap.git

