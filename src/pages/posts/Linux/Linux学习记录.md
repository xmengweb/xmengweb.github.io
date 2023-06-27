---
layout: "@layouts/MarkdownPost.astro"
title: "Linux学习笔记"
pubDate: 2022-09-01
description: "笔记总结"
author: "XMeng"
cover:
  url: "https://miro.medium.com/v2/resize:fit:640/format:webp/1*M8WP_RFKNaqRLSujd9Ik3w.png"
  alt: "cover"
tags: ["Linux"]
theme: "light"
featured: true
---

# Linux 学习记录

## 一、获取帮助信息

### 1.1 使用`man`获取帮助信息

例如： 查看 mkdir 的帮助信息

```
[root@iZubwqvlhz9096Z ~]# man mkdir
```

![image-20220612000732861](https://cugdemo.oss-cn-hangzhou.aliyuncs.com/image-20220612000732861.png)

![](https://cugdemo.oss-cn-hangzhou.aliyuncs.com/202206120006022.png)

### 1.2 使用`help`获取 shell 内置命令帮助

例如:

```
[root@iZubwqvlhz9096Z ~]# cd --help
//或者
[root@iZubwqvlhz9096Z ~]# help cd
```

## 二、常用快捷键

| 常用快捷键    | 功能                                  |
| :------------ | ------------------------------------- |
| ctrl + c      | 停止进程                              |
| ctrl+l        | 清屏，等同于 clear；彻底清屏是：reset |
| 上下键        | 查找执行过的命令                      |
| 善于用 tab 键 | 提示(更重要的是可以防止敲错)          |

## 三、文件操作

### 3.1pwd

> 显示当前工作目录的绝对路径

```
[root@iZubwqvlhz9096Z ~]# pwd
/root
```

### 3.2ls

> 列出文件目录的内容

语法:

```
ls [选项] [目录或者文件]
```

选项说明:

| 选项 | 功能                                                         |
| ---- | ------------------------------------------------------------ |
| -a   | 全部的文件，连同隐藏档( 开头为 . 的文件) 一起列出来(常用)    |
| -l   | 长数据串列出，包含文件的属性与权限等等数据；(常用)等价于“ll” |

例如: 查看当前目录的所有内容信息

```
[root@iZubwqvlhz9096Z ~]# ls -la
总用量 48
dr-xr-x---.  6 root root  245 5月  25 00:06 .
dr-xr-xr-x. 17 root root  244 5月  24 23:12 ..
-rw-------   1 root root 1908 6月  12 00:34 .bash_history
-rw-r--r--.  1 root root   18 5月  11 2019 .bash_logout
-rw-r--r--.  1 root root  176 5月  11 2019 .bash_profile
-rw-r--r--.  1 root root  176 5月  11 2019 .bashrc
drwx------   3 root root   17 9月  14 2020 .cache
drwx------   3 root root   20 5月  24 23:13 .config
-rw-r--r--.  1 root root  100 5月  11 2019 .cshrc
-rw-------   1 root root  412 5月  25 00:04 .mysql_history
drwxr-xr-x   2 root root   22 9月  14 2020 .pip
-rw-r--r--   1 root root  206 5月  24 22:58 .pydistutils.cfg
drwx------   2 root root   29 9月  14 2020 .ssh
-rw-r--r--.  1 root root  129 5月  11 2019 .tcshrc
-rw-------   1 root root 9494 5月  25 00:06 .viminfo
-rw-r--r--   1 root root  168 5月  24 23:26 .wget-hsts
//文件类型与权限  链接数 文件属主 文件属组 文件大小用byte来表示 建立或最近修改的时间 名字
```

### 3.3cd

> 切换目录

| 参数        | 功能                                 |
| ----------- | ------------------------------------ |
| cd 绝对路径 | 切换路径                             |
| cd 相对路径 | 切换路径                             |
| cd ~或者 cd | 回到自己的家目录                     |
| cd -        | 回到上一次所在目录                   |
| cd ..       | 回到当前目录的上一级目录             |
| cd -P       | 跳转到实际物理路径，而非快捷方式路径 |

```
(1) 使用绝对路径切换到 root 目录

[root@hadoop101 ~]# cd /root/

（2）使用相对路径切换到“公共的”目录

[root@hadoop101 ~]# cd 公共的/

（3）表示回到自己的家目录，亦即是 /root 这个目录

[root@hadoop101 公共的]# cd ~

（4）cd- 回到上一次所在目录

[root@hadoop101 ~]# cd -

（5）表示回到当前目录的上一级目录，亦即是 “/root/公共的”的上一级目录的意思；

[root@hadoop101 公共的]# cd ..
```

### 3.4mkdir
