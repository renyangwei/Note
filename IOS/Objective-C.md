# Objective-C

`Objective-C`是C语言的 **严格超集**－－任何C语言程序不经修改就可以直接通过Objective-C编译器，**在Objective-C中使用C语言代码也是完全合法的**。Objective-C被描述为盖在C语言上的薄薄一层，因为Objective-C的原意就是在C语言主体上加入面向对象的特性。

## 1.导包

```objective-c
#import <Foundation/Foundation.h>
```

## 2.数据结构

相互转化等，数字、字典、集合等等

### 2.1 基本数据类型

char、int、short、long、float、double、bool

**void类型**

`void`类型指定没有可用的值。比如函数返回值、函数参数。

在Objective-C编程语言中，要以对象形式保存基本数据类型，如：`int`，`float`，`bool`。Objective-C提供了一系列与`NSNumber`一起使用的方法，一些常用重要的方法列在下表中（暂时不知道有什么用）。

### 2.2 变量

```objective-c
int i = 0;
char c = 123;
float f = 1.14;
extern double d = 3.443;// extern 类似public
```

### 2.3 常量

有两种方式：define和const

```objective-c
#define LENGTH 10
const int WIDTH = 10
```

### 2.4 数组

用法基本相同。

```objc
int arr[5] = {1, 2, 3, 4, 5};
for (int a=0; a<(sizeof(arr)/sizeof(arr[0])); a++) {
    NSLog(@"a=%d", arr[a]);
}
```

### 2.5 指针

也没什么不同。

```objc
int *zhishen;
int x = 5;
zhishen = &x;
NSLog(@"zhizhen=%x", zhishen);
NSLog(@"zhizhen value=%d", *zhishen);
```

### 2.6 字符串

Objective-C编程语言中的字符串使用`NSString`表示，其子类`NSMutableString`提供了几种创建字符串对象的方法。 创建字符串对象的最简单方法是使用Objective-C的标识符：`@""`来构造。

```objc
// 定义
NSString *ss = @"12345";
NSLog(@"%@", ss);
// 字符串操作
NSLog(@"%lu", (unsigned long)[ss length]);// 长度
NSLog(@"append a and b=%@", [ss stringByAppendingFormat:@"0987"]);// 连接，不能用+
```

### 2.7 结构体

OC里的 `.` 只在结构体用到，其他是大括号[]。

结构体用法也基本相同。

```objc
struct Book {
    int id;
    NSString *title;
    NSString *author;
};
struct Book book;
book.id = 1;
book.title = @"OC从入门到放弃";
book.author = @"ren";
NSLog(@"Book title : %@\n", book.title);
```

### 3.8 NS基础类

`Foundation`框架定义了Objective-C类的基础层。在基本数据类型上提供一小组基本实用程序类。

使用`#import <Foundation/Foundation.h>`导入。

**NSArray和NSMutableArray**

`NSArray`用于保存不可变对象数组，`NSMutableArray`用于保存可变对象数组。`NSMutableArray` 继承自 `NSArray` 。

```objc
// NSMultiArray
NSMutableArray *mutableArr = [[NSMutableArray alloc]init];
[mutableArr addObject:@"hello"];
NSLog(@"index0=%@", [mutableArr objectAtIndex:0]);
[mutableArr removeAllObjects];
```

**NSDictionary和NSMutableDictionary**

`NSDictionary`用于保存对象的不可变字典，`NSMutableDictionary`用于保存对象的可变字典。`NSMutableDictionary`继承自`NSDictionary` 。

```objc
// NSMutableDictionary
NSMutableDictionary *md = [[NSMutableDictionary alloc]init];
[md setValue:@"world" forKey:@"10"];
NSLog(@"md=%@", [md objectForKey:@"10"]);
[md removeAllObjects];
```

### 3.9 类型转化

**NSInteger转化NSString类型**

`NSString *m = [NSString stringWithFormat:@"%d", {NSInteger}];`

**NSString转化 NSInteger类型：**

`NSInteger *i = [{NSInteger} intValue]; `

## 3.算法

### 3.1 运算符

`+、-、*、/、%、==、!=、>、<、&&、||、!`

用法全部相同，包括其他。

### 3.2 循环

和Java完全一样。好像没看到switch。

```objective-c
const int WIDTH = 4;
for (int i=0; i<WIDTH; i++) {
	// anything you do
}
while (true) {
  // 无限循环
  // 合适的时候使用
  break;
  continue;
}
if (1<2) {
  // print ...
} else {
  // print ...
}
```

## 4.面向对象

### 4.1 函数

在一个源文件中定义方法并在另一个文件中调用该方法时，需要方法声明。 在这种情况下，应该在调用该函数的文件顶部声明该函数。或者在头文件里声明。

```objective-c
// 声明
// 去掉函数体就是声明
// 在一个源文件中定义方法并在另一个文件中调用该方法时，需要方法声明。 在这种情况下，应该在调用该函数的文件顶部声明该函数。
- (int) max:(int) num1 :(int) num2

// 定义
/* 返回两个参数的最大值 */
- (int) max:(int) num1 :(int) num2 {
   /* 局部变量声明 */
   int result;
   if (num1 > num2) {
      result = num1;
   } else {
      result = num2;
   }
   return result; 
}
  
// 调用,self表示本类的对象，也可以写其他对象
int max = [self maxNum:1 :2];
NSLog(@"%d", max);
```



另一种写法，可供参考

```objc
#import <Foundation/Foundation.h>

@interface SampleClass:NSObject
/* 方法声明 */
- (int)max:(int)num1 andNum2:(int)num2;
@end

@implementation SampleClass

/* 返回两个数的最大值 */
- (int)max:(int)num1 andNum2:(int)num2 {

   /* 声明局部变量 */
   int result;

   if (num1 > num2) {
      result = num1;
   } else {
      result = num2;
   }

   return result; 
}

@end

int main () {

   /* 定义局部变量 */
   int a = 119;
   int b = 199;
   int ret;

   SampleClass *sampleClass = [[SampleClass alloc]init];

   /* 调用方法来获取最大值 */
   ret = [sampleClass max:a andNum2:b];

   NSLog(@"Max value is : %d\n", ret );
   return 0;
}
```



### 4.2 块

块是C，Objective-C和C++等编程语言中的高级功能，它允许创建不同的代码段，这些代码段可以传递给方法或函数，就像它们是值一样。 块是Objective-C对象，类似于其他编程语言中的闭包或`lambda`。

用法和匿名函数类似。既然是函数，也需要声明、实现和调用。

举例：

```objc
#import <Foundation/Foundation.h>

// 块声明
typedef void (^CompletionBlock)();

// 声明接口
@interface SampleClass:NSObject
  // 声明函数里的参数是块名称
- (void)performActionWithCompletion:(CompletionBlock)completionBlock;
@end

  // 实现接口
@implementation SampleClass

- (void)performActionWithCompletion:(CompletionBlock)completionBlock {
   NSLog(@"Action Performed");
   completionBlock();
}

@end

int main() {

   /* 第一个Objective-C程序 */
   SampleClass *sampleClass = [[SampleClass alloc]init];
   // 调用函数，传入匿名块，用法应该是回调函数
   [sampleClass performActionWithCompletion:^{
      NSLog(@"Completion is called to intimate action is performed.");
   }];

   return 0;
}
```

### 4.3 类

需要先声明。函数、类、块都需要 声明 -> 实现 -> 调用。

太TM麻烦了。

举例：

```objc
// 声明类
@interface Box : NSObject {
    // Protected instance variables (not recommended)
}
// 属性
@property(nonatomic, readwrite) int x;
// 方法
- (int)sum: (int)y;
@end
```

```objc
// 实现类
@implementation Box

// 构造函数
-(id)init {
    return [super init];
}

- (int)sum: (int)y {
    return  self.x * y;
}

@end
```

```objc
// 调用类
Box *box = [[Box alloc]init];
// 访问属性用点
box.x = 10;
// 访问方法用[]，这什么玩意
int sum = [box sum:10];
NSLog(@"sum=%d", sum);
```

### 4.4 继承

OC只能有一个基类但允许多级继承。所有类都派生自超类`NSObject`。定义一个类至少要继承 `NSObjcet`。

用法估计差不多。

## 5.错误处理

捕获错误

## 6.异步

多线程、多进程等

## 7.其他特性

该语言特性，比如宏、装饰器、defer、channel、反射等等。

### 7.1 预处理器

Objective-C预处理器只是一个文本替换工具，它指示编译器在实际编译之前进行必要的预处理。

举例：

```objc
// 定义宏
#define MAX_LENTH 20
// 导入头文件
#import <Foundation/Foundation.h>
#include "myheader.h"
```

### 7.2 typedef

`typedef`为类型指定新名称。比如：

```objc
typedef unsigned char BYTE;
```

为单字节数字定义术语`BYTE` 。

估计不怎么用。

## 8.应用

JSON、网络、存储、文件、时间日期、日志等

### 8.1 日志处理

打印日志使用 `NSLog()`。

举例：

```objc
#define DEBUG 1

#if DEBUG == 0
#define DebugLog(...)
#elif DEBUG == 1
#define DebugLog(...) NSLog(__VA_ARGS__)
#endif

int main() {
   DebugLog(@"Debug log, our custom addition gets \
   printed during debug only" );
   NSLog(@"NSLog gets printed always" );     
   return 0;
}
```



