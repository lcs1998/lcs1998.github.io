---

layout:     post
title:      cachestat 安装文档
subtitle:   测试cache命中率
date:       2019-04-11
author:     Lcs
header-img: img/post-bg-ios9-web.jpeg
catalog: true
tags:
    - cachestat
    - ubuntu
    - terminal
---

# cachestat 安装文档

>安装环境：ubuntu18.04

## 安装步骤

### 1. 打开命令行，输入以下命令

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4052245BD4284CDD
echo "deb https://repo.iovisor.org/apt/xenial xenial main" | sudo tee /etc/apt/sources.list.d/iovisor.list
sudo apt-get update
sudo apt-get install -y bcc-tools libbcc-examples linux-headers-$(uname -r)
```

### 2. 查找 bcc 安装目录

```
whereis bcc
```

![1554778901499](D:/Learn-File/大三/大三春季学期/计算机系统结构/研讨/cachestat 安装文档.assets/1554778901499.png)

```
cd usr/share/bcc/tools
```

### 3. 运行cachestat

```
 sudo ./cachestat
```

![1554779035177](D:/Learn-File/大三/大三春季学期/计算机系统结构/研讨//cachestat 安装文档.assets/1554779035177.png)

## 原理解析

