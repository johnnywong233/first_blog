## 行首#!/bin/sh
是指此脚本使用/bin/sh来解释执行，#!是特殊的表示符，解释此脚本的shell的路径。

$bash $表示系统提示符，$ 表示此用户为普通用户，超级用户的提示符是＃。

bash是shell的一种，最常用。

$bash的意思是执行一个子shell，此子shell为bash。

在每个脚本的开头都使用"#!"，这意味着告诉你的系统这个文件的执行需要指定一个解释器。#!实际上是一个2字节的魔法数字，这是指定一个文件类型的特殊标记，换句话说，在这种情况下指的就是一个可执行的脚本(键入man magic来获得关于这个迷人话题的更多详细信息)。

在#!之后接着是一个路径名，指定一个解释脚本中命令的程序。这个程序可以是shell。程序语言或者是任意一个通用程序。这个指定的程序从头开始解释并且执行脚本中的命令(从#!行下边的一行开始)。如:
 
```
1.#!/bin/sh

2 #!/bin/bash
 
3 #!/usr/bin/perl
 
4 #!/usr/bin/tcl
 
5 #!/bin/sed -f
 
6 #!/usr/awk -f
```

注意: #!后边给出的路径名必须是正确的，否则将会出现一个错误消息，通常是 "Command not found"，这将是你运行这个脚本时所得到的唯一结果。

如果在脚本的里边还有一个#!行，那么bash将把它认为是一个一般的注释行。

## Shell脚本编写
### 注意事项
1) 开头加解释器：#!/bin/bash

2) 语法缩进，使用四个空格;多加注释说明。

3) 命名建议规则：变量名大写、局部变量小写，函数名小写，名字体现出实际作用。

4) 默认变量是全局的，在函数中变量local指定为局部变量，避免污染其他作用域。

5) 有两个命令能帮助我调试脚本：set -e 遇到执行非0时退出脚本，set-x 打印执行过程。

6) 写脚本一定先测试再到生产上。

### 1 获取随机字符串或数字
获取随机8位字符串：

方法一

```
echo $RANDOM | md5sum |cut -c 1-8
```

方法二

```
openssl rand -base64 4
```

方法三

```
cat /proc/sys/kernel/random/uuid |cut -c 1-8
```

获取随机8位数字：

方法一

```
echo $RANDOM | cksum |cut -c 1-8

```
方法二

```
openssl rand -base64 4 | cksum |cut -c 1-8
```

方法三

```
date +%N |cut -c 1-8
cksum：打印CRC效验和统计字节
```

## 2.检查服务状态
```
#!/bin/bash
PORT_C=$(ss -anu |grep -c 123)
PS_C=$(ps -ef|grep ntpd |grep -vc grep)
if [$PORT_C -eq 0 -o $PS_C -eq 0];
then
echo "内容" |mail -s "" dst@example.com
fi
```