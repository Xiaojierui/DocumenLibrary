# Git基础
----

#### 1.注册GitHub账户 熟悉GitHub和认识Github 
（1）实名注册 Github 账户、点亮个人头像、完善个人资料      
（2）能够在 Github 上搜索资料（你感兴趣的方面，python、java等等）   
（3）搜索大神（阮一峰等等）、搜索项目（例如CRM）   
（4）能够评估人和项目的活跃度（按照贡献度等等）   
（5）Star 收藏项目  Follow 关注高手    

----
#### 2.Git工具使用
&emsp;&emsp;命令行工具 Bash、Cmd、Power Shell等   
&emsp;&emsp;GUI工具Git GUI、Github Desktop等    
&emsp;&emsp;IDE 集成工具Visual Studio、Eclipse、IntelliJ IDE等     
&emsp;&emsp;[Git命令行工具](https://git-scm.com/)的下载，在Git Bash 中运行 git --version 验证安装是否成功，然后设置简单配置颜色和字体    

-----

#### 3.Bash命令初体验 
（1）github git bash 练习   

- pwd  当前路径   
- mkdir  创建文件夹   
- cd  进入 文件夹  
- echo 打印  
- cat  打印文件内容  
- cp  复制   
- ls .. 上级目录  
- mv 移动目录   
- rm 删除    
- clear 清除    

（2）设置git参数 //设置个人信息参数

- git config  --list
- git config  --global user.name "Hansiyuan131"
- git config  --global user.email "422295068@qq.com"

 （3）其他操作

- cd ~  ls 主目录   
- ls -a 隐藏目录     
- vim  .gitconfig   进行编辑  vim编辑器   //要在.gitcofig目录中使用此命令

   


-------

#### 4.git 命令 

![git 简介](https://i.imgur.com/8onAyiv.png)    

&emsp;&emsp;Workspace：工作区   
&emsp;&emsp;Index / Stage：暂存区   
&emsp;&emsp;Repository：仓库区（或本地仓库）    

(1) git bash  命令练习

1.在当前目录下建一个git 代码库

git init

2.下载一个项目和他的代码历史 url 

git clone [url]

3.添加指定文件到暂存区

git add  [file1]  [file2]

4.删除工作区文件，并且将这次删除的文件放在暂存去

git  rm  [file1]  [file2]

5.改名文件，并且将这个名改放入暂存区

 
git  mv  [file-origin]  [file-renamed]

6.提交暂存区到仓库

git  commit  -m  [message]

7.直接提交从工作区到仓库（前提该文件已经有仓库的历史版本）

git commit  -a  -m [message]

8.显示变更信息

git status

9.显示当前分支的历史版本

git log 
git log --oneline

![git remote](https://i.imgur.com/LfL2BwY.png)

(2)同步远程仓库

1.增加远程仓库、并命名 (git remote add origin [url])

git remote add [shortname] [url]

2.将本地的提交推送到远程仓库  (git push origin master)

git push [remote] [branch]

3.将远程仓库提交拉下本地

git pull [remote] [branch]

其他相关操作  git remote -v 查看绑定的仓库

cat 文本    查看文本内容

cd 进入
cd ..进入上一级



(3)git 在线练习

1.try.github.io 按照题目练习

2.闯关git-it

首先安装 nodeJS  npm install  git-it-g  电脑 ->cmd  输入npm install  git-it-g 安装包
  
   
(4)其他命令   

1. 命令行换行

 \  继续编写不用慌

2. 命令行终结 

 Ctrl+c 强制退出

三、命令行的翻页和退出

 git log

下翻页 ：   
上翻页：Ctrl+u    
退出： q或者Ctrl+c   
最上：gg   
最下：G   
搜索：/n   
下一匹配行：u  
上一匹配行：n    
基本上于vim的操作一样    

四、vim操作模式    


vim  readme.md     


编辑模式： i   
回到普通模式：Esc   
保存退出：：wq  
放弃保存并退出 q!    





----















----