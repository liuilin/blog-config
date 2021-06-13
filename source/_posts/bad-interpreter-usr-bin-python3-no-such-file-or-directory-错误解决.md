---
title: 'bad interpreter: /usr/bin/python3:  no such file or directory 错误解决 '
date: 2021-06-10 13:28:30
tags: Python
---
## 分析

查阅资料后发现原因是 python 的符号链接 symbolic links 问题。我自己安装 / 卸载 python 后把环境搞出问题了

## 解决

```bash

ll /usr/bin/python*

sudo unlink /usr/bin/python3

sudo ln -s /usr/bin/python3.8（whereis python 安装目录） /usr/bin/python3

```
