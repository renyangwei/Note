# 数据结构与算法

## 1.线性表

```cpp
// 线性表的顺序存储结构
// 静态分配
#include <stdio.h>

/* 存储空间初始分配量 */
#define MAXSIZE 10

typedef struct {
    int data[MAXSIZE];
    int length;
} SqList;

// 初始化
void InitList(SqList &L) {
    for (int i=0; i<MAXSIZE; i++) {
        L.data[i] = 0;
    }
    L.length = MAXSIZE;
}

// 插入元素
bool ListInsert(SqList &L, int i, int e) {
    if (i<1 || i>L.length+1)
    {
        return false;
    }
    if (L.length > MAXSIZE)
    {
        return false;
    }
    for (int j = L.length; j >= i; j--) {
        L.data[j] = L.data[j-1]; // 将第i个元素及其以后的元素后移
    }
    L.data[i-1] = e;
    L.length++;
    return true;
}

// 删除元素
bool ListDelete(SqList &L, int i, int &e) {
    if (i<1 || i>L.length)
    {
        return false;
    }
    e = L.data[i-1];  // 被删除的元素赋值给e
    for (int j = i; j <= L.length; j++)
    {
        L.data[j-1] = L.data[j];    // 将第i个位置以及以后前移
    }
    L.length++;
    return true;
}

void printList(SqList &l) {
    for (int i = 0; i < l.length; i++)
    {
        printf("list:%d,%d\n", i, l.data[i]);
    }
    printf("length=%d\n", l.length);
}

int main(int argc, char const *argv[]) {
    SqList l;
    InitList(l);
    printList(l);
    ListInsert(l, 1, 1);
    printList(l);
    ListInsert(l, 2, 2);
    printList(l);
    int e = -1;
    if (ListDelete(l, 1, e)) {
        printf("删除第1个元素成功，值为%d\n", e);
        printList(l);
    } else {
        printf("删除失败\n");
    }
    return 0;
}
```

```cpp
// 顺序表的动态分配
#include <stdio.h>
#include <stdlib.h>

#define InitSize 10

typedef struct {
    int *data;      // 动态分配数组的指针
    int MaxSize;    // 最大容量
    int length;     // 当前长度
} SqList;

// 初始化
void initList(SqList &l) {
    // 用malloc申请连续内存，data表示首地址
    l.data = (int *)malloc(InitSize*sizeof(int));
    l.length = 0;
    l.MaxSize = InitSize;
}

// 动态增加数组长度
void increaseSize(SqList &l, int len) {
    int *p = l.data;
    l.data = (int *)malloc((l.MaxSize+len)*sizeof(int));
    for (int i = 0; i < l.length; i++) {
        l.data[i] = p[i];   // 将数据复制到新区域
    }
    l.MaxSize = l.MaxSize + len;
    free(p);
}

int main(int argc, char const *argv[])
{
    SqList l;
    initList(l);
    increaseSize(l, 5);
    return 0;
}
```

```cpp
// 带头结点的单链表
#include <stdlib.h>

typedef int ElemType;
typedef struct LNode
{
    ElemType data;
    struct LNode *next;
} LNode, *LinkList;

// 初始化
bool InitList(LinkList &l) {
    l = (LNode *)malloc(sizeof(LNode));  // 分配一个头结点
    if (l == NULL)
    {
        return false;
    }
    l->next = NULL;
    return true;
}

bool isEmpty(LinkList &l) {
    if (l->next == NULL)
    {
        return true;
    }
    return false;
    
}
```

```cpp
// 双向链表
#include <stdio.h>
#include <stdlib.h>

typedef int ElemType;

typedef struct DNode {
    ElemType data;
    struct DNode *prior, *next;
} DNode, *DLinkList;

// 初始化
bool InitDLinkList(DLinkList &l) {
    l = (DNode *)malloc(sizeof(DNode)); // 分配头节点
    if (l == NULL)
    {
        return false;
    }
    l->prior = NULL;
    l->next = NULL;
    return true;
}

// 在p节点后插入s节点
bool InsertNextDNode(DNode *p, DNode *s) {
    if (p == NULL || s == NULL)
    {
        return false;
    }
    s->next = p->next;  // 将p的后继节点设置为s的后继节点
    if (p->next != NULL) // 如果p有后继节点
    {
        // 将p的后继节点的上一个设置为s
        p->next->prior = s;
    }
    s->prior = p;
    p->next = s;
}

// 删除p节点的后继节点
bool DeleteNextDNode(DNode *p) {
    if (p == NULL) {
        return false;
    }
    DNode *q = p->next;
    if (q == NULL)
    {
        return false;
    }
    p->next = q->next;
    if (q->next != NULL)
    {
        q->next->prior = p;
    }
    free(q);
    return true;
}

int main(int argc, char const *argv[])
{
    DLinkList l;
    bool ret = InitDLinkList(l);
    if (ret)
    {
        printf("初始化成功\n");
    } else
    {
        printf("初始化失败\n");
    }
    return 0;
}
```

## 2.栈

```cpp
// 栈(数组实现)
#include <stdio.h>
#define MaxSize 10

typedef struct {
    int data[MaxSize];
    int top;
} SqStack;

// 初始化
void InitStack(SqStack &s) {
    s.top = -1;
}

bool IsEmpty(SqStack &s) {
    if (s.top == -1)
    {
        return true;
    }
    return false;
}

// 入栈
bool push(SqStack &s, int &x) {
    // 栈已满
    if (s.top == MaxSize - 1)
    {
        return false;
    }
    s.top++;
    s.data[s.top] = x;
    return true;
}

// 出栈
bool pop(SqStack &s) {
    if (s.top == -1)
    {
        return false;
    }
    int x = s.data[s.top];
    printf("pop stack, value=%d\n", x);
    s.top--;
    return true;
}

int main(int argc, char const *argv[])
{
    SqStack stack;
    InitStack(stack);
    int x = 1;
    push(stack, x);
    pop(stack);
    return 0;
}
```

```cpp
/*
* 检查括号是否成对出现，且没有交叉 
*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MaxSize 10

// 定义栈
typedef struct {
    char data[MaxSize];
    int top;
} SqStack;

// 初始化
void initStack(SqStack &s) {
    s.top = -1;
}

// 是否空
bool isEmpty(SqStack &s) {
    if (s.top == -1)
    {
        return true;
    }
    return false;
}

// 入栈
bool push(SqStack &s, char x) {
    if (s.top == MaxSize-1) {
        return false;
    }
    s.top++;
    s.data[s.top] = x;
    return true;
}

// 出栈，用x返回
bool pop(SqStack &s, char &x) {
    if (s.top == -1)
    {
        return false;
    }
    x = s.data[s.top];
    s.top--;
    return true;
}

bool bracketCheck(char str[]) {
    SqStack s;
    initStack(s);
    int length = strlen(str);
    printf("str length is %d\n", length);
    for (int i = 0; i < length; i++)
    {
        if (str[i] == '(' || str[i] == '[' || str[i] == '{') {
            push(s, str[i]);  // 左括号则入栈
        } else {
            // 右括号检查，如果栈空，则失败
            if (isEmpty(s))
                return false;
            char topElem;
            pop(s, topElem); // 栈顶元素出栈
            if (str[i] == ')' && topElem != '(') {
                return false;
            }
            if (str[i] == ']' && topElem != '[') {
                return false;
            }
            if (str[i] == '}' && topElem != '{') {
                return false;
            }
        }
    }
    return isEmpty(s);
}

int main(int argc, char const *argv[])
{
    char ss[] = "([])[";
    bool ret = bracketCheck(ss);
    if (ret) {
        printf("检查成功");
    } else {
        printf("检查失败");
    }
    
    return 0;
}
```