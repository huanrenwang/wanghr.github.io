---
lyout: post
title: linux 忘记root密码处理
categories: linux
description: linux 忘记密码处理
keyword: root密码修改
---

# CentOS忘记root密码的处理方式

## 具体步骤如下
- 进入启动页面
- 按"e"进入编辑页面
- 寻找以Linux16开头 在行末尾添加 init=/bin/sh
- 输入 init=/bin/sh 后按Ctrl+x 进入单用户模式
- mount -o remount, rw /
- 输入passwd 按Enter
- 输入新密码
- touch /.autorelabel
- 输入exec /sbin/init 按Enter 系统开始重启