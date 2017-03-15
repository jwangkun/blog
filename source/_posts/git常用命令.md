---
title: Git常用命令
date: 2016-12-21 21:58:38
tags: git命令
---

$ git clone #克隆远程版本库
$ git init #初始化本地版本库
修改和提交

$ git status #查看状态
$ git diff #查看变更内容
$ git add . #跟踪所有改动过的文件
$ git add #跟踪指定的文件
$ git mv #文件改名
$ git rm #删除文件
$ git rm –cached #停止跟踪文件但不删除
$ git commit -m “commit message” #提交所有更新过的文件
$ git commit –amend #修改最后一次提交
查看提交历史

$ git log #查看提交历史
$ git log -p #查看指定文件的提交历史
$ git blame #以列表方式查看指定文件的提交历史
撤消

$ git reset –hard HEAD #撤消工作目录中所有未提交文件的修改内容
$ git checkout HEAD #撤消指定的未提交文件的修改内容
$ git revert #撤消指定的提交
分支与标签

$ git branch #显示所有本地分支
$ git checkout #切换到指定分支或标签
$ git branch #创建新分支
$ git branch -d #删除本地分支
$ git tag #列出所有本地标签
$ git tag #基于最新提交创建标签
$ git tag -d #删除标签
合并与衍合

$ git merge #合并指定分支到当前分支
$ git rebase #衍合指定分支到当前分支
远程操作

$ git remote -v #查看远程版本库信息
$ git remote show #查看指定远程版本库信息
$ git remote add #添加远程版本库
$ git fetch #从远程库获取代码
$ git pull #下载代码及快速合并
$ git push #上传代码及快速合并
$ git push : #删除远程分支或标签
$ git push –tags #上传所有标签