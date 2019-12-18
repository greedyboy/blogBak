---
title: pycharm个性化python新建文件模板
urlname: python-new-pycharm-index
tags:
  - python
  - pycharm
categories:
  - python
date: 2019-04-29 11:30:50
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 在pycharm中新建文件时候，使用固定的模板，这样比较有逼格，我是这样做到的。

<!-- more -->
### 软件设置
- 打开pycharm
- `File`-`Settings`-`Editor`--`Color&Style`--`File and Templates`--`Python-Script`

### 可使用系统变量
```
可用的预定义文件模板变量为：

$ {PROJECT_NAME} - 当前项目的名称。

$ {NAME} - 在文件创建过程中在“新建文件”对话框中指定的新文件的名称。

$ {USER} - 当前用户的登录名。

$ {DATE} - 当前的系统日期。

$ {TIME} - 当前系统时间。

$ {YEAR} - 今年。

$ {MONTH} - 当月。

$ {DAY} - 当月的当天。

$ {HOUR} - 目前的小时。

$ {MINUTE} - 当前分钟。

$ {PRODUCT_NAME} - 将在其中创建文件的IDE的名称。

$ {MONTH_NAME_SHORT} - 月份名称的前3个字母。 示例：1月，2月等

$ {MONTH_NAME_FULL} - 一个月的全名。 示例：1月，2月等
```

### 我的设置
```
#!/usr/bin/env python 
# -*- coding:utf-8 -*-
# @Time    : ${DATE} ${TIME}
# @Author  : Greedyboy
# @Email   : greedyboy@163.com
# @File    : ${NAME}.py
# @Software: ${PRODUCT_NAME}
"""info

"""
def aq_x():

    pass

if __name__=="__main__":

    pass
```

### 饮水思源
- https://www.cnblogs.com/mat-wu/p/7130358.html
- https://www.cnblogs.com/luke0011/p/8084476.html