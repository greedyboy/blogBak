---
title: python中base64加密解密
urlname: index
tags:
  - python
  - base64
categories:
  - python
date: 2019-04-29 10:46:11
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 利用python对字符串或者文件进行base64位加密解密。

<!-- more -->

### 内容提示
- 字符加密
- 字符串解密
- 文件加密
- 文件解密

### 代码
```
#!/usr/bin/env python 
# -*- coding:utf-8 -*-
"""info

"""

import base64
def encode_str(strs):
    #加密
    # s1='40ab6290da9a5c2ddd43760511a01e8af21b5187'
    encodestr = base64.b64encode(strs.encode('utf-8'))
    enstrs=str(encodestr,'utf-8')
    print(enstrs)
    return enstrs

def decode_str(enstrs):
    #解密
    # enstr='5pyJ5b+D55qE5L2g77yM55yL5Yiw5LqG5pyJ5b+D55qE5oiR77yM5LiN5b6X5LiN6K+05piv5LiA56eN57yY5YiG77yM5aaC5p6c5L2g5Zyo5aWL5paX77yM5Yqg5rK577yM54ix6Ieq5bex77yM54ix5pyL5Y+L77yM54ix5a625Lq644CC'

    strs=str(base64.b64decode(enstrs[:].encode('utf-8')),'utf-8')
    print(strs)
    return strs

def endcode_file(fn):
    # 文件转化为base64
    f = open(fn, 'rb')
    fnb64 = base64.b64encode(f.read()).decode('utf-8')
    return fnb64

def decode_file(fn):
    # 文件转化为base64
    f = open(fn, 'rb')
    fnb64str = str(base64.b64decode(f.read()).ecode('utf-8'),'utf-8')
    return fnb64str

if __name__=="__main__":

    pass

```
### 网络工具
- 的确最好用https://base64.us/
- http://tool.oschina.net/encrypt?type=3
- 图片转64位http://imgbase64.duoshitong.com/