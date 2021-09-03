
$ git clone https://github.com/lpointer/devNote.git #拉取或关联仓库

## 配置相关
$ git config --global user.name "Your Name"		# 设置全局用户名
$ git config --global user.email "email@example.com"	# 设置全局用户邮箱
$ git config user.name  # 查看用户名
$ git config user.email # 查看用户邮箱

## 分支相关
$ git switch -c dev 	#创建dev分支并切换至dev
$ git checkout dev	#切换分支
$ git branch #查看本地所有分支
$ git branch -a #查看远程所有分支
$ git branch -d xxx	#删除本地分支
$ git branch -dr xxx #删除远程分支

## 查看日志相关
$ git log 	 #查看当前分支提交记录
$ git log --oneline #只看提交的message
$ git reflog #查看历史执行记录

## 常用相关
$ git diff   #对比修改的内容
$ git add .  #添加文件
$ git stash   #存入工作空间
$ git stash clear   #清除工作空间
$ git status #查看在你上次提交之后是否有对文件进行再次修改
$ git commit -m # 提交所有暂存区文件至本地仓库 m = message提交备注信息
$ git commit [file] [file2] ... -m # 提交暂存区指定文件至本地仓库 m = message提交备注信息
$ git commit --amend	# 追加提交暂存区所有文件至本地仓库（不够熟悉情况下慎用！！！）
$ git commit -a		# -a 参数设置修改文件后不需要执行 git add 命令，直接来提交

## 推送拉取远程分支相关
$ git pull #拉取远程代码
$ git pull origin develop	#远程拉取指定的分支
$ git push #推送代码到远程服务器
$ git push -f #强制推送代码到远程服务器（不够熟悉情况下慎用！！！）
$ git push origin develop # 推送到指定的远程分支
$ git push origin develop_luyi:develop_luyi #把自己的分支推送到远程
$ git push origin --delete xxx	#删除远程分支

## 回退相关
$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ [file] 	 # 回退 file 文件的版本到上一个版本  
$ git reset 052e            # 回退到指定版本

## 合并相关	（合并完切记要push推送上去，有冲突解决冲突之后也需要push）
$ git merge develop # 当前分支合并develop分支
$ git merge --continue	#合并完成确认 （合并完之后需要执行该命令确认） 

## 高级功能
$ git branch --set-upstream-to=develop_luyi -u origin/develop_luyi #设置本地的分支与远程的分支关联
