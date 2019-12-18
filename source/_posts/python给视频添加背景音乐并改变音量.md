---
title: python给视频添加背景音乐并改变音量
urlname: python-ffmpeg-index
tags:
  - python
  - ffmpeg
categories:
  - 软件列表
date: 2019-10-31 17:06:48
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 用到给视频添加背景音乐，并改变音量。记录一下，与碰到同样问题的朋友共享。

<!-- more -->

### 直接上代码吧，干就完了

```
import subprocess

inmp4='E:/PycharmProjects/untitled2/hecheng/191030_232_xs.mp4'
inmp3='E:/PycharmProjects/untitled2/hecheng/bg.mp3'
inmp32='E:/PycharmProjects/untitled2/hecheng/bg2.mp3'
outmp3='E:/PycharmProjects/untitled2/hecheng/bg_out.mp3'
outmp4='E:/PycharmProjects/untitled2/hecheng/191030_232_xs_bg.mp4'


cmd='ffmpeg -y -i '+ inmp4 +' -i '+ inmp3 +' -filter_complex \
"[0:a]volume=10dB[a0]; \
[1:a]volume=-10dB[a1]; \
[a0][a1]amix=inputs=2[a]" \
-map 0:v -map "[a]" -c:v copy -c:a aac -shortest '+ outmp4

p = subprocess.call(cmd, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)

# 查看音轨信息
print('*'*80)
cmd='ffmpeg -i '+ outmp3 +' -filter_complex volumedetect -c:v copy -f null /dev/null'
P = subprocess.call(cmd)

```

### 记录几个cmd
```
# 分别降低音量后叠加
cmd='ffmpeg -y -i '+ inmp4 +' -i '+ inmp3 +' -filter_complex \
"[0:a]volume=10dB[a0]; \
[1:a]volume=-30dB[a1]; \
[a0][a1]amix=inputs=2[a]" \
-map 0:v -map "[a]" -c:v copy -c:a aac -shortest '+ outmp4

# 纯音频，叠加，可控制音量，并且设置一个循环，并按照第一个截取时间
cmd='ffmpeg -y -i '+ mp4p3 +' -i '+ inmp3 +' -filter_complex \
"[0:a]volume=10dB[a0]; \
[1:a]aloop=loop=-1:size=2e+09[a1]; \
[a1]volume=-15dB[a12]; \
[a0][a12]amix=inputs=2:duration=first:dropout_transition=2" ' + outmp4mp3

# 视频添加循环音乐
cmd='ffmpeg -y -i '+ inmp4 +' -i '+ inmp3 +' -filter_complex \
"[0:a]volume=10dB[a0]; \
[1:a]aloop=loop=-1:size=2e+09[a1]; \
[a1]volume=-15dB[a12]; \
[a0][a12]amix=inputs=2:duration=first:dropout_transition=2[a]" \
-map 0:v -map "[a]" -c:v copy -c:a aac -shortest '+ outmp4

```

### ffmpeg 隐藏调试信息
```
 -loglevel quiet 
```


### 饮水思源
- https://stackoverflow.com/questions/13780736/ffmpeg-unable-to-find-a-suitable-output-format-for-i
- https://stackoverflow.com/questions/44712868/ffmpeg-set-volume-in-amix