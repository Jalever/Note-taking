---
layout: post
title: Linux上安装MongoDB
subtitle: MongoDB学习笔记系列
date: 2019-03-29
author: Jalever
header-img: img/home-bg-geek.jpg
catalog: true
tags:
  - MongoDB
  - Database
---

## 下载完安装包，并解压 `tgz`
```
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.6.tgz    # 下载
tar -zxvf mongodb-linux-x86_64-3.0.6.tgz                                   # 解压

mv  mongodb-linux-x86_64-3.0.6/ /usr/local/mongodb                         # 将解压包拷贝到指定目录
```

## 添加到`PATH`路径中
```
export PATH=$PATH:/usr/local/mongodb/bin
```