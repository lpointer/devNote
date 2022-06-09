# git

``` cmd

$ git remote add origin git@github.com:lpointer/devNote.git  #本地关联远程分支	(可关联多个远程分支)
$ git remote add origin git@gitee.com:lpointer/devNote.git  #本地关联远程分支	(可关联多个远程分支)
$ git remote -v #查看已关联的分支
$ git remote rm origin #移除已关联的远程分支
$ git push github master # 推送到github的远程分支		(在关联多个远程分支的情况下)
$ git push gitee master  # 推送到gitee的远程分支		(在关联多个远程分支的情况下) 
$ git pull github master # 拉取github的远程分支		(在关联多个远程分支的情况下) 
$ git pull gitee master  # 拉取gitee的远程分支			(在关联多个远程分支的情况下) 


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
$ git commit --amend	# 追加提交暂存区所有文件至本地仓库，上个分支未推送到远程可以使用（不够熟悉情况下慎用！！！）
$ git commit -a		# -a 参数设置修改文件后不需要执行 git add 命令，直接来提交
$ git checkout .	#放弃当前全部修改
$ git checkout -- filename #放弃工作区中某个文件的修改

## 推送拉取远程分支相关
$ git pull #拉取远程代码
$ git pull origin develop	#远程拉取指定的分支
$ git push #推送代码到远程服务器
$ git push -f #强制推送代码到远程服务器（不够熟悉情况下慎用！！！）
$ git push origin develop # 推送到指定的远程分支
$ git push origin develop_ly:develop_ly #把自己的分支推送到远程
$ git push origin --delete xxx	#删除远程分支

## tag相关
$ git tag # 查看tag的命令
$ git tag tagName -m "message" #创建tag

## 回退相关
$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ [file] 	 # 回退 file 文件的版本到上一个版本  
$ git reset 052e            # 回退到指定版本

## 合并相关	（合并完切记要push推送上去，有冲突解决冲突之后也需要push）
$ git merge develop # 当前分支合并develop分支
## 出现合并冲突的时候，需要先解决冲突，进行 add 之后在进行执行继续合并
$ git merge --continue	#合并完成确认 （合并完之后需要执行该命令确认） 

## 高级功能
$ git branch --set-upstream-to=develop_ly -u origin/develop_ly #设置本地的分支与远程的分支关联

```

<div>
    <span style="color:#e3d859">commit 642d85eb58c6f718ece85492122f8be7f0be6244</span>
    <span style="color:blue">HEAD -> </span>
    <span style="color:#00ff37">develop_ly, </span>
    <span style="color:red">origin/develop_ly, origin/develop, </span>
    <span style="color:#00ff37">develop </span>
</div>
本地develop分支要合并自己的本地分支（develop_ly）才能提交到远程



# git commit 提交规范

```text
<type>(<scope>): <subject>

<body>

<footer>
```

大致分为三个部分(使用空行分割):

1. 标题行: 必填, 描述主要修改类型和内容
2. 主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
3. 页脚注释: 放 Breaking Changes 或 Closed Issues

### type

commit 的类型：

- feat: 新功能、新特性  
- fix: 修改 bug
- perf: 更改代码，以提高性能（在不影响代码内部行为的前提下，对程序性能进行优化）
- refactor: 代码重构（重构，在不影响代码内部行为、功能下的代码修改）
- docs: 文档修改
- style: 代码格式修改, 注意不是 css 修改（例如分号修改）
- test: 测试用例新增、修改
- build: 影响项目构建或依赖项修改
- revert: 恢复上一次提交
- ci: 持续集成相关文件修改
- chore: 其他修改（不在上述类型中的修改）
- release: 发布新版本
- workflow: 工作流相关文件修改

### scope

commit 影响的范围, 比如: route, component, utils, build...

### subject

commit 的概述

### body

commit 具体修改内容, 可以分为多行.

### footer

一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.

## 约定式提交规范

以下内容来源于：[https://www.conventionalcommits.org/zh-hans/v1.0.0-beta.4/](https://link.zhihu.com/?target=https%3A//www.conventionalcommits.org/zh-hans/v1.0.0-beta.4/)

- 每个提交都必须使用类型字段前缀，它由一个名词组成，诸如 `feat` 或 `fix` ，其后接一个可选的作用域字段，以及一个必要的冒号（英文半角）和空格。
- 当一个提交为应用或类库实现了新特性时，必须使用 `feat` 类型。
- 当一个提交为应用修复了 `bug` 时，必须使用 `fix` 类型。
- 作用域字段可以跟随在类型字段后面。作用域必须是一个描述某部分代码的名词，并用圆括号包围，例如： `fix(parser):`
- 描述字段必须紧接在类型/作用域前缀的空格之后。描述指的是对代码变更的简短总结，例如： `fix: array parsing issue when multiple spaces were contained in string.`
- 在简短描述之后，可以编写更长的提交正文，为代码变更提供额外的上下文信息。正文必须起始于描述字段结束的一个空行后。
- 在正文结束的一个空行之后，可以编写一行或多行脚注。脚注必须包含关于提交的元信息，例如：关联的合并请求、Reviewer、破坏性变更，每条元信息一行。
- 破坏性变更必须标示在正文区域最开始处，或脚注区域中某一行的开始。一个破坏性变更必须包含大写的文本 `BREAKING CHANGE`，后面紧跟冒号和空格。
- 在 `BREAKING CHANGE:` 之后必须提供描述，以描述对 API 的变更。例如： `BREAKING CHANGE: environment variables now take precedence over config files.`
- 在提交说明中，可以使用 `feat` 和 `fix` 之外的类型。
- 工具的实现必须不区分大小写地解析构成约定式提交的信息单元，只有 `BREAKING CHANGE` 必须是大写的。
- 可以在类型/作用域前缀之后，: 之前，附加 `!` 字符，以进一步提醒注意破坏性变更。当有 `!` 前缀时，正文或脚注内必须包含 `BREAKING CHANGE: description`

## 示例

### fix

如果修复的这个BUG只影响当前修改的文件，可不加范围。如果影响的范围比较大，要加上范围描述。

例如这次 BUG 修复影响到全局，可以加个 global。如果影响的是某个目录或某个功能，可以加上该目录的路径，或者对应的功能名称。

```text
// 示例1
fix(global):修复checkbox不能复选的问题
// 示例2 下面圆括号里的 common 为通用管理的名称
fix(common): 修复字体过小的BUG，将通用管理下所有页面的默认字体大小修改为 14px
// 示例3
fix: value.length -> values.length
```

### feat

```text
feat: 添加网站主页静态页面

这是一个示例，假设对点检任务静态页面进行了一些描述。
 
这里是备注，可以是放BUG链接或者一些重要性的东西。
```

### chore

chore 的中文翻译为日常事务、例行工作，顾名思义，即不在其他 commit 类型中的修改，都可以用 chore 表示。

```text
chore: 将表格中的查看详情改为详情
```

## 参考资料

- [约定式提交](https://link.zhihu.com/?target=https%3A//www.conventionalcommits.org/zh-hans/v1.0.0-beta.4/)
