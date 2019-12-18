---
title: python获取粘贴板
urlname: python-clip-index
tags:
  - python
categories:
  - 软件列表
date: 2019-11-16 22:30:04
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 直接上代码

<!-- more -->

### 获取windows粘贴板剪切板

```
# -*- coding: utf-8 -*-
# pip install pywin32
import win32clipboard as wc
import win32con

def getCopyText():
    wc.OpenClipboard()
    copy_text = wc.GetClipboardData(win32con.CF_TEXT)
    wc.CloseClipboard()
    return copy_text.decode('utf-8')

# test
# import chardet
# print(chardet.detect(getCopyText()))  # 找到包含中文内容的字符串编码
print(getCopyText()) # 转码

```