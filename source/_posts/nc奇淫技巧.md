---
title: nc奇淫技巧
toc: false
date: 2024-07-02 14:28:39
categories:
tags:
keywords:
top:
cover:
summary:
password:
mathjax:
---


# 扫描端口

```bash
nc -zv 127.0.0.1 80-65535 2>&1 | grep "succeeded"

```


# 传输文件

```bash

# 接收方监听端口并将文件内容重定向到文件中
nc -l 127.0.0.1 1234 > filename

# 发送方将文件重定向到服务端监听的端口中
nc 127.0.0.1 1234 < filename
```
