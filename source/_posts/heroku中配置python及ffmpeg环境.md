---
title: heroku中配置python及ffmpeg环境
urlname: heroku-python-ffmpeg-index
tags:
  - heroku
  - python
  - ffmpeg
categories:
  - 软件列表
date: 2019-11-07 09:20:24
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 在heroku中配置python环境，及利用ffmpeg进行多媒体处理。

<!-- more -->

### heroku
- 有一定的免费额度，进行测试可用。
- 支持多种环境
- git配置，可以进行github使用。

### 安装heroku
- http://www.heroku.com
- 安装cil
- `heroku login`
- 登录方法等等，其他基础知识查阅官方网站。
- 创建app

### 设置app的buildpack
- https://dashboard.heroku.com/apps/`[app name]`/settings
- 选择`heroku/python`和`https://github.com/jonathanong/heroku-buildpack-ffmpeg-latest.git`
- 注意顺序

### deploy
- https://dashboard.heroku.com/apps/`[app name]`/deploy/heroku-git
- 紧跟`Deploy using Heroku Git`步骤，没问题

### heroku run
- 本地项目文件夹运行git bash
- 运行命令出现如下结果表示都已经安装完成
```
$ heroku buildpacks
=== ginomempin-ffmpeg-app Buildpack URLs
1. heroku/python
2. https://github.com/jonathanong/heroku-buildpack-ffmpeg-latest.git
```

### 检测ffmpeg状态
- https://dashboard.heroku.com/apps/t2video/deploy/heroku-git?web-console=`[app name]`
- 打开console远程端
- `ffmpeg`运行能显示则没问题
- `python pytest.py`可运行程序查看自编译程序。


### 饮水思源
- https://elements.heroku.com/buildpacks/jonathanong/heroku-buildpack-ffmpeg-latest#buildpack-instructions
- https://stackoverflow.com/questions/58146519/how-to-use-the-heroku-buildpack-ffmpeg-for-python