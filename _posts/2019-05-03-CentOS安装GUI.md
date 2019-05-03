---
layout: post
title: CentOS 安装GUI
subtitle: Linux学习笔记系列
date: 2019-05-03
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Linux
------
`CentOS`安装桌面
```
yum -y groups install "GNOME Desktop"
startx
```
配置源
```
yum install  epel* -y
```

安装`xrdp`
```
yum --enablerepo=epel -y install xrdp
```

启动`xrdp`并设置开机启动
```
systemctl start xrdp
systemctl enable xrdp
```