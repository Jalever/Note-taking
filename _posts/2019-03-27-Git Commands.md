---
layout: post
title: Git Common Commands
subtitle: Git Learning Notes
date: 2019-03-27
author: Jalever
header-img: img/post_2019_git_bg.png
catalog: true
tags:
  - Git
---

- [Common](#common)
    - [git init](#git-init)
    - [git add -A](#git-add--a)
    - [git add -u](#git-add--u)
    - [git add .](#git-add)
    - [git remote add origin URLPath](#git-remote-add-origin-urlpath)
    - [git remote set-url origin URLPath](#git-remote-set-url-origin-urlpath)
    - [git commit -m "comments"](#git-commit--m-%22comments%22)
    - [git push origin master](#git-push-origin-master)
    - [git push -u origin master -f](#git-push--u-origin-master--f)
    - [Git Getting Started](#git-getting-started)
- [创建版本库](#%E5%88%9B%E5%BB%BA%E7%89%88%E6%9C%AC%E5%BA%93)
    - [git clone <url>](#git-clone-url)
    - [git init](#git-init-1)
- [修改和提交](#%E4%BF%AE%E6%94%B9%E5%92%8C%E6%8F%90%E4%BA%A4)
    - [git status](#git-status)
    - [git diff](#git-diff)
    - [git add .](#git-add--1)
    - [git add <file>](#git-add-file)
    - [git mv <old> <new>](#git-mv-old-new)
    - [git rm <file>](#git-rm-file)
    - [git rm --cached <file>](#git-rm---cached-file)
    - [git commit -m "commit message"](#git-commit--m-%22commit-message%22)
    - [git commit --amed](#git-commit---amed)
- [查看提交历史](#%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)
    - [git log](#git-log)
    - [git log -p <file>](#git-log--p-file)
    - [git blame <file>](#git-blame-file)
- [撤销](#%E6%92%A4%E9%94%80)
    - [git reset --hard HEAD](#git-reset---hard-head)
    - [git checkout HEAD <file>](#git-checkout-head-file)
    - [git revert <commit>](#git-revert-commit)
- [分支和标签](#%E5%88%86%E6%94%AF%E5%92%8C%E6%A0%87%E7%AD%BE)
    - [git branch](#git-branch)
    - [git checkout <branch/tag>](#git-checkout-branchtag)
    - [git branch <new-branch>](#git-branch-new-branch)
    - [git branch -d <branch>](#git-branch--d-branch)
    - [git tag](#git-tag)
    - [git tag <tagname>](#git-tag-tagname)
    - [git tag -d <tagname>](#git-tag--d-tagname)
- [合并与衍合](#%E5%90%88%E5%B9%B6%E4%B8%8E%E8%A1%8D%E5%90%88)
    - [git merge <branch>](#git-merge-branch)
    - [git rebase <branch>](#git-rebase-branch)
- [远程操作](#%E8%BF%9C%E7%A8%8B%E6%93%8D%E4%BD%9C)
    - [git remote -V](#git-remote--v)
    - [git remote show <remote>](#git-remote-show-remote)
    - [git remote add <remote> <url>](#git-remote-add-remote-url)
    - [git fetch <remote>](#git-fetch-remote)
    - [git pull <remote> <branch>](#git-pull-remote-branch)
    - [git push <remote> <branch>](#git-push-remote-branch)
    - [git push <remote> :<branch/tag-name>](#git-push-remote-branchtag-name)
    - [git push --tags](#git-push---tags)

## Common

#### git init

#### git add -A

提交所有变化

#### git add -u

提交`被修改(modified)`和`被删除(deleted)`文件，不包括新文件(new)

#### git add .

提交`新文件(new)`和`被修改(modified)`文件，不包括被删除(deleted)文件

#### git remote add origin URLPath

#### git remote set-url origin URLPath
从别人的repository fetch下来之后，想要上传到自己的repository中的命令
#### git commit -m "comments"

#### git push origin master

#### git push -u origin master -f

#### Git Getting Started

[Link](https://git-scm.com/book/en/v2)

## 创建版本库

#### git clone <url>

克隆远程版本库

#### git init

初始化本地版本库

## 修改和提交

#### git status

查看状态

#### git diff

查看变更内容

#### git add .

跟踪所有改动过的文件

#### git add <file>

跟踪指定文件

#### git mv <old> <new>

文件改名

#### git rm <file>

删除文件

#### git rm --cached <file>

停止跟踪文件但不删除

#### git commit -m "commit message"

提交所有更新过的文件

#### git commit --amed

提交最后一次提交

## 查看提交历史

#### git log

查看提交历史<br>
`git log`输入之后可以输入`q`推出

#### git log -p <file>

查看指定文件的提交历史

#### git blame <file>

以列表方式查看制定文件的制定历史

## 撤销

#### git reset --hard HEAD

撤销工作目录中所有未提交文件的修改内容

#### git checkout HEAD <file>

撤销指定的未提交文件的修改内容

#### git revert <commit>

撤销指定的提交

## 分支和标签

#### git branch

显示所有本地分支

#### git checkout <branch/tag>

切换到指定分支或标签

#### git branch <new-branch>

创建新分支

#### git branch -d <branch>

删除本地分支

#### git tag

列出所有本地标签

#### git tag <tagname>

基于最新提交创建标签

#### git tag -d <tagname>

删除标签

## 合并与衍合

#### git merge <branch>

合并指定分支到当前分支

#### git rebase <branch>

衍合指定分支到当前分支

## 远程操作

#### git remote -V

查看远程版本库信息

#### git remote show <remote>

查看指定远程版本库信息

#### git remote add <remote> <url>

添加远程版本库

#### git fetch <remote>

从远程库获取代码

#### git pull <remote> <branch>

下载代码及快速合并

#### git push <remote> <branch>

上传代码及快速合并

#### git push <remote> :<branch/tag-name>

删除远程分支或标签

#### git push --tags

上传所有标签