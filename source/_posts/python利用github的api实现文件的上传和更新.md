---
title: python利用github的api实现文件的上传和更新
urlname: python-github-api-index
tags:
  - python
  - github
categories:
  - python
date: 2019-04-26 13:06:04
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> python利用官方的api实现文件的上传和更新。

<!-- more -->

### 申请github的tokens
- https://github.com/settings/tokens

### 根据官方api说明进行设定
- https://developer.github.com/v3/repos/contents/#get-contents

### 上传新文件代码实例
```
import requests,base64,random,time,json

def creat_file(strx=''):
    randx=random.randint(1000, 9999)
    fn= ''+ time.strftime("%Y%m%d%H%M%S", time.localtime())+str(randx)+'.txt'
    with open(fn, 'a+') as f:
        f.write(fn + '\n')  # 加\n换行显示
        f.write(strx)
    return fn

def fn_base64(fn):
    # 打开本地图片，并转化为base64
    f = open(fn, 'rb')
    fnb64 = base64.b64encode(f.read()).decode('utf-8')
    return fnb64

tokens='6b987297b89c4f8e0'#

fn=creat_file('sxs')
url = "https://api.github.com/repos/[user]/[proj]/contents/[path]/"+ fn
# d = {
   "message": "my commit message",
   "committer": {
     "name": "user",
     "email": "user@163.com"
   },
   "content": fn_base64(fn)
 }


headers = {"Authorization": 'token '+tokens} # 前两行会在后面的代码中忽略掉不写
r = requests.put(url=url,data=json.dumps(d), headers=headers)
rs=r.status_code
if rs==201:
    print('sucess')
#出现422错误，有可能是文件在项目中已经存在了。

```

### 获取sha为update更新文件做准备
```
#get content
url = "https://api.github.com/repos/[user]/[proj]/contents/[path]/"+ fn
r=requests.get(url=url,headers=headers)
if r.status_code==200:
    sha=json.loads(r.text)['sha']
else:
    sha=''

```


### 更新文件，需要核对文件名和sha一致时候方可进行
```
d={
  "message": "my commit message update",
  "committer": {
    "name": "Scott Chacon",
    "email": "schacon@gmail.com"
  },
  "content": fn_base64(fn),
    "sha":sha
}
url = "https://api.github.com/[user]/[proj]/contents/[path]/"+ fn

headers = {"Authorization": 'token '+tokens} # 前两行会在后面的代码中忽略掉不写
r = requests.put(url=url,data=json.dumps(d), headers=headers)

print(r.status_code)

#200说明成功
```

### 添加comment
```
#!/usr/bin/env python 
# -*- coding:utf-8 -*-
"""info

"""
import requests,base64,random,time,json
tokens='7b89c4f8e0'#
url = "https://api.github.com/repos/[user]/[proj]/issues/[n]/comments"

d={
  "body": "i am a boy"
}

headers = {"Authorization": 'token '+tokens} # 前两行会在后面的代码中忽略掉不写
r = requests.post(url=url,data=json.dumps(d), headers=headers)

rs=json.loads(r.text)
print(r.status_code)
print(rs)

```

### 饮水思源
- https://developer.github.com/v3/repos/contents/#get-contents
- https://segmentfault.com/a/1190000015144126
- 