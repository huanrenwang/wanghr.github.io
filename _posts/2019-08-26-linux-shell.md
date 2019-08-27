---
lyout: post
title: linux shell 命令
categories: linux
description: shell 编程
keyword: shell 命令编程
---

# linux shell命令的学习和使用

## shell的基本格式

*#!/bin/bash*  那种shell脚本解释器。

## linux 中的shell解释器有哪些

* 在linux中有Bourne shell(/usr/bin/sh或者/bin/sh)

* Bourne Again Shell (/bin/bash)

* C shell (/usr/bin/csh)

* ...

shell开头都要加上解释器的类型

## shell脚本的基本格式

```
#!/bin/bash
echo "Hello World !"
```
由类型解释器语法与脚本语法两部分组成,shell脚本必须指定解释器类型，要不脚本容易报错。

## shell 变量

类似于动态语言，所以不用提前定义变量的类型，但是变量名必须由字母、数字、下划线组成，其他任何都是多余的。

* 变量的赋值: a=123 切记等号左右两边不能由空格

* 变量的使用。有两种方式：1) $a、${a}

* 只读变量：readonly a

* 删除变量：unset a  这个时候在使用变量就使用不了了，例如echo $a 则输出为空白。


