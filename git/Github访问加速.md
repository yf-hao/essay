由于某些原因，国内访问Github会异常缓慢，在clone仓库时甚至只有10k以下的速度，下载半天有时还会失败需要从头再来，甚是让人恼火。 
本文介绍通过修改系统hosts文件的办法，绕过国内dns解析，直接访问GitHub的CDN节点，从而达到加速的目的。不需要科学上网，也不需要海外的服务器辅助。

## 1.获取GitHub官方CDN地址
打开: https://www.ipaddress.com/

查询以下三个链接的DNS解析地址 
1. github.com 
2. assets-cdn.github.com 
3. github.global.ssl.fastly.net

![](https://i.loli.net/2019/02/20/5c6cace840bbe.png)

记录下查询到的IP地址。

## 2.修改系统Hosts文件
打开系统hosts文件(需管理员权限)。 
路径：C:\Windows\System32\drivers\etc

在末尾添加三行记录并保存。(需管理员权限，注意IP地址与域名间需留有空格)
```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#   127.0.0.1       localhost
#   ::1             localhost

  192.30.253.112     github.com

  151.101.72.133    assets-cdn.github.com

  151.101.193.194    github.global.ssl.fastly.net
```
## 3.刷新系统DNS缓存
Windows+X 打开系统命令行（管理员身份）或powershell
运行 ipconfig /flushdns 手动刷新系统DNS缓存。
