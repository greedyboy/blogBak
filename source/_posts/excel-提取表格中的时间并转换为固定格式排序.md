---
title: excel 提取表格中的时间并转换为固定格式排序
urlname: excel-index
tags:
  - excel
categories:
  - 软件列表
date: 2019-11-08 10:00:14
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 运用中将excel中某个不规则的时间，提取出来进行排序，比如导出的课表中时间。

<!-- more -->

### 目标
- 2018/9/27 时间：16:05--17:45 
- 2018092716

### excel代码
```
=TEXT(LEFT(D2,FIND("时",D2,1)-2),"yyyymmdd") & MID(D2,FIND("时",D2,1)+3,2)
```

