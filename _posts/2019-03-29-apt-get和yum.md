---
layout: post
title: apt-get和yum命令
subtitle: Linux学习笔记系列
date: 2019-03-29
author: Jalever
header-img: img/home-bg-geek.jpg
catalog: true
tags:
  - Linux
---

- [Preface](#preface)
- [apt-get](#apt-get)
- [yum](#yum)

## Preface
`apt-get`和`yum`是两种`Linux`系统下最常见的安装包格式

## apt-get
1. `apt-get`可以用于运作`deb`包
2. `deb`包主要应用于`Debian`系列
3. `Ubuntu`
- 安装
> apt-get install <package_name> 
- 卸载
> apt-get remove <package_name> 
- 更新
> apt-get update <package_name>

## yum
1. `yum`可以用于运作`rpm`包
2. `rpm`包主要应用在`RedHat`系列
3. `Fedora`
4. `CentOS`
- 安装
> yum install <package_name> 
- 卸载
> yum remove <package_name> 
- 更新
> yum update <package_name> 