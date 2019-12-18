---
title: python引用配置文件json
urlname: index
tags:
  - diary
categories:
  - daybreak
date: 2019-04-28 11:56:23
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> python在不同目录下引用配置文件，可能会出错，尤其是嵌套引用过程中，设置不正确，容易出现问题。此坑已填，舒服。

<!-- more -->
###目录结构
```
└── folder
    ├── setting
    │   └── setx.json
    │   └── setx.py
    |   └── check.py
    |   └── __init__.py 
    └── webs
    │   └── __init__.py
    │   └── login.py
    └── web.py
    └── __init__.py

```
### 配置文件json
- 文件名为sets.json
```
{
    "name":"pizi",
    "posts":{
        .......
    }
}

```
### setx.py内读取配置
- linux虚拟主机测试通过
```
import json,os,sys

def load_sets():
    #当前目录绝对路径
    work_dir = os.path.dirname(os.path.abspath(__file__))
    #切换工作环境
    os.chdir(work_dir)
    print(work_dir)
    CONF_FILE ='setx.json'
    with open(CONF_FILE, 'r', encoding='utf-8') as b_oj:
        settings = json.load(b_oj)
    return settings
```


### 在web.py下调用setx.py
- linux测试通过
- 运行时候会把当前目录作为工作目录，直接根据相对目录引用
```
import sys
from setting.setx import load_sets
s=load_sets()
```

### 在login.py下调用setx.py
```
import sys,os
pathx=os.path.abspath(os.path.dirname(os.path.dirname(__file__)))
sys.path.append(pathx)
## 添加文件所在目录的上级目录到运行环境目录，再根据相对引用方法进行引用
print(sys.path)
from testp.setx import load_sets
s=load_sets()
```

### 在check.py下调用setx.py
- 依据相对目录的方式调用
```
from setx import load_sets
s=load_sets()
print(s)
```

### 各种python获取目录
```
import os

print '***获取当前目录***'
print os.getcwd()
print os.path.abspath(os.path.dirname(__file__))

print '***获取上级目录***'
print os.path.abspath(os.path.dirname(os.path.dirname(__file__)))
print os.path.abspath(os.path.dirname(os.getcwd()))
print os.path.abspath(os.path.join(os.getcwd(), ".."))

print '***获取上上级目录***'
print os.path.abspath(os.path.join(os.getcwd(), "../.."))
```

### python添加工作目录
```
sys.path.append(pathx)
```

### 饮水思源
- https://blog.csdn.net/xuqi7/article/details/78757548
- https://www.cnblogs.com/damumu/p/7321540.html
- https://www.cnblogs.com/apollo1616/p/9513510.html