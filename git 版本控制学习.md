# git 版本控制学习

## 1.git基础命令

```bash
# 查看git软件版本
git --version

# 设置git用户名及邮箱
git config --global user.name "用户名"
git config --global user.email "xx@qq.com"

# 查看配置信息
git config -l
```



## 2.新建仓库

```bash
# 新建操作，需要在文件夹目录下操作
git init

>>>> Initialized empty Git repository in F:/GolangProjects/src/awesomeProject/.git/


# 在awesomeProject文件夹下，除了.git目录，所有的目录都称之为工作区

```

# 3.查看当前仓库的状态

```bash
# 查看当前仓库的状态
git status

>>>> No commits yet  //在当前仓库中，没有做过任何的提交
Untracked files:  // 未跟踪的文件
	1.xxx
	2.xxx
```

# 4.工作区文件全部放置到 暂存区中

```bash
# 工作区文件全部放置到 暂存区中
git add .    // . 是所有文件

# add 后的文件，不会再显示 未跟踪  状态
# 文件前面是 new file
```



# 5.提交暂存区中的文件到分支版本中

```bash
# 提交暂存区文件至分支版本
git commit -m "add Golang Leaning Porject"

# message // 每次提交都要留下一条描述信息，必填

>>>  23 files changed, 780 insertions(+)
 // 显示提交的文件数量
 

git status 
# 执行之后，我们就看不到其他的信息了

// On branch master
// nothing to commit, working tree clean
```

# 6.关联远程仓库地址

```bash
# 关联远程仓库，这样git才知道把代码传到那个仓库里

git remote add origin https://github.com/laoliudada/Go-Learning-Project.git

# origin  地址名，随便起的


# 查看关联后的地址
git remote -v

push  上传代码到远程仓库
clone 
pull 从远程仓库下载代码
```

# 7. 把本地仓库代码上传到远程仓库

```bash
# 提交本地仓库代码到远程
git push -u origin master

# master  分支名
# main  好像是github 最近变化的


# 新建main分支   (目前该内容还没有学习到)
git branch -M main
git push -u origin main
```



# 8.克隆远程仓库

```bash
# 克隆私有项目时，会提示输入该仓库的帐号和密码

git clone https://github.com/laoliudada/Go-Learning-Project.git
```



# 9.协作开发

```bash
# 在一个人修改代码，进行git push origin master后
# 远程仓库的代码更新了，第二个人本地仓库的代码还是旧版本

# 在项目目录下执行，需要输入帐号和密码，如果在下载仓库是私有的，已经输入过的，就不需要再次输入了。

git pull origin master
```



# 10.分支

```bash
# 查看当前仓库的分支
git branch

>>> master   只有一个分支
// 执行git commit 默认是在master分支上保存版本


# 创建新分区  dev
git branch dev

>>> dev
	* master   // * 当前使用的分支
		
		
# 切换分支
git checkout dev

>>> * dev
  	master
  	
  # 切换分支后，add 文件，commit 创建分支
  # 再切换回原来的master 分支后，增加的文件会消失
  # 再切换回dev又会出现，所有master和dev分支是两个独立分割开的
```



# 11.指针

```bash
# 指针始终指向当前分支的最新版本
# 新的分支（dev）被创建后，和当前分支（master）有着相同的内容
```

# 12.分支日志

```bash
# 该日志命令只会显示当前分支的日志（dev）
git log --oneline 


$ git log --oneline
8b20318 (HEAD -> dev, origin/dev) add c.txt in dev br
221a276 (origin/master, master) Create README.md
2bb9d06 add /a/a.pptx
1dd28a4 add z.txt b.doc
54448d7 add a.xls


# 查看完整的log提交日志
git log
```



# 13.分支合并（快速）

```bash
# 一般在master分支合并dev的分支,所以先用git checkout master切换分支

git checkout master
git merge dev   // 合并dev分支

>>>
Updating 221a276..8b20318
Fast-forward    //快速合并
 c.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c.txt


# 触发快速合并的情况
1. master 没有动，只修好过dev分区

```

# 14.分支合并（三方）

```bash
# 三方：共同的起点，master的终点，dev的终点
git merge dev

# 查看日志（图形）
git log --oneline --graph

# 所谓三方合并跟快速合并的区别是：在满足快速合并条件下，master有提交了一次文件。
```

# 15.分支合并冲突问题

```bash
# 合并分支时，可能会出现分支合并冲突（三方合并的时候）
# 原因：master里的一个文件，A把文件改为111，而B把文件改为222，合并时会产生冲突


$ git merge dev
CONFLICT (add/add): Merge conflict in bb.txt
Auto-merging bb.txt  // 出现冲突
Automatic merge failed; fix conflicts and then commit the result.  // 建议修复后再提交

# 打开bb.txt 发现内容

<<<<<<< HEAD   // 当前分支内容
321
=======
123
>>>>>>> dev   //dev分支内容

# 通过协商后选择需要保留的那部分代码，不需要的就删除

321


# 修改之后
git add .
git commit -m "fix conflict in master"
>>>
[master e5fb57b] fix conflict in master

```

# 16.忽略文件



在目录的根文件下创建  '.gitignore'

```bash
.idea
*.md
nodejs //文件夹
```



# 17. 恢复之前的仓库版本

```bash
# 退回之前版本
git log   //找到退回版本的版本号
git reset --hard b42593ee1e7d64c040f6caaf08da24bf63e692fb   //一般是不需要填这么长的

git commit -m "xxx"
git push -f  //强行推送，-f，一般推送会报错，因为版本比指针版本库要旧
```

# 18.反做

>  git revert是用于“反做”某一个版本，以达到撤销该版本的修改的目的。比如，我们commit了三个版本（版本一、版本二、 版本三），突然发现版本二不行（如：有bug），想要撤销版本二，但又不想影响撤销版本三的提交，就可以用 git revert 命令来反做版本二，生成新的版本四，这个版本四里会保留版本三的东西，但撤销了版本二的东西。

```bash
git log
git revert -n 8b896210
git commit -m "xxx"
git push
```



# xx.清楚git记录的密码

```bash
git credential-manager uninstall   //重置windows本地所有的密码

git config --system --unset credential.helper
git config --global --unset credential.helper

// 修改了仓库密码，但是本地的密码没有修改为最新
git config --local --unset credential.helper

```

