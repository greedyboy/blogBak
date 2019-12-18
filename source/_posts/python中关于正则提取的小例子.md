---
title: python中关于正则提取的小例子
urlname: python-re-index
tags:
  - python
  - 正则
categories:
  - python
date: 2019-10-30 10:31:59
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 一个小例子，关于正则表达式的应用。python中正则例子。

<!-- more -->

### 直接代码

直接上代码吧。不多说，应用中用到了。

```
import  re

    # url = "http://news.nankai.edu.cn/ywsd/index${12-34}.shtml"
    url = "http://news.nankai.edu.cn/ywsd/index.shtml"

    matchObj = re.match(r'(.*)\$\{(.*)-(.*)\}(.*)', url, re.M | re.I)
    if matchObj:
        print("matchObj.group() : ", matchObj.group())

        print("matchObj.group(1) : ", matchObj.group(1))

        print("matchObj.group(2) : ", matchObj.group(2))
        print("matchObj.group(3) : ", matchObj.group(3))
        print("matchObj.group(4) : ", matchObj.group(4))

        for i in range(int(matchObj.group(2)),int(matchObj.group(3))+1):
            urlnn=matchObj.group(1)+str(i)+matchObj.group(4)
            print(urlnn)

    else:
        print(url)

    pass
```


### 饮水思源
- https://www.runoob.com/python/python-reg-expressions.html
