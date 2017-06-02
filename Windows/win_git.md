<header><h2 align="center">Windows搭建Git环境</h2></header>

Git作为一种版本控制命令系统，可以很好地辅助进行项目开发与版本禁止，越来越多地被应用到项目开发中去。

Unix系统，一般都已经预装了Git，而且用户可以通过更新获取最新版。对于Windows系统，用户可以选择从[官网](https://git-scm.com/downloads)根据位数下载相应的".exe"安装程序。然后一路下一步间或设置一些选项，就完成了。安装完成后可以通过`git --version`查看Git版本。

### Git基本配置

Git配置通常使用`git config`命令，但它也分为三个级别
```bash
git config --system # 系统级，位于/etc/config
git config --global # 用户级，位于~/.gitconfig
git config --local # 仓库级，位于repo/.git/config
```
其中，"--local"优先级最高

下面更多地以Github为远程仓库来介绍配置流程

1. 配置用户参数
	```bash
	git config --global user.name "username"
	git config --global user.email "useremail"
	git config --global push.default matching

	git config --global diff.tool meld
	git config --global merge.tool meld
	git config --global color.ui.true
	```

2. 基本操作
	```bash
	git clone git@github.com:USERNAME/repo.git # 非必须
	cd repo # 非必须
	git init # 如果是自己在本地新建的工程，在工程顶级目录进行该操作
	git add .
	git commit -m "The first commit ."
	git remote add origin git@github.com:USERNAME/repo.git
	git push -u origin master # 仅第一次需要加"-u"的参数
	```

3. 查看状态
	```bash
	git status # 查看当前项目状态
	git log --pretty=oneline # 查看提交历史
	git branch # 查看本地分支，加"-a"可以查看远程分支
	git diff # 查看不同
	```

4. 将远程仓库同步到本地
	```bash
	git remote -v # 查看已关联远程仓库，如果没有关联的远程仓库，执行`git remote add origin git@github.com:USERNAME/repo.git`
	git fetch origin
	git diff.tool <local-branch> origin/master
	git merge origin/master # 如果报错，则执行`git mergetool`
	```

5. 撤销与回退
	```bash
	git checkout -- <filename> # 撤销工作区的修改至上一次commit或add后的状态
	git reset HEAD <filename> # 撤销提交到暂存区的某个文件
	git reset HEAD . # 撤销提交到暂存区的所有文件
	git reset --hard <commit-id> # 撤销提交到版本库的修改，也可以用"HEAD^"、"HEAD^^"等表示之前的版本
	git rm <filename> # 从版本库删除文件
	git revert <commit-id> # 在代码已经push到线上的情况下，才用该命令回滚
	```
	> revert是用一次新的commit来回滚之前的commit，更安全；reset则是直接删除指定的commit，若直接push会导致冲突。

6. 分支管理
	```bash
	git branch (-a) # 查看已有分支
	git checkout <branch> # 创建或者切换到某分支
	git checkout -b <newbranch> # 创建并切换到该分支
	git push (-u) origin <remote-branch-name> # 推送到远程分支，只需在第一次推送时添加"-u"参数
	git push --set-upstream origin <remote-branch-name>

	git branch -d <branch> # 删除本地分支，若当前分支因为有修改未提交或其它情况不能删除，使用-D选项强制删除。
	git push origin --delete <remote-branch-name> # 删除远程分支
	git remote prune origin # 清除无用的分支：remote上的一个分支被其他人删除后，需要更新本地的分支列表。
	git branch --set-upstream <local-branch> origin/branch # 获取远程分支到本地已有分支
	git checkout -b <local-branch> <remote-branch> # 获取远程分支到本地并新建本地分支

	git fetch origin <remote-branch> # 获取远程最新分支
	git difftool <local-branch> origin/<remote-branch> # 查看更新内容
	git merge origin/<remote-branch> # 尝试合并远程分支到当前分支
	git mergetool # 非必须，如果报错，则执行`git mergetool`来解决冲突

7. 删除本地仓库
	```bash
	git branch -d <branch-name>
	git tag -d <tag-name>
	git rm -r --cached . # 删除本地缓存，使得新的".gitignore"文件能够生效
	git gc --prune=now # 清理".git"目录，一般本地仓库过大都是由于存在过多的loose object
	```
	> 在执行push操作时，git会自动执行一次gc操作，不过只有loose object达到一定数量后才会真正调用，建议手动执行。

