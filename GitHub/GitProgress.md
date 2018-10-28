# Git进阶
参考知识：   
（1）阮一峰老师的 [Git 命令列表](https://github.com/ruanyf/articles/blob/ed02bdef4a2b61d6a1fbdf56e3fbcffcbac5e68a/dev/git/commands.md)   
（2）编写语言[Markdown](https://www.appinn.com/markdown/)  
（3）各语言ignore参考[gitignore](https://github.com/Hansiyuan131/gitignore)
---
## 一、GIT 图形界面工具
### 1.Git GUI工具基本用法
### 2.SourceTree基本用法
### 3.EGit基本用法 
---
## 二、Git配置

### 1.gitignore和换行符
（1） .gitignore忽略某个文件的状态  

>vim .gitIgnore进入vim编辑状态   
>输入要忽略的文件  通配符 （* ？）    
>通常写注释注明  以#开头     

（2）.gitignore使用场合：   
- <1>忽略操作系统自动生成的文件，比如：缩略图，等；    
- <2>忽略编译生成的中间文件、可执行文件等，比如： C 语言编译产生的 .obj 文件和 .exe 文件；  
- <3>忽略你自己的带有敏感信息的配置文件，比如：存放口令的配置文件；   
- <4>tmp/ 临时目录；   
- <5>log/ 日志目录；   
- <6>等等。   

(3)强制添加 .gitignore 忽略的文件   

       git add –f <file name>    

查看 .gitignore 策略生效行号  

       git check-ignore –v <file name>   

(4)消除换行符警告  
>CR: carriage return 回车，光标到首行， ‘\r’ = return  
>LF: line feed 换行，光标下移一行，’\n’ = newline   
>linux: 换行 \n   
>windows: 换行 \r\n   
>MAC OS: 换行 \r   

- <1>提交时转换为LF，检出时转换为CRLF，默认设置不用修改，Git 是 linux 配置   
   - git config –-global core.autocrlf true   
- <2>允许提交包含混合换行符的文件   
   - git config –-global core.safecrlf false    


### 2.别名和缓存凭证
（1） git bash查看日志  

> git  log  
>git  log --oneline      

（2） git 图形化查看日志
>git log  --pretty=format:'%h %ad | %s%d  [%an]'  --graph  --date=short

(3) 别名的使用   
&nbsp;&nbsp;我们可以看到git 图形化查看日志命令很长 所以我们可以使用别名来进行我们想要的操作。alias(别名)   
 &nbsp;&nbsp;例如：我们现在用hi(History历史的前两个字母代替用git图形化查看日志的命令)
>git config --global  alias.hi  --pretty=format:'%h %ad | %s%d  [%an]'  --graph  --date=short    

&nbsp;&nbsp;下面在Vim中更改 比较方便  步骤如下    
- <1>&nbsp;&nbsp;cd ~   进入下一级目录        
- <2>&nbsp;&nbsp;ls -l -a  查看列表  我们看到一个.gitconfig的文件    
- <3>&nbsp;&nbsp;vim  .gitconfig  进入编辑      
- <4>&nbsp;&nbsp; 退出编辑
（如果是输出状态，首先按Esc键退出输入状态，然后按Shift+“;”，再输入q!或wq!（不保存改动，wq!是保存文件的写入修改）退出。）   
- <5>&nbsp;&nbsp;cd -  返回上一级目录 抓紧去感受一下    

&nbsp;&nbsp;记录一下我对其他命令的更改项      
>ci = commit  
>ad = add .  
>br = branch   
>hi = log  --pretty=format:'%h %ad | %s%d  [%an]'  --graph  --date=short   
>st = status  

（4）缓存凭证的使用
&nbsp;&nbsp;每次我们在提交的时候  git总是会提醒我们输入密码  
&nbsp;&nbsp;解决办法 若在http协议下
> git config –-global credential.helper wincred

----
## 三、Git协议
传输文件速度慢和每次提交时需要输入密码
### 1.本地协议（放服务器上比较麻烦 配置相对复杂）

（1）克隆本地仓库    

- git clone /c/wd/Github.git   

- .git(可省)
- git remote -v 

（2）克隆本地仓库，不建议使用 file://    
- git clone file:///c/wd/Github.git

（3）添加远程仓库的链接   
- git remote add origin /c/wd/Github.git

### 2.Git协议（要么完全权限要么没有权限）访问速度最快 一般跟其他权限共同使用  端口问题

（1）克隆远程仓库   
- git clone git://server_ip/Github.git

（2）添加远程仓库的链接   
- git remote add origin git://server_ip/Github.git

### 3.HTTP协议/HTTPS协议（80端口/443端口）简单有效  新手容易上手  防火墙开放端口  传输效率低  

（1）克隆远程仓库   
- git clone https://github.com/Hansiyaun131/Github.git

（2）添加远程仓库的链接   
- git remote add origin https://github.com/Hansiyaun131/Github.git

### 4.SSH协议 公钥、私钥（在企业服务器上容易搭建  对数据压缩最大  速度快  防火墙可能会屏蔽SSH端口）

（1）克隆远程仓库，一般写成简短的命令   
- git clone ssh://git@github.com/Hansiyaun131/Github.git（完整写法）   
- git clone git@github.com:Hansiyaun131/Github.git（简写）    

（2）添加远程仓库的链接
- git remote add origin git@github.com:Hansiyaun131/Github.git

（3）生成 RSA 密钥对 :  
- <1>ssh-Keygen -t rsa -C "422295068@qq.com"（之后操作回车即可）
 
在 Github 网站添加公钥:    
- <1>生成密钥对后  进入SSH文件夹（cd ~  cd  .ssh ）    
- <2>然后查看公钥文件 cat  id_rsa.pub复制其中信息   
- <3>在Setting中SSH and GPG keys 中实则SSH keys   
- <4>new  一个设置题目  复制公钥  结束

使用 SSH 协议，克隆仓库或者添加远程链接:
- <1>git clone git@github.com:Hansiyaun131/(你的项目名)
- <2>第一次使用需要  yes

（5）查看当前协议
- git remote -v


---
##  四、Git基本操作
### 1.几个Git新命令
（1）git 命令信息：
- git  

（2）查看全部 git 子命令： 
- git help -a  

（3）逐行查看文件的修改历史：
- git blame <GitProgress.md> 

（4）从第 100 行开始，到 110 行。逐行查看文件的修改历史：
- git blame –L 100,110 <GitProgress.md>  

（5）列出打算清除的档案：
- git clean -n   

（6）真正的删除：
- git clean –f

（7）连 .gitignore 中忽略的档案也清除：
- git clean -x    

### 2.Git add深入讲解
（1）文件提交：  
- git add .   

（2）一个文件多个提交：
- git add –p

### 3.Git commit深入讲解
（1）add & commit mothed 1：   
- git add .    
- git commit –m “message”      

（2）add & commit mothed 2：
- git commit –a –m “message”    

（3）add & commit mothed 3：
- git commit –am “message”     

（4）每个提交要保证适当的颗粒度、相关性和独立性。
- 以一个小功能、小改进或一个 bug fix 为单位  
- 对应的 unit test 程序在同一个 commit  
- 无相关的修改不在同一个 commit  
- 语法错误的半成品程序不能 commit    

（5）使用Angular提交规范

参考文档：[阮一峰老师的博客](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html
)
### 4.查看信息深入讲解
（1）short and branch
- git status -sb

（2）查看某个提交信息
- git show HEAD
- git show HEAD~2
- git show HEAD^

（3）查看提交历史
- git log <file name>//某文件历史查看
- git log --grep  <msg>//筛选需要查看的历史
- git log -n  //n为需要查看的条数
- git diff  //工作区与暂存区的差异
- git diff --cached  //暂存区与版本的差异
- git diff --HEAD  //工作区与版本差异

### 5.回撤操作深入讲解

（1）回撤暂存区内容到工作目录
- git reset HEAD

（2）回撤提交到暂存区
- git reset HEAD^ --soft

（3）回撤提交，放弃变更
- git reset HEAD（某版本哈希值） –-hard  //回撤到某版本

（4）回撤远程仓库，-f  即 --force
- git push -f

（5）回撤上一次提交
- git add .
- git commit --amend –m “message” //并提交本次

（6）变基操作，改写历史提交
- git rebase –i HEAD~3

---
##  五、标签操作
### 1.git tag标签操作

（1）在当前提交上，打标签 v0.0
- git tag v0.0 

（2）在当前提交上，打标签 v0.0，并给 message 信息注释
- git tag v0.0 –m “message”

（3）在当前提交之前的第 4 个版本上，打标签 v0.0
- git tag v0.0 HEAD~4

（4）列出所有标签
- git tag

（5）删除本地标签
- git tag –d v0.0

（6）把所有标签推送到远程仓库
- git push origin --tags

（7）把某个标签推送到远程仓库
- git push origin v0.0

（8）删除远程标签
- git push origi:refs/tags/v0.0


---
##  六、Git分支操作
### 1.分支简介
### 2.实例演示分支操作
### 3.冲突解决
【要点】：     
（1）在不同分支上，修改同一个文件；   
（2）不同的人，修改了同一个文件；   
（3）不同的仓库，修改了同一个文件；   
（4）冲突只在合并分支的时候才会发生；    
（5）发生冲突并不可怕，冲突的代码不会丢失；   
（6）解决冲突，重新提交，commit 时不要给 message；    
（7）冲突信息的格式；    

### 4.分支命令
（1）创建分支 foo
- git branch foo   
    
（2）切换到分支 foo
- git checkout foo

（3）创建分支并同时切换到 foo，一步做到
- git checkout -b foo

（4）修改分支名字
- git branch –m old_name new_name
- git branch –M old_name new_name   
    
（5）删除分支 foo
- git branch -d foo  //提示
- Git branch –D foo   //强制

（6）列出远程分支
- git branch -r

（7）列出本地分支版本
- git branch -v

（8）查看已合并的分支
- git branch --merged
- git branch --no-merged
    
（9）列出远程合并的分支
- git branch -r --merged

（10）取出远程 foo 分支
- git checkout –t origin/foo

（11）删除远程分支
- git push origin <space>:<remote branch>
- git fetch -p
    
（12）合并分支
- git merge <branch name>

（13）合并分支，拒绝 fast forward，产生合并 commit
- git merge –-no-ff

（14）保存进度
- git stash
    
（15）弹出进度
- git stash pop

（16）查看 stash 列表
- git stash list

（17）删除 stash 列表
- git stash clear

---
