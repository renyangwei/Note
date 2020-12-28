# C语言

C语言是一种适合用来开发操作系统的语言。

先上Hello World。

```c
#include <stdio.h>
int main(int argc, char const *argv[])
{
    /* code */
    printf("hello world!");
    return 0;
}
```

## 1.数据类型

```c
#include <stdio.h>

// 常量名和值之间用空格，不用等号，也不用写类型。
#define HELLO "hello"

int main(int argc, char const *argv[])
{
    // 常量
    printf(HELLO);

    // bool 值
    _Bool b = 0;
    printf("\nbool=%d\n", b);

    // sizeof 获得数据类型或表达式的长度
    printf("sizeof=%d\n", sizeof(char)); // 4

    // 字符
    char height = 's';
    char *s = "hello";
    printf("your height=%d\n", height);

    // 字符串
    char name[] = "hello";
    printf("say=%s\n", name);

    // if
    int a = 5;
    if (a > 0)
    {
        printf("%s","a大于0\n");
    }
    
    // switch
    switch (a)
    {
    case 1:
        printf("hahah\n");
        break;
    case 2:
        printf("eee");
    }

    // for
    // 数组越界访问居然不报错
    int arr[a];
    for (int i = 0; i < a; i++)
    {
        arr[i] = i;
    }
    for (int i = 0; i <= a; i++)
    {
        printf("%d\n", arr[i]);    
    }
    
    return 0;
}
```

**变量类型**

1.自动变量

函数中的局部变量,都是动态地分配存储空间的,数据存储在动态存储区中。
在调用该函数时系统会给它们分配存储空间,在函数调用结束时就自动释放这些存储空间。这类局部变量称为自动变量。

```c
int fun(int a)
{
    auto int b,c=3; /*定义 b,c 为自动变量*/
}
```

执行完 fun()函数后,自动释放 a、b、c 所占的存储单元。 

2.全局变量

作用域为从变量定义处开始,到本程序文件的末尾。

extern int i; //声明，不是定义

3.静态变量

用static修饰

4.寄存器变量

为提高效率,C 语言允许将局部变量的值存放在 CPU 的寄存器中,这种变量叫做寄存器变量,用关键字 register 声明。


## 2.字符串操作、函数等



## 3.导入第三方库

