---
layout: post

title: Git 常用命令简介
tags: Git  
---

> 下文总结一下git命令

## 基本命令

### 1、<code style="color:red">git init</code> 将当前目录修改为Git可以管理的仓库

### 2、<code style="color:red">git add readme.md</code> 将readme.md文件添加到仓库

### 3、<code style="color:red">git commit -m "wrote a readme file"</code> 告诉Git，把文件提交到仓库，<code style="color:red">-m</code>后面输入的是本次提交的说明.

### 4、<code style="color:red">git log</code>,查看当前仓库的历史记录，也根据查看具体文件，加上文件路径。此外，<code style="color:red">git log</code>还可以加上<code style="color:red">--pretty=oneline</code>参数，两者命令对比结果如图：

![git](/images/git01.jpg)

![git](/images/git02.jpg)

## 版本回退

上面已经提到可以使用<code style="color:red">git log</code> 查看历史记录，图片中黄色的一串代码就表示了commit的版本号

### 1、<code style="color:red">git reset --hard HEAD^</code>,将当期版本回退到上一个版本。 <code style="color:red">HEAD</code>表示当期版本，<code style="color:red">HEAD^</code>表示上一个版本，<code style="color:red">HEAD^^</code>表示上上个版本，依次类推。还可以写成<code style="color:red">HEAD~20</code>表示前20个版本

![git](/images/git03.jpg)

### 2、<code style="color:red">git reset --hard 版本号</code>，改命令后面可以直接跟上commit的版本号，如上已经将版本回退到上一个版本，现在又后悔了想要回到没有回退前。如图，版本号可以不写全，git会自动去查找

![git](/images/git04.jpg)

### 3、<code style="color:red">git reflog</code> 查看使用命令的历史记录


![git](/images/git05.jpg)

### 4、<code style="color:red">git checkout -- readme.txt</code>放弃对工作区的修改，没有<code style="color:red">git add</code>之前

### 5、<code style="color:red">git reset HEAD readme.txt</code>,可以把暂存区的修改撤销掉

### 6、<code style="color:red">git rm 文件</code> 用于删除一个文件。 

## 分支管理

### 1、<code style="color:red">git branch 分支名</code>创建新的分支，可以使用<code style="color:red">git branch</code>查看当前分支

### 2、<code style="color:red">git checkout 分支名</code>修改当前分支，还可以在创建的分支的时候同时修改，使用命令<code style="color:red">git checkout -b 分支名</code>

### 3、<code style="color:red">git merge 分支名</code>将分支合并

### 4、<code style="color:red">git log --graph --pretty=oneline --abbrev-commit</code>查看分支的合并情况

### 5、<code style="color:red">git branch -d 分支名</code>删除分支

### 6、<code style="color:red">git merge --no-ff -m "merge with no-ff" 分支名</code>合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而<code style="color:red">fast forward</code>合并就看不出来曾经做过合并。

### 7、分支策略，<code style="color:red">master</code>分支仅用来发布新版本，平时不在上面干活，平常操作的是其他分支，比如：<code style="color:red">dev</code>,这个分支是不稳定的，需要发布时再把dev分支合并到master上，然后在master分支发布1.0版本。工作都在<code style="color:red">dev</code>分支上，然后每个人有自己的分支，工作做完都向<code style="color:red">dev</code>分支上合并就可以了。团队合作的分支如图：

![git](/images/git06.jpg)

### 8、修改有问题的分支，先对将当前工作现场“储藏”，使用<code style="color:red">git stash</code>命令，然后切换到需要修改的分支，创建临时分支，并在临时分支上修复问题后再合并到问题分支上，接着删除临时分支。最后，切换到之前的工作分支，恢复工作现场使用<code style="color:red">git stash pop</code>恢复的同时删除stash内容，如果单纯恢复使用<code style="color:red">git stash apply</code>，删除使用<code style="color:red">git stash drop</code>，另外使用<code style="color:red">git stash list</code>查看保存的内容

### 9、<code style="color:red">git branch -D 分支名</code>使用该命令强行删除还没有被合并的分支。

## 协作

### 1、<code style="color:red">git remote</code>查看远程库的信息，<code style="color:red">git remote -v</code>显示更详细的信息

### 2、<code style="color:red">git push origin master</code>将本地主分支推送到远程库，如果要推送其他分支，比如：<code style="color:red">dev</code>,改成：<code style="color:red">git push origin dev</code>即可。

### 3、分支推送一般原则是：
 * <code style="color:red">master</code>分支是主分支，因此要时刻与远程同步
 * <code style="color:red">dev</code>分支是开发分支，团队所有成员都需要在上面工作，所以也需要远程同步
 * 其他分支取决于你是否和你的团队成员合作在上面开发


## 标签管理

### 1、<code style="color:red">git tag 标签名</code>新建标签

### 2、<code style="color:red">git tag</code>查看所有标签

### 3、默认标签是打在最新提交的commit上，如果需要指定commit上打标签，可以使用<code style="color:red">git log --pretty=oneline --abbrev-commit</code>查看历史提交的commit id ，然后在执行<code style="color:red">git tag 标签名 commitid</code>

### 4、<code style="color:red">git show 标签名</code>用于查看标签信息

### 5、<code style="color:red">git tag -a 标签名 -m "说明信息" commitid</code>可以使用-m参数为标签指定说明文字

### 6、<code style="color:red">git tag -s 标签名 -m "说明信息" commitid</code>通过-s用私钥签名一个标签

### 7、<code style="color:red">git tag -d 标签名</code>删除标签

### 8、<code style="color:red">git push origin 标签名</code>将标签推送到远程，或者可以使用<code style="color:red">git push origin --tags</code>一次性推送全部尚未推送到远程的本地标签

### 9、删除已经推送到远程仓库的标签，先要将本地标签删除，然后再使用<code style="color:red">git push origin :refs/tags/标签名</code>删除远程仓库的标签

### 10、允许无关的历史

###<code style="color:red">git pull origin master --allow-unrelated-histories</code>

### 11、允许无关的历史

###<code style="color:red">git remote add origin git@XXXXX</code>

### 12、.gitignore规则不生效的解决办法，先把本地缓存删除（改变成未被追踪状态），然后再提交 
###<code style="color:red">git rm -r --cached .</code>
