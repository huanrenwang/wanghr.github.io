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


* 参数传递：向脚本传递参数$0代表文件名，1为执行脚本的第一个参数，其他以此类推。

```
1. touch test.sh
2. chmod 775 test.sh
3. #!/bin/bash
4. echo "shell 脚本传递参数实例"
5. echo "执行的文件名:$0"
6. echo "执行的第一个参数:$1"
7. echo "执行的第二个参数:$2"
8. echo "执行的第三个参数:$3"

参数传递说明：
$#：参数传递个数
$*:双引号括起来所有参数当一个参数 例如:test.sh 1 2 3 则: "1 2 3"
$$:脚本运行的当前进程id
$!:后台运行的最后一个进程id
$-:显示 shell 使用的当前选项
$@:同$*但不同点在于参数的个数，$*当1个，$@当n个
$?:显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误
```

## shell数组

在shell脚本里面只有一维数组。

* 定义数组:arry_num=(value1,value2....valuen) 
* 读取数组:${arry_num[0]}

```
#!/bin/bash
my_array[0]=A
my_array[1]=B
my_array[2]=C
my_array[3]=D

echo "数组元素个数为: ${#my_array[*]}"
echo "数组元素个数为: ${#my_array[@]}"

输出结果:
数组元素个数为: 4
数组元素个数为: 4
```
## shell 运算符

```
1.算数运算符

+	加法	`expr $a + $b` 结果为 30。
-	减法	`expr $a - $b` 结果为 -10。
*	乘法	`expr $a \* $b` 结果为  200。
/	除法	`expr $b / $a` 结果为 2。
%	取余	`expr $b % $a` 结果为 0。
=	赋值	a=$b 将把变量 b 的值赋给 a。
==	相等。用于比较两个数字，相同则返回 true。[ $a == $b ] 返回 false。
!=	不相等。用于比较两个数字，不相同则返回 true。[ $a != $b ] 返回 true

例如:
val=`expr 2+2`
echo $val

注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。乘法必须要有"\"且"\*"
左右要有空格

2.比较运算符（关系运算符）

-eq	检测两个数是否相等，相等返回 true。	[ $a -eq $b ] 返回 false。
-ne	检测两个数是否不相等，不相等返回 true。	[ $a -ne $b ] 返回 true。
-gt	检测左边的数是否大于右边的，如果是，则返回 true。[ $a -gt $b ] 返回 false。
-lt	检测左边的数是否小于右边的，如果是，则返回 true。[ $a -lt $b ] 返回 true。
-ge	检测左边的数是否大于等于右边的，如果是，则返回 true。[ $a -ge $b ] 返回 false。
-le	检测左边的数是否小于等于右边的，如果是，则返回 true。[ $a -le $b ] 返回 true。

#!/bin/bash

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b: a 大于 b"
else
   echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b: a 小于 b"
else
   echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b: a 大于或等于 b"
else
   echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
   echo "$a -le $b: a 小于或等于 b"
else
   echo "$a -le $b: a 大于 b"
fi


3.布尔运算符
!	非运算，表达式为 true 则返回 false，否则返回 true。[ ! false ] 返回 true。
-o	或运算，有一个表达式为 true 则返回 true。[ $a -lt 20 -o $b -gt 100 ] 返回 true。
-a	与运算，两个表达式都为 true 才返回 true。[ $a -lt 20 -a $b -gt 100 ] 返回 false

4.逻辑运算符
&&	逻辑的 AND	[[ $a -lt 100 && $b -gt 100 ]] 返回 false
||	逻辑的 OR	[[ $a -lt 100 || $b -gt 100 ]] 返回 true

5.字符串运算符

=	检测两个字符串是否相等，相等返回 true。[ $a = $b ] 返回 false。
!=	检测两个字符串是否相等，不相等返回 true。[ $a != $b ] 返回 true。
-z	检测字符串长度是否为0，为0返回 true。[ -z $a ] 返回 false。
-n	检测字符串长度是否为0，不为0返回 true。[ -n "$a" ] 返回 true。
$	检测字符串是否为空，不为空返回 true。[ $a ] 返回 true。

```
## shell printf

printf 使用引用文本或空格分隔的参数，外面可以在 printf 中使用格式化字符串，还可以制定字符串的宽度、左右对齐方式等。默认 printf 不会像 echo 自动添加换行符，我们可以手动添加 \n。

printf  format-string  [arguments...]

%s %c %d %f都是格式替代符

%-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。

%-4.2f 指格式化为小数，其中.2指保留2位小数

## Shell test 命令 

* 检查条件是否成立，可以进行数值，字符和文件三个方面进行测试

  -eq	等于则为真
  -ne	不等于则为真
  -gt	大于则为真
  -ge	大于等于则为真
  -lt	小于则为真
  -le	小于等于则为真

```
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi

文件测试

e 文件名	如果文件存在则为真
-r 文件名	如果文件存在且可读则为真
-w 文件名	如果文件存在且可写则为真
-x 文件名	如果文件存在且可执行则为真
-s 文件名	如果文件存在且至少有一个字符则为真
-d 文件名	如果文件存在且为目录则为真
-f 文件名	如果文件存在且为普通文件则为真
-c 文件名	如果文件存在且为字符型特殊文件则为真
-b 文件名	如果文件存在且为块特殊文件则为真

```

## shell 流程控制

* if else
```
if condition
then
    command1
    command2
fi

if else-if else

if condition1
then
    commcand1
elif condition2
then
    command2
else
    command3
fi
```

* for 
```
for var in item1 item3....
do
    command1;command2....
done

例如:

for loop in 1 2 3 4 5
do
    ehco "The value is: $loop"
done
```

* while

```
while condition
do
   command
done

例如:
#!/bin/bash
int=1
while(($int<=5>))
do
    echo $int
    let "int++"

done
```


* until 循环 ---直到条件为true时停止

```
until condition
do
    command
done

例如:

#!/bin/bash
a=0
until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```

* case

```
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2）
    command1
    command2
    ...
    commandN
    ;;
esac
```

* break ,continue 参考之前的编程语言就ok
