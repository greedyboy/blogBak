---
title: scrapy通过css和xpath抓取内容调试
urlname: scrapy-css-xpath-index
tags:
  - scrapy
categories:
  - 软件列表
date: 2019-10-18 09:59:54
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 近日使用爬虫scrapy，过程中需要用到对于信息的提取，进行总结，以备后查。

<!-- more -->

### 安装scrapy
- 使用pip install scrapy
- 注意：过程中有可能存在twist安装出现问题，可以通过百度查找，因为距离当时安装有一段时间了，忘记怎么填坑的了，貌似是通过下载wheel包，手动安装的。

### 初始化scrapy并创建项目
- 暂时不总结

### 测试并进行采集
- 主要是记录几个规则
- 抓取页面
    - `scrapy shell http://news.nankai.edu.cn/ywsd/index.shtml`
- 抓取内容
    - 抓取css内容中以某些字符开始的href
    - `response.css('.cms_block_span a[href^="http://news."]::attr(href)').extract()`
    - 抓取xpath内容，xpth可以同chrome浏览器右键得的xpath,直接复制可以。
    - `response.xpath('//*[@id=\"root\"]/table[3]/tbody/tr/td[1]/table[2]/tbody/tr[1]/td//text()').extract_first()`
    - 抓取xpath内容内部图片的地址。如果是内容,则直接在地址后加`//text`,如果为img的src，则为`//img/@src`
    - `response.xpath('//*[@id=\"root\"]/table[3]/tbody/tr/td[1]/table[2]/tbody/tr[3]//img/@src').extract()`
    - 下面几个有代表意义的参考

### 备注用到的几个规则记录

```
  "methods": {
    "nankai": {
      "info": "南开大学",
      "enable": true,
      "urls": {
        "http://news.nankai.edu.cn/qqxy/index.shtml": true,
        "http://news.nankai.edu.cn/nkyw/index.shtml": false,
        "http://news.nankai.edu.cn/zhxw/index.shtml": false
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".news a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".news-content",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".news-content img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "南开",
          "南开大学",
          "nankai.info"
        ],
        "categories": [
          "南开大学",
          "nankai.info"
        ]
      },
      "posts": {
        "api_nf": true
      }
    },
    "cumt": {
      "info": "中国矿业大学",
      "enable": true,
      "urls": {
        "http://xwzx.cumt.edu.cn/513/list.htm": false,
        "http://xwzx.cumt.edu.cn/521/list.htm": false,
        "http://xwzx.cumt.edu.cn/523/list.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".wp_article_list a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".wp_articlecontent",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".wp_articlecontent img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "矿大",
          "中国矿业大学",
          "cumt",
          "cumt.net.cn"
        ],
        "categories": [
          "中国矿业大学",
          "cumt.net.cn"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "hrbeu": {
      "info": "哈尔滨工程大学",
      "enable": true,
      "urls": {
        "http://gongxue.cn/news/ShowClass.asp?ClassID=4383": false,
        "http://gongxue.cn/news/ShowClass.asp?ClassID=4315": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".wenzhangzhengwen a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".wenzhangzhengwen",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".wenzhangzhengwen img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "哈工程",
          "哈尔滨工程大学",
          "hrbeu",
          "hrbeu.com.cn"
        ],
        "categories": [
          "哈尔滨工程大学",
          "hrbeu.com.cn"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "sicau": {
      "info": "四川农业大学",
      "enable": true,
      "urls": {
        "https://news.sicau.edu.cn/syzd.htm": true,
        "https://news.sicau.edu.cn/syxw.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".mar_10 a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "h1::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".v_news_content",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".v_news_content img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "川农大",
          "四川农业大学",
          "sicau",
          "sicau.com.cn"
        ],
        "categories": [
          "四川农业大学",
          "sicau.com.cn"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "utibet": {
      "info": "西藏大学",
      "enable": false,
      "urls": {
        "http://www.utibet.edu.cn/news/article_3_5_0.html": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": "#right table a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "xpath",
          "selstr": "//*[@id=\"right\"]/div[2]/table/tr[1]/td/div[2]//text()",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "xpath",
          "selstr": "//*[@id=\"right\"]/div[2]/div",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "xpath",
          "selstr": "//*[@id=\"right\"]/div[2]/div//img/@src",
          "seltype": "extract"
        },
        "tags": [
          "藏大",
          "西藏大学",
          "utibet",
          "utibet.com.cn"
        ],
        "categories": [
          "西藏大学",
          "utibet.com.cn"
        ],
        "posts": [
          "api_nf"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "tijmu": {
      "info": "天津医科大学",
      "enable": true,
      "urls": {
        "http://www.tmu.edu.cn/132/list.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": "#newslist table a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".Article_Content",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".Article_Content img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "天津医大",
          "天津医科大学",
          "tijmu",
          "tijmu.com.cn",
          "tijmu.cc"
        ],
        "categories": [
          "天津医科大学",
          "tijmu.com.cn",
          "tijmu.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "tjutcm": {
      "info": "天津中医药大学",
      "enable": true,
      "urls": {
        "http://news13.tjutcm.edu.cn/erji.jsp?urltype=tree.TreeTempUrl&wbtreeid=1526": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": "a[class=\"c42389\"]::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": ".titlestyle42391::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": "#vsb_newscontent",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": "#vsb_newscontent img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "天中",
          "天津中医药大学",
          "tjutcm",
          "tjutcm.com.cn"
        ],
        "categories": [
          "天津中医药大学",
          "tjutcm.com.cn"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "shutcm": {
      "info": "上海中医药大学",
      "enable": true,
      "urls": {
        "https://www.shutcm.edu.cn/221/list.htm": true,
        "http://www.shutcm.edu.cn/xykx/list.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".column-news-title a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".wp_articlecontent",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".wp_articlecontent img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "上中医",
          "上海中医药大学",
          "shutcm",
          "shutcm.com.cn"
        ],
        "categories": [
          "上海中医药大学",
          "shutcm.com.cn"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "nwsuaf": {
      "info": "西北农林科技大学",
      "enable": true,
      "urls": {
        "https://news.nwsuaf.edu.cn/xnxw/index.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".lb01 a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": "title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": "#work",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": "#work img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "西农",
          "西北农林",
          "西北农林科技大学",
          "nwsuaf",
          "nwsuaf.cc"
        ],
        "categories": [
          "西北农林科技大学",
          "nwsuaf.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "shsmu": {
      "info": "上海交通大学医学院",
      "enable": true,
      "urls": {
        "https://www.shsmu.edu.cn/news/xyyw.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": "#s65872874_content table a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": ".mod_font08.mod_bold.mod_align::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": "#article_content",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": "#article_content img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "上海交大医学院",
          "上海交通大学医学院",
          "shsmu",
          "shsmu.cc"
        ],
        "categories": [
          "上海交通大学医学院",
          "shsmu.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "swjtu": {
      "info": "西南交通大学",
      "enable": true,
      "urls": {
        "https://news.swjtu.edu.cn/showlist-82.shtml": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".detail__list__1.body__left__list a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": ".article h1::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".article .content14",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".article .content14 img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "西南交大",
          "西南交通大学",
          "swjtu",
          "swjtu.cc"
        ],
        "categories": [
          "西南交通大学",
          "swjtu.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "njust": {
      "info": "南京理工大学",
      "enable": true,
      "urls": {
        "http://zs.njust.edu.cn/zhywx/list.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": ".wp_article_list a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": ".arti_title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".wp_articlecontent",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".wp_articlecontent img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "南理工",
          "南京理工大学",
          "njust",
          "njust.cc"
        ],
        "categories": [
          "南京理工大学",
          "njust.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    },
    "sufe": {
      "info": "上海财经大学",
      "enable": true,
      "urls": {
        "http://news.sufe.edu.cn/179/list.htm": true
      },
      "crawls": {
        "newslist": {
          "sel": "css",
          "selstr": "#wp_news_w69 a::attr(href)",
          "seltype": "extract"
        },
        "title": {
          "sel": "css",
          "selstr": ".arti-title::text",
          "seltype": "extract_first"
        },
        "content": {
          "sel": "css",
          "selstr": ".wp_articlecontent",
          "seltype": "extract_first"
        },
        "imgs": {
          "sel": "css",
          "selstr": ".wp_articlecontent img::attr(src)",
          "seltype": "extract"
        },
        "tags": [
          "上财",
          "上海财经大学",
          "sufe",
          "sufe.cc"
        ],
        "categories": [
          "上海财经大学",
          "sufe.cc"
        ]
      },
      "posts": [
        "api_nf"
      ]
    }
  }

```



