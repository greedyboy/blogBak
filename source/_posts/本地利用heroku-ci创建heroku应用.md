---
title: 本地利用heroku ci创建heroku应用
urlname: heroku-index
tags:
  - heroku
categories:
  - heroku
date: 2019-05-09 21:40:28
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 本地创建heroku应用过程

<!-- more -->

### 注册heroku网址
- https://heroku.com

### 下载heroku软件
- https://heroku.com

### 本地执行命令建立app并推送到git
- 命令行如下，等待总结

```
登录
heroku操作

E:\PycharmProjects\herotest>heroku login
heroku: Press any key to open up the browser to login or q to exit:
Opening browser to https://cli-auth.heroku.com/auth/browser/9c97ded1-*
heroku: Waiting for login... !
SyntaxError: Unexpected end of JSON input
    at JSON.parse (<anonymous>)
    at HTTP._parse (e:/Program Files/heroku/client/node_modules/http-call/lib/http.js:342:30)

E:\PycharmProjects\herotest>heroku login
heroku: Press any key to open up the browser to login or q to exit:
Opening browser to https://cli-auth.heroku.com/auth/browser/6ac21c80-*
Logging in... done
Logged in as ***@gmail.com



Install the Heroku CLI
Download and install the Heroku CLI.

If you haven't already, log in to your Heroku account and follow the prompts to create a new SSH public key.

$ heroku login
Clone the repository
Use Git to clone gapp's source code to your local machine.

$ heroku git:clone -a gapp
$ cd gapp
Deploy your changes
Make some changes to the code you just cloned and deploy them to Heroku using Git.

$ git add .
$ git commit -am "make it better"
$ git push heroku master

```



