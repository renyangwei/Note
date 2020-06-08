# C语言

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

## 2.字符串操作、函数等



## 3.导入第三方库

