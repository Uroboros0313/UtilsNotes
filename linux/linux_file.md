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

## 创建文件

Linux touch命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。

`ls -l`可以显示档案的时间记录。

`touch [-acfm][-d<日期时间>][-r<参考文件或目录>] [-t<日期时间>][--help][--version][文件或目录…]`

```vim
a 改变档案的读取时间记录。
m 改变档案的修改时间记录。
c 假如目的档案不存在，不会建立新的档案。与 --no-create 的效果一样。
f 不使用，是为了与其他 unix 系统的相容性而保留。
r 使用参考档的时间记录，与 --file 的效果一样。
d 设定时间与日期，可以使用各种不同的格式。
t 设定档案的时间记录，格式与 date 指令相同。
--no-create 不会建立新档案。
--help 列出指令格式。
--version 列出版本讯息。
```

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

1. **修改权限分数**

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

2. **符号类型改变文件权限**

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

