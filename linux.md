> # SSH连接linux

1. 用户名/密码登录

`ssh <username>@<IP address or domain name>`

2. 密钥登录

```
icacls <已下载的与实例关联的私钥文件的路径> /grant <Windows 系统用户帐户>:F
icacls <已下载的与实例关联的私钥文件的路径> /inheritancelevel:r
ssh -i <已下载的与实例关联的私钥文件的路径> <username>@<IP address or domain name>

```
# Vim

## 删除
```
d1G	删除光标所在到第一行的所有数据
dG	删除光标所在到最后一行的所有数据
```

> # 文件管理

## 查看Linux文件用户权限

`ll` 或者 `ls –l` 命令来显示一个文件的属性以及文件所属的用户和组

示例:
```
ls -l
total 64
<文件类型><属主权限><属组权限><其他用户权限>  - <属主名><属组名>
dr-xr-xr-x   2 root root 4096 Dec 14  2012 bin
dr-xr-xr-x   4 root root 4096 Apr 19  2012 boot
```

- 文件类型

`d`目录；`-`文件；`l`链接文档(link file)；`b`装置文件里面的可供储存的接口设备(可随机存取装置)；`c`装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。

- 权限类型

`r`可读；`w`可写；`x`可执行；`-`无

## 修改文件权限

### chgrp：更改文件属组

`chgrp [-R] 属组名 文件名`

`-R`：递归更改文件属组。

### chown：更改文件属主，也可以同时更改文件属组

```
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```

### chmod：更改文件9个属性

#### 修改权限分数

各权限的分数对照表如下：
- r:4
- w:2
- x:1

每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为： -rwxrwx--- 分数则是：
```
owner = rwx = 4+2+1 = 7
group = rwx = 4+2+1 = 7
others= --- = 0+0+0 = 0
```


即设定权限的变更时，该文件的权限数字就是 770。

`chmod [-R] xyz 文件或目录`

`xyz `: 就是刚刚提到的数字类型的权限属性，为 rwx 属性数值的相加。
```
[root]# ls -al .bashrc
-rw-r--r--  1 root root 395 Jul  4 11:45 .bashrc
[root]# chmod 777 .bashrc
[root]# ls -al .bashrc
-rwxrwxrwx  1 root root 395 Jul  4 11:45 .bashrc
```

#### 符号类型改变文件权限

```
user：用户
group：组
others：其他
```
使用`u, g, o`来代表三种身份的权限。

`a `则代表 all，即全部的身份

```
chmod		u	+(加入)	r	文件或目录
		g	-(除去)	w
		o	=(设定)	x
		a					
```

```
#  touch test1    // 创建 test1 文件
# ls -al test1    // 查看 test1 默认权限
-rw-r--r-- 1 root root 0 Nov 15 10:32 test1
# chmod u=rwx,g=rx,o=r  test1    // 修改 test1 权限
# ls -al test1
-rwxr-xr-- 1 root root 0 Nov 15 10:32 test1
```

去掉全部人的可执行权限，则：
```
#  chmod  a-x test1
# ls -al test1
-rw-r--r-- 1 root root 0 Nov 15 10:32 test1
```

> # SHELL

## 第一个shell脚本

```
#!/bin/bash //#!约定标记，告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。
echo "Hello World !" //echo 命令用于向窗口输出文本。
```

### 运行shell的两种方式

#### 作为可执行程序

将上面的代码保存为`test.sh`，并`cd`到相应目录：
```
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```

#### 作为解释器参数

即直接运行解释器，其参数就是 shell 脚本的文件名，如：
```
/bin/sh test.sh
/bin/php test.php

//这种方式运行的脚本，不需要在第一行指定解释器信息
```

## shell 变量

1. 定义变量

定义变量时，变量名不加美元符号(**变量名和等号之间不能有空格**)
`your_name="uroboros"`

2. 使用变量

使用一个定义过的变量，只要在变量名前面加美元符号即可
```
echo $your_name
echo ${your_name}
```
变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如：

```
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

3. 只读变量

`readonly myUrl \\myUrl的值不能改变`

### shell字符串

1. **单引号字符串** 

str='this i`s a string'`

单引号字符串的限制：

- 单引号里的字符会原样输出，字符串中的变量是无效的；

- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

2. **双引号字符串**

```
your_name="uroboros"
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

输出结果：

`Hello, I know you are "uroboros"!` 

- 双引号里可以有变量
- 双引号里可以出现转义字符

