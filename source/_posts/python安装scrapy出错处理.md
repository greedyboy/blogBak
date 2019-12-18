---
title: python安装scrapy出错处理
urlname: python-scrapy-index
tags:
  - python
  - scrapy
categories:
  - daybreak
date: 2019-04-24 11:33:40
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> python安装scrapy过程中出现错误。`from cryptography.hazmat.bindings._openssl import ffi, lib ImportError: DLL load failed: 找不到指定的程序。`记录处理过程。

<!-- more -->

### 安装使用conda进行
- 使用命令
```
conda install -c conda-forge scrapy
```
- 结果正常
```
E:\PycharmProjects\pyscrapy>conda install -c conda-forge scrapy
Collecting package metadata: done
Solving environment: done

## Package Plan ##

  environment location: E:\ProgramData\Anaconda3

  added / updated specs:
    - scrapy


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2019.3.9   |       hecc5488_0         184 KB  conda-forge
    certifi-2019.3.9           |           py37_0         149 KB  conda-forge
    conda-4.6.14               |           py37_0         2.1 MB  conda-forge
    openssl-1.1.1b             |       hfa6e2cd_2         4.8 MB  conda-forge
    scrapy-1.5.2               |           py37_0         336 KB  conda-forge
    ------------------------------------------------------------
                                           Total:         7.5 MB

The following packages will be UPDATED:

  ca-certificates    pkgs/main::ca-certificates-2019.1.23-0 --> conda-forge::ca-certificates-2019.3.9-hecc5488_0
  openssl              pkgs/main::openssl-1.1.1b-he774522_1 --> conda-forge::openssl-1.1.1b-hfa6e2cd_2

The following packages will be SUPERSEDED by a higher-priority channel:

  certifi                                         pkgs/main --> conda-forge
  conda                                           pkgs/main --> conda-forge
  scrapy                                          pkgs/main --> conda-forge


Proceed ([y]/n)? y


Downloading and Extracting Packages
ca-certificates-2019 | 184 KB    | ########################################################################### | 100%
certifi-2019.3.9     | 149 KB    | ########################################################################### | 100%
scrapy-1.5.2         | 336 KB    | ########################################################################### | 100%
conda-4.6.14         | 2.1 MB    | ########################################################################### | 100%
openssl-1.1.1b       | 4.8 MB    | ########################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```

### 创建scrapy项目出错
- 出错提示
```
E:\PycharmProjects\pyscrapy>scrapy startproject gking
Traceback (most recent call last):
  File "E:\ProgramData\Anaconda3\Scripts\scrapy-script.py", line 10, in <module>
    sys.exit(execute())
  File "E:\ProgramData\Anaconda3\lib\site-packages\scrapy\cmdline.py", line 149, in execute
    cmd.crawler_process = CrawlerProcess(settings)
  File "E:\ProgramData\Anaconda3\lib\site-packages\scrapy\crawler.py", line 252, in __init__
    log_scrapy_info(self.settings)
  File "E:\ProgramData\Anaconda3\lib\site-packages\scrapy\utils\log.py", line 149, in log_scrapy_info
    for name, version in scrapy_components_versions()
  File "E:\ProgramData\Anaconda3\lib\site-packages\scrapy\utils\versions.py", line 35, in scrapy_components_versions
    ("pyOpenSSL", _get_openssl_version()),
  File "E:\ProgramData\Anaconda3\lib\site-packages\scrapy\utils\versions.py", line 43, in _get_openssl_version
    import OpenSSL
  File "E:\ProgramData\Anaconda3\lib\site-packages\OpenSSL\__init__.py", line 8, in <module>
    from OpenSSL import crypto, SSL
  File "E:\ProgramData\Anaconda3\lib\site-packages\OpenSSL\crypto.py", line 16, in <module>
    from OpenSSL._util import (
  File "E:\ProgramData\Anaconda3\lib\site-packages\OpenSSL\_util.py", line 6, in <module>
    from cryptography.hazmat.bindings.openssl.binding import Binding
  File "E:\ProgramData\Anaconda3\lib\site-packages\cryptography\hazmat\bindings\openssl\binding.py", line 15, in <modul
e>
    from cryptography.hazmat.bindings._openssl import ffi, lib
ImportError: DLL load failed: 找不到指定的程序。

```

### 失败尝试
- 失败尝试`conda install -c conda-forge lxml`
- 失败尝试`conda install -c conda-forge openssl`

### 问题解决
- 安装代码`pip install -I cryptography`

```
E:\PycharmProjects\pyscrapy>pip install -I cryptography
Collecting cryptography
  Downloading https://files.pythonhosted.org/packages/00/39/088ba8da28dd77582219d4b77263d5aedac37c5c1c31f75859f241b9fcd
2/cryptography-2.6.1-cp37-cp37m-win_amd64.whl (1.5MB)
    100% |████████████████████████████████| 1.5MB 198kB/s
Collecting asn1crypto>=0.21.0 (from cryptography)
  Using cached https://files.pythonhosted.org/packages/ea/cd/35485615f45f30a510576f1a56d1e0a7ad7bd8ab5ed7cdc600ef7cd062
22/asn1crypto-0.24.0-py2.py3-none-any.whl
Collecting six>=1.4.1 (from cryptography)
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e
9/six-1.12.0-py2.py3-none-any.whl
Collecting cffi!=1.11.3,>=1.8 (from cryptography)
  Downloading https://files.pythonhosted.org/packages/2f/ad/9722b7752fdd88c858be57b47f41d1049b5fb0ab79caf0ab11407945c1a
7/cffi-1.12.3-cp37-cp37m-win_amd64.whl (171kB)
    100% |████████████████████████████████| 174kB 67kB/s
Collecting pycparser (from cffi!=1.11.3,>=1.8->cryptography)
Installing collected packages: asn1crypto, six, pycparser, cffi, cryptography
Successfully installed asn1crypto-0.24.0 cffi-1.12.3 cryptography-2.6.1 pycparser-2.19 six-1.12.0

E:\PycharmProjects\pyscrapy>scrapy startproject gking
New Scrapy project 'gking', using template directory 'E:\\ProgramData\\Anaconda3\\lib\\site-packages\\scrapy\\templates
\\project', created in:
    E:\PycharmProjects\pyscrapy\gking

You can start your first spider with:
    cd gking
    scrapy genspider example example.com

E:\PycharmProjects\pyscrapy>

```

### 饮水思源
- https://blog.csdn.net/tfun_zhang/article/details/83745614
- http://www.scrapyd.cn/doc/139.html