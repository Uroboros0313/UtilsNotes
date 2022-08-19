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

