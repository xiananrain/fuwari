---
title: Alpine关闭ipv6
published: 2025-10-07
description: This is the first post of my new Astro blog.
tags: [alpine]
category: Front-end
draft: false
---、


```bash

echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf

```
\
立即执行
```bash
sysctl -p
```
\
验证结果
```bash
cat /proc/sys/net/ipv6/conf/all/disable_ipv6
```
\
若输出 1，说明 IPv6 已成功关闭。

设置每次开机执行
```bash
echo '#!/bin/sh' > /etc/local.d/sysctl.start
echo 'sysctl -p' >> /etc/local.d/sysctl.start
chmod +x /etc/local.d/sysctl.start
rc-update add local default
```
\
手动验证是否正常运行
```bash
/etc/init.d/sysctl-load start
```
