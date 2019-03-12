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

```
#!/bin/bash
echo "UserId:$UID"
```

### 用户变量

定义变量不要`$`，但是使用时需要

```
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

```
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

```
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
| str1 = str2 | 
