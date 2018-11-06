## 团队协作
在 GitHub 上展开团队协作，掌握 GitHub 的 Fork 以及 Pull Request 的流程，能够参与到他人的项目中。而且，能够掌握几种常规的 Git 协作方式，能够让自己身边的小伙伴，参与到自己的开源项目中，还可以更好的参与其他伙伴项目。
   
最常用的四种团队协作方式，团队方式我们称为工作流，其中包括集中式工作流、功能分支工作、
Gitflow 工作流、Forking 工作流（github上使用最多的)，本文中的几种工作流是作为方案指导而不是条例规定。在展示了各种工作流可能的用法后，你可以从不同的工作流中挑选或揉合出一个满足你自己需求的工作流。  

先看几个由团队共同完成的项目案例：   
&emsp;&emsp;（1）[how-to-markdown](https://github.com/workshopper/how-to-markdown/graphs/contributors)   
&emsp;&emsp;（2）[gitignore](https://github.com/github/gitignore) 一共997个协作者   
&emsp;&emsp;（3）[阮一峰老师的 jstutorial 项目](https://github.com/ruanyf/jstutorial) 59个协作者    
   
参考资料：  
&emsp;&emsp;（1）[Git 工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)  阿里巴巴大神翻译的一个关于git团队协作的文档，我们可以作为参考学习  其原文链接：[Git Workflows and Tutorials](https://www.atlassian.com/git/tutorials/comparing-workflows)    
&emsp;&emsp;（2）[**Subversion**](https://baike.baidu.com/item/SVN) SVN是Subversion的简称


---
## 1.集中式工作流
如果你的开发团队成员已经很熟悉 **Subversion** ，集中式工作流让你无需去适应一个全新流程就可以体验 **Git** 带来的收益。这个工作流也可以作为向更 **Git** 风格工作流迁移的友好过渡。    

![Git Workflows: SVN-style](https://i.imgur.com/O6M74DV.png) 


转到分布式版本控制系统看起来像个令人生畏的任务，但不改变已用的工作流，你也可以用上 **Git** 带来的收益。团队可以用和  **Subversion**  完全不变的方式来开发项目。但使用 **Git** 加强开发的工作流，相比 **SVN** ， **Git** 有以下两个优势:   

&emsp;&emsp;（1）每个开发者可以有属于自己的整个工程的本地拷贝。隔离的环境让各个开发者的工作和项目的其他部分修改独立开来 ——即自由地提交到自己的本地仓库，先完全忽略上游的开发，直到方便的时候再把修改反馈上去。    

&emsp;&emsp;（2）**Git** 提供了强壮的分支和合并模型。不像 **SVN** ， **Git** 的分支设计成可以做为一种用来在仓库之间集成代码和分享修改的『失败安全』的机制。

### 2.1.1 工作方式

像 **Subversion** 一样，集中式工作流以中央仓库作为项目所有修改的单点实体。相比 **SVN** 缺省的开发分支 **trunk** ，**Git** 叫做 **master** ，所有修改提交到这个分支上。本工作流只用到 **master** 这一个分支。

首先，开发者克隆中央仓库。在自己的项目拷贝中，像 **SVN** 一样的编辑文件和提交修改；但修改是存在本地的，和中央仓库是完全隔离的。开发者可以把和上游的同步延后到一个方便时间点。

然后，开发者发布修改到正式项目中，开发者要把本地 **master** 分支的修改『推』到中央仓库中。这相当于 **svn commit** 操作，但 **push** 操作会把所有还不在中央仓库的本地提交都推上去。

![git-workflow-svn-push-local](https://i.imgur.com/RS1cggp.png)

### 2.1.2 冲突解决

中央仓库代表了正式项目，所以提交历史应该被尊重且是稳定不变的。如果开发者本地的提交历史和中央仓库有分歧，`Git`会拒绝`push`提交否则会覆盖已经在中央库的正式提交。

![git-workflow-svn-managingconflicts](https://i.imgur.com/gpWNqdZ.png)

在开发者提交自己功能修改到中央库前，需要先`fetch`在中央库的新增提交，`rebase`自己提交到中央库提交历史之上。
这样做的意思是在说，『我要把自己的修改加到别人已经完成的修改上。』最终的结果是一个完美的线性历史，就像以前的`SVN`的工作流中一样。

如果本地修改和上游提交有冲突，`Git`会暂停`rebase`过程，给你手动解决冲突的机会。`Git`解决合并冲突，用和生成提交一样的[`git status`](https://www.atlassian.com/git/tutorial/git-basics#!status)和[`git add`](https://www.atlassian.com/git/tutorial/git-basics#!add)命令，很一致方便。还有一点，如果解决冲突时遇到麻烦，`Git`可以很简单中止整个`rebase`操作，重来一次（或者让别人来帮助解决）。

### 2.1.3 示例

让我们一起逐步分解来看看一个常见的小团队如何用这个工作流来协作的。有两个开发者小明和小红，看他们是如何开发自己的功能并提交到中央仓库上的。

#### 有人先初始化好中央仓库

![git-workflow-svn-initialize](https://i.imgur.com/WTVJkHT.png)

第一步，有人在服务器上创建好中央仓库。如果是新项目，你可以初始化一个空仓库；否则你要导入已有的`Git`或`SVN`仓库。

中央仓库应该是个裸仓库（`bare repository`），即没有工作目录（`working directory`）的仓库。可以用下面的命令创建：

```bash
ssh user@host
git init --bare /path/to/repo.git
```

确保写上有效的`user`（`SSH`的用户名），`host`（服务器的域名或IP地址），`/path/to/repo.git`（你想存放仓库的位置）。
注意，为了表示是一个裸仓库，按照约定加上`.git`扩展名到仓库名上。

#### 所有人克隆中央仓库

![人热热 热热](images/git-workflow-svn-clone.png)

下一步，各个开发者创建整个项目的本地拷贝。通过[`git clone`](https://www.atlassian.com/git/tutorial/git-basics#!clone)命令完成：

```bash
git clone ssh://user@host/path/to/repo.git
```

基于你后续会持续和克隆的仓库做交互的假设，克隆仓库时`Git`会自动添加远程别名`origin`指回『父』仓库。

#### 小明开发功能

![git-workflow-svn-1](https://i.imgur.com/82ehyJQ.png)

在小明的本地仓库中，他使用标准的`Git`过程开发功能：编辑、暂存（`Stage`）和提交。
如果你不熟悉暂存区（`Staging Area`），这里说明一下：**暂存区**用来准备一个提交，但可以不用把工作目录中所有的修改内容都包含进来。
这样你可以创建一个高度聚焦的提交，尽管你本地修改很多内容。

```bash
git status # 查看本地仓库的修改状态
git add # 暂存文件
git commit # 提交文件
```

请记住，因为这些命令生成的是本地提交，小明可以按自己需求反复操作多次，而不用担心中央仓库上有了什么操作。
对需要多个更简单更原子分块的大功能，这个做法是很有用的。


#### 小红开发功能


![git-workflow-svn-2](https://i.imgur.com/fvjOQs7.png)

与此同时，小红在自己的本地仓库中用相同的编辑、暂存和提交过程开发功能。和小明一样，她也不关心中央仓库有没有新提交；
当然更不关心小明在他的本地仓库中的操作，因为所有本地仓库都是私有的。

#### 小明发布功能

![git-workflow-svn-3](https://i.imgur.com/YY8QsMp.png)

一旦小明完成了他的功能开发，会发布他的本地提交到中央仓库中，这样其它团队成员可以看到他的修改。他可以用下面的[`git push`命令](https://www.atlassian.com/git/tutorial/remote-repositories#!push)：

```bash
git push origin master
```

注意，`origin`是在小明克隆仓库时`Git`创建的远程中央仓库别名。`master`参数告诉`Git`推送的分支。
由于中央仓库自从小明克隆以来还没有被更新过，所以`push`操作不会有冲突，成功完成。

#### 小红试着发布功能

![git-workflow-svn-4](https://i.imgur.com/E89f5s3.png)

一起来看看在小明发布修改后，小红`push`修改会怎么样？她使用完全一样的`push`命令：

```bash
git push origin master
```

但她的本地历史已经和中央仓库有分岐了，`Git`拒绝操作并给出下面很长的出错消息：

```
error: failed to push some refs to '/path/to/repo.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

这避免了小红覆写正式的提交。她要先`pull`小明的更新到她的本地仓库合并上她的本地修改后，再重试。

#### 小红在小明的提交之上`rebase`

![git-workflow-svn-5](https://i.imgur.com/6ftI9bM.png)


小红用[`git pull`](https://www.atlassian.com/git/tutorial/remote-repositories#!pull)合并上游的修改到自己的仓库中。
这条命令类似`svn update`——拉取所有上游提交命令到小红的本地仓库，并尝试和她的本地修改合并：

```bash
git pull --rebase origin master
```

`--rebase`选项告诉`Git`把小红的提交移到同步了中央仓库修改后的`master`分支的顶部，如下图所示：

![git-workflow-svn-6](https://i.imgur.com/WD914xd.png)


如果你忘加了这个选项，`pull`操作仍然可以完成，但每次`pull`操作要同步中央仓库中别人修改时，提交历史会以一个多余的『合并提交』结尾。
对于集中式工作流，最好是使用`rebase`而不是生成一个合并提交。

#### 小红解决合并冲突

![git-workflow-svn-7](https://i.imgur.com/d57Ncbf.png)

`rebase`操作过程是把本地提交一次一个地迁移到更新了的中央仓库`master`分支之上。
这意味着可能要解决在迁移某个提交时出现的合并冲突，而不是解决包含了所有提交的大型合并时所出现的冲突。
这样的方式让你尽可能保持每个提交的聚焦和项目历史的整洁。反过来，简化了哪里引入`Bug`的分析，如果有必要，回滚修改也可以做到对项目影响最小。

如果小红和小明的功能是不相关的，不大可能在`rebase`过程中有冲突。如果有，`Git`在合并有冲突的提交处暂停`rebase`过程，输出下面的信息并带上相关的指令：

```
CONFLICT (content): Merge conflict in <some-file>
```

![git-workflow-svn-8](https://i.imgur.com/zc0Z9je.png)

`Git`很赞的一点是，任何人可以解决他自己的冲突。在这个例子中，小红可以简单的运行[`git status`](https://www.atlassian.com/git/tutorial/git-basics#!status)命令来查看哪里有问题。
冲突文件列在`Unmerged paths`（未合并路径）一节中：


>  # Unmerged paths:    
>  #(use "git reset HEAD <some-file>..." to unstage)   
>  #(use "git add/rm <some-file>..." as appropriate to mark resolution)   
>  #both modified: <some-file>  


接着小红编辑这些文件。修改完成后，用老套路暂存这些文件，并让[`git rebase`](https://www.atlassian.com/git/tutorial/rewriting-git-history#!rebase)完成剩下的事：

```bash
git add <some-file> 
git rebase --continue
```

要做的就这些了。`Git`会继续一个一个地合并后面的提交，如其它的提交有冲突就重复这个过程。

如果你碰到了冲突，但发现搞不定，不要惊慌。只要执行下面这条命令，就可以回到你执行[`git pull --rebase`](https://www.atlassian.com/git/tutorial/remote-repositories#!pull)命令前的样子：

```bash
git rebase --abort
```

#### 小红成功发布功能

![git-workflow-svn-9](https://i.imgur.com/9MrQMWP.png)

小红完成和中央仓库的同步后，就能成功发布她的修改了：

```bash
git push origin master
```

如你所见，仅使用几个`Git`命令我们就可以模拟出传统`Subversion`开发环境。对于要从`SVN`迁移过来的团队来说这太好了，但没有发挥出`Git`分布式本质的优势。

如果你的团队适应了集中式工作流，但想要更流畅的协作效果，绝对值得探索一下 `功能分支工作流` 的收益。
通过为一个功能分配一个专门的分支，能够做到一个新增功能集成到正式项目之前对新功能进行深入讨论。

---
## 2.功能分支工作流

---
## 3.Gitflow 工作流

---
## 4.Forking 工作流

---
## 5.Pull Request 总结

---