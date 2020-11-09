- [shell脚本](#shell%e8%84%9a%e6%9c%ac)
  - [指定解析器](#%e6%8c%87%e5%ae%9a%e8%a7%a3%e6%9e%90%e5%99%a8)
  - [输出](#%e8%be%93%e5%87%ba)
  - [变量](#%e5%8f%98%e9%87%8f)
    - [环境变量](#%e7%8e%af%e5%a2%83%e5%8f%98%e9%87%8f)
    - [用户变量](#%e7%94%a8%e6%88%b7%e5%8f%98%e9%87%8f)
  - [命令替换](#%e5%91%bd%e4%bb%a4%e6%9b%bf%e6%8d%a2)
  - [重定向](#%e9%87%8d%e5%ae%9a%e5%90%91)
    - [输出重定向](#%e8%be%93%e5%87%ba%e9%87%8d%e5%ae%9a%e5%90%91)
    - [重定向输入](#%e9%87%8d%e5%ae%9a%e5%90%91%e8%be%93%e5%85%a5)
    - [重定向错误](#%e9%87%8d%e5%ae%9a%e5%90%91%e9%94%99%e8%af%af)
  - [管道](#%e7%ae%a1%e9%81%93)
  - [退出脚本](#%e9%80%80%e5%87%ba%e8%84%9a%e6%9c%ac)
    - [退出状态码](#%e9%80%80%e5%87%ba%e7%8a%b6%e6%80%81%e7%a0%81)
    - [退出命令](#%e9%80%80%e5%87%ba%e5%91%bd%e4%bb%a4)
  - [结构化命令](#%e7%bb%93%e6%9e%84%e5%8c%96%e5%91%bd%e4%bb%a4)
    - [if-then](#if-then)
    - [if-then-else](#if-then-else)
    - [if-then-else if](#if-then-else-if)
  - [对比](#%e5%af%b9%e6%af%94)
    - [数值对比](#%e6%95%b0%e5%80%bc%e5%af%b9%e6%af%94)
    - [字符串比较](#%e5%ad%97%e7%ac%a6%e4%b8%b2%e6%af%94%e8%be%83)
    - [文件比较](#%e6%96%87%e4%bb%b6%e6%af%94%e8%be%83)
  - [逻辑运算符](#%e9%80%bb%e8%be%91%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [循环](#%e5%be%aa%e7%8e%af)
    - [for命令](#for%e5%91%bd%e4%bb%a4)
  - [命令行参数](#%e5%91%bd%e4%bb%a4%e8%a1%8c%e5%8f%82%e6%95%b0)
    - [位置参数](#%e4%bd%8d%e7%bd%ae%e5%8f%82%e6%95%b0)
    - [特殊参数变量](#%e7%89%b9%e6%ae%8a%e5%8f%82%e6%95%b0%e5%8f%98%e9%87%8f)
    - [移动变量](#%e7%a7%bb%e5%8a%a8%e5%8f%98%e9%87%8f)
    - [getopts](#getopts)
  - [用户输入](#%e7%94%a8%e6%88%b7%e8%be%93%e5%85%a5)
  - [后台运行程序](#%e5%90%8e%e5%8f%b0%e8%bf%90%e8%a1%8c%e7%a8%8b%e5%ba%8f)
  - [分割字符串](#%e5%88%86%e5%89%b2%e5%ad%97%e7%ac%a6%e4%b8%b2)


# shell脚本

## 指定解析器

脚本第一行输入

    #!/bin/bash

表示指定`bash`作为解析器

## 输出

    $ echo 'This is "Test"'
    This is "Test"

字符串可以用双引号或者单引号其中一种表示字符串，那么另一种就表示引号

    $ echo "This is 'Test'"
    This is 'Test'

## 变量

### 环境变量

可以用`set`查看，然后使用环境变量

```bash
#!/bin/bash
echo "UserId:$UID"
```

### 用户变量

定义变量不要`$`，但是使用时需要

```bash
#!/bin/bash
value=1
echo "value = $value"
```

## 命令替换

即将命令输出赋值给变量，有两种方式：

- 反引号 `
- `$()`

举例：

```
v1=`date`
v2=$(date)
echo $v1
echo $v2
```

## 重定向

### 输出重定向

使用大于号`>`

    command > file

举例：

1.将`date`命令的结果保存到文件中

```
$ date > date.txt
$ cat date.txt 
2019年 3月 9日 星期六 22时12分57秒 CST
```

2.将`who`命令的结果追加到*date.txt*

```
$ who >> date.txt 
$ decompile cat date.txt 
2019年 3月 9日 星期六 22时12分57秒 CST
renyangwei console  Mar  9 11:37 
renyangwei ttys001  Mar  9 17:11 
```

### 重定向输入

使用小于号`<`

    command < file

举例：

1.统计文件的行数、词数和字节数

```
$ wc < date.txt
   3      17     116
```

解释：3行、17个单词和116个字节

> 当然也是可以直接输入 `wc date.txt`

2.同理，两个小于号 `<<`表示追加

### 重定向错误

在大于号 `>` 之前加 `2`

    $ ./test 2> 123.log

## 管道

将一个命令的输出作为另一个命令的输入

    command1 | command2

举例：

```
$ cat -n date.txt | grep tt
3	renyangwei ttys001  Mar  9 17:11
```

## 退出脚本

### 退出状态码

shell中运行每个命令都使用**退出状态码**，一个0~255的整数，用`$?`表示。`0`表示执行成功，非零则执行失败。

举例：

```
$ date
2019年 3月10日 星期日 22时05分56秒 CST
$ echo $?
0
```

### 退出命令

默认情况下，shell脚本会议脚本中最后一个命令的退出状态码退出

    exit

也可以自定义状态码

    exit 2

## 结构化命令

### if-then

如果`if`后的命令的状态码是`0`，则执行下一个命令，否则跳过。

    if [command]
    then
        [command]
    fi

举例：

```bash
#!/bin/bash
if pwd;then
    echo "It works"
fi

$ ./test.sh
/Users/renyangwei/Documents/package/workdir/nnzdxsgaz/build/dyb/decompile
It works
```

> 例子中是另一种写法

### if-then-else

    if [command];then
        [command]
    else
        [command]
    fi

和上面的用法相同

### if-then-else if

    if [command];then
        [command]
    elif [command];then
        [command]
    fi

同理，省略

## 对比

包括数值、字符串和文件对比

### 数值对比

| 比较 | 描述 |
|---|---|
| n1 -eq n2 | n1 == n2 |
| n1 -ge n2 | n1 >= n2 |
| n1 -gt n2 | n1 > n2  |
| n1 -le n2 | n1 <= n2 |
| n1 -lt n2 | n1 < n2  |
| n1 -ne n2 | n1 != n2 |

举例：

```bash
#!/bin/bash
v1=10
v2=5
if [ $v1 -eq 2 ];then
    echo "$v1 == 2"
elif [ $v2 -gt 3 ];then
    echo "$v2 > 3"
fi
```
> bash shell只能处理整数

### 字符串比较

| 比较 | 描述 |
|---|---|
| str1 = str2 | str1 等于 str2 |
| str1 != str2 | str1 不等于 str2 |
| str1 < str2 | str1 小于 str2 |
| str1 > str2 | str1 大于 str2 |
| -n str1 | str1的长度是否非0 |
| -z str1 | str1的长度是否为0 |

举例：

1.字符串相等性

```bash
#!/bin/bash
v1="ren"
v2=$USER
v3="renyangwei"
if [[ $v1 == $v2 ]];then
    echo "$v1 == $v2"
else
    echo "$v1 != $v2"
fi

if [[ $v2 == $v3 ]];then
    echo "$v2 == $v3"
fi
```

> 比较相等时会区分大小写，需要增加一对大括号。

2.字符串顺序

大于和小于号要转义;大写字符比小写字母大，但是`sort`命令是小写字母在前。所谓大小就是按字母排序。

```bash
#!/bin/bash
v1="ren"
v2=$USER
v3="renyangwei"
if [ $v1 \< $v2 ];then
    echo "$v1 < $v2"
fi
if [ "ab" \< "b" ];then
    echo "ab < b"
fi
```

### 文件比较

| 比较 | 描述 |
|---|---|
| -d file | file是否存在并是否是目录 |
| -e file | file是否存在 |
| -f file | file是否存在并是否是文件 |
| -r file | file是否存在并是否可读 |
| -s file | file是否存在并是否非空 |
| -w file | file是否存在并是否可写 |
| -x file | file是否存在并是否可执行 |
| -O file | file是否存在并属于当前用户 |
| -G file | file是否存在并默认组与当前用户相同 |
| file1 -nt file2 | file1是否比file2新 |
| file1 -ot file2 | file1是否比file2旧 |

举例：

1.检查目录

```bash
#!/bin/bash
dir=/Users/renyangwei/Documents/ShellScript
if [ -d $dir ];then
    echo "$dir exist"
fi
```

2.检查对象是否存在(包括目录和文件)

```bash
#!/bin/bash
if [ -e $HOME ];then
    echo "$HOME exist"
fi
```

3.检查文件是否存在

```bash
#!/bin/bash
file=`pwd`/a.txt
if [ -f $file ];then
    echo "$file exist"
else
    echo "$file not exist"
fi
```

4.检查是否可读

```bash
#!/bin/bash
file=`pwd`/a.txt
touch file
if [ -r file ];then
    echo "$file can read"
fi
```

5.检查空文件

```bash
#!/bin/bash
file=`pwd`/a.txt
touch $file
if [ -s $file ];then
    echo "$file has content"
else
    echo "$file is empty"
fi
```

## 逻辑运算符

    [ condition1 ] && [ condition2 ]
    [ condition1 ] || [ condition2 ]

举例：

 ```bash
#!/bin/bash
# 逻辑运算符
#
file=`pwd`/a.txt
touch $file
if [ -s $file ] && [ -r $file ];then
    echo "$file nice"
else
    echo "$file is empty"
fi
 ```
## 循环

### for命令

    for var in list
    do
        commands
    done

举例：

```bash
#!/bin/bash
# for命令
#
for i in a b c d
do
    echo "i=$i"
done
```

```bash
ls=`ls`
for i in $ls;do
    echo "i=$i"
done
```

```bash
for (( i=1; i<=10; i++));do
    echo "i = $i"
done
```

```bash
#!/bin/bash
# for
# IFS 表示 for 要判断的是哪个标点，默认是空格
IFS.OLD=$IFS
IFS=$`\n`
for entry in `cat /etc/passwd`;do
    echo "values in $entry -"
    IFS=:
    for value in $entry;do
        echo "  $value"
    done
done
```

> 重定向for循环输出，在`done` 后加类似 `> [file]` 这样的重定向语句。

## 命令行参数

### 位置参数

- `$0`：程序名
- `$1`：第一个参数
- `$2`：第二个参数
- 以此类推，直到第九个
- `${10}`：第十个参数

### 特殊参数变量

- `$#`：参数个数
- `$*`：所有参数，作为一个整体，for循环不管用
- `$@`：所有参数，作为单个单词，可以用for循环遍历

### 移动变量

- `shift`：将所有参数移动一个位置

### getopts

    getopts optstring variable

有效的选项字母都会列在 *optstring* 中，如果有参数值就加一个 `:` 号，如果要去掉错误消息就在 *otpstring* 前加 `:` 。

- `OPTARG`：保存参数值
- `OPTIND`：保存正在处理的参数位置

```bash
#!/bin/bash
# 处理选项
# getopts
#
while getopts :ab:c opt;do
    case "$opt" in 
        a) echo "Found the -a option";;
        b) echo "Found the -b option $OPTARG";;
        c) echo "Found the -c option";;
        *) echo "Unknow option: $opt"
    esac
done
```

```bash
$ ./test.sh -a -b "ren yangwei" -c -f
Found the -a option
Found the -b option ren yangwei
Found the -c option
Unknow option: ?
```

> 如果参数没有空格就可以不写引号

## 用户输入

    read

从标准输入（键盘）或另一个文件描述符中接受输入。

举例：

1.获取输入

```bash
#!/bin/bash
# 用户输入
# read
#
echo "input your name:"
read name
echo "hello $name"
```

2.提示符

```bash
#!/bin/bash
# 用户输入
# read
#
read -p "input your name:" name
echo "hello $name"
```

## 后台运行程序

    nohup ./test.sh &

nohup和&的区别

- `nohup`: 使命令永久的执行下去，注意并**没有后台运行**的功能，终端不能再输入
- `&`：后台运行

## 分割字符串

举例：fltx.apk 中的fltx字符

    dirName=`echo $apkFile|cut -d"." -f1`