---
title: mongodb4安装记录
urlname: mongodb-index
tags:
  - mongodb
categories:
  - mongodb
date: 2019-04-25 23:54:34
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 安装mongodb过程及配置，中间出现假死现象。

<!-- more -->

### mongodb下载
- https://www.mongodb.com/download-center

### 安装
- 安装过程中可以修改目录
- 安装过程注意有个屏幕右下角“MongoDB compass”取消，有可能出现假死
- 一路下一步完成

### 配置
- 我把程序安装在了E:\Program Files\mongodb，以后表示为安装目录
- 在安装目录\data文件夹下创建新的文件夹db
- 在安装目录\log文件夹下创建新文件mongo.config
- 在安装目录\bin管理员打开cmd，或者打开cmd.exe后文件夹转移到这里
- 运行以下命令
- 运行`.\mongod –dbpath  E:\Program Files\MongoDB\data\db`
- 浏览器中打开http://localhost:27017
- 出现以下文字表示成功`It looks like you are trying to access MongoDB over HTTP on the native driver port.`

### 继续配置
```
.\mongod –dbpath  E:\Program Files\MongoDB\data\db

.\mongod –dbpath E:\Program Files\MongoDB\data\db   
.\mongod –logpath E:\Program Files\MongoDB\log\mongo.log   
.\mongod –logappend   
.\mongod –serviceName MongoDB   
.\mongod –auth   
.\mongod –install   
```

### 开启和关闭服务
- 开启`net start MongoDB`
- 关闭`net stop MongoDB`

### 安装mongodb compass
- 下载https://www.mongodb.com/download-center/compass
- 选择`community Edition Stable`，`Windows 64-bit 7+`的exe版本
- 下载后直接安装即可使用

### 饮水思源
- https://blog.csdn.net/m0_37243869/article/details/81165931
- http://www.runoob.com/mongodb/mongodb-window-install.html