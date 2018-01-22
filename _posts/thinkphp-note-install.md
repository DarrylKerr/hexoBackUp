---
title: ThinkPHP5.0学习笔记--【安装篇】
date: 2016-01-09
categories: work
tags: ThinkPHP5.0学习笔记
---
## 环境要求

`ThinkPHP5.0`环境要求如下:

> `PHP >= 5.4.0`
> `PDO PHP EXtension`
> `MBstring PHP Extension`
> `CURL PHP Extension`

<!--more-->
## 安装方式

安装方式有三种：`官网下载安装`、`Composer安装` 及 `Git安装`，推荐采用Git安装的方式，因为官网下载不一定是最新版本，而万恶的`Composer`速度慢的要死。

ThinkPHP5.0可以拆分为多个仓库，主要包括有：

+ 应用项目：`https://github.com/top-think/think`
+ 核心框架：`https://github.com/top-think/framework`

当然，因为众所周知的原因，gayhub的速度可能比较慢，除了搭梯子之外，你也可以考虑使用国内的Git仓库：

>码云

+ 应用项目：`https://git.oschina.net/liu21st/thinkphp5.git`
+ 核心框架：`https://git.oschina.net/liu21st/framework.git`

>coding

+ 应用项目：`https://git.coding.net/liu21st/thinkphp5.git`
+ 核心框架：`https://git.coding.net/liu21st/framework.git`

## 安装过程

首先克隆下载应用项目仓库
``` bash
$ git clone https://github.com/top-think/think thinkphp5
```

然后切换到`thinkphp5`目录下，再克隆核心框架仓库
``` bash
$ cd thinkphp5
$ git clone https://github.com/top-think/framework thinkphp
```
两个仓库克隆完之后，就完成了ThinkPHP5.0的下载安装,如果需要升级核心框架，需要切到thinkphp目录下，然后执行:
``` bash
$ git pull https://github.com/top-think/framework
```
到这里所有的安装工作就完成了，接下来在浏览器验证是否安装成功，在浏览器输入地址：
``` bash
http://localhost/thinkphp5/public/
```
如果浏览器输出:

![ThinkPHP5.0安装记录](https://box.kancloud.cn/2016-03-11_56e274a2376df.png)

恭喜你，已经安装成功!

`需要注意的是，mac或者Linux环境下要确保runtime目录可写`