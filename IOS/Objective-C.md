# Objective-C

`Objective-C`是C语言的 **严格超集**－－任何C语言程序不经修改就可以直接通过Objective-C编译器，**在Objective-C中使用C语言代码也是完全合法的**。Objective-C被描述为盖在C语言上的薄薄一层，因为Objective-C的原意就是在C语言主体上加入面向对象的特性。

## 1.导包

`import` 是C语言中的 `clude` 的增强版，不会重复导入。

```objective-c
#import <Foundation/Foundation.h>
```

## 2.数据结构

相互转化等，数字、字典、集合等等, 注释可以用 `#pragma mark` 。

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

- 当我们使用 `@` 符号创建字符串的时候，该对象存储在数据段。
- 当内存中创建一个字符串对象后，这个字符串对象就无法更改，重新赋值只是改变了指针变量而已。

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

#### 3.8.1 NSArray和NSMutableArray

`NSArray`用于保存不可变对象数组，`NSMutableArray`用于保存可变对象数组。`NSMutableArray` 继承自 `NSArray` 。

```objc
// NSMultiArray
NSMutableArray *mutableArr = [[NSMutableArray alloc]init];
[mutableArr addObject:@"hello"];
NSLog(@"index0=%@", [mutableArr objectAtIndex:0]);
[mutableArr removeAllObjects];
```

#### 3.8.2 NSDictionary和NSMutableDictionary

`NSDictionary`用于保存对象的不可变字典，`NSMutableDictionary`用于保存对象的可变字典。`NSMutableDictionary`继承自`NSDictionary` 。

```objc
// NSMutableDictionary
NSMutableDictionary *md = [[NSMutableDictionary alloc]init];
[md setValue:@"world" forKey:@"10"];
NSLog(@"md=%@", [md objectForKey:@"10"]);
[md removeAllObjects];
```

#### 3.8.3 NSString常用方法

```objc
// C语言中的字符数组转化成字符串
char * x = "rose";
NSString * s = [NSString stringWithUTF8String:x];
NSLog(@"%@", s);
// 返回格式化字符串
NSString * t = [NSString stringWithFormat:@"123%@", @"456"];
NSLog(@"t=%@", t);
// 字符串长度，可以处理中文
NSUInteger length = [t length];
NSLog(@"length=%lu", length);
// 判断是否相等,不能用==
[t isEqualToString:@"1234"];
// 根据asc码比较大小
[t isEqualToString:@"1234"];
NSComparisonResult result = [t compare:@"4321"];
```

> OC 中的中文占两个字节。

### 3.9 类型转化

**NSInteger转化NSString类型**

`NSString *m = [NSString stringWithFormat:@"%d", {NSInteger}];`

**NSString转化 NSInteger类型：**

`NSInteger *i = [{NSInteger} intValue]; `

**字典转模型**

定义：

```objc
#import "Teacher.h"

@implementation Teacher {

}

- (instancetype)initWithDictionary:(NSDictionary *)dict {
    if (self = [super init]) {
        // 核心方法
        [self setValuesForKeysWithDictionary:dict];
    }
    return self;
}

+ (instancetype)provinceWithDictionary:(NSDictionary *)dict {
    return [[self alloc] initWithDictionary:dict];
}

@end
```

调用：

```objc
NSDictionary *temDic = @{@"name": @"July", @"color": @"white"};
Teacher *model = [Teacher provinceWithDictionary:temDic];
NSLog(@"name=%@, color=%@", model.name, model.color);
```



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

新建cocoa class 文件就可以创建头文件和M文件。

数据类型是再内存中开辟空间的模板，类的本质是自定义数据类型，所以可以作为参数和返回值。

`static` 关键字：修饰的对象只初始化一次。

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

另一种方式：

```objc
// 声明
@interface Person : NSObject
// 属性在大括号里,属性名称必须要以下划线开头
// 默认情况下不能直接被访问
{
    // 如果要被访问则加public
    @public NSString *_name;
    @public int _age;
    float _height;
}
// 方法声明
- (void) run: (int)aa;
- (void) eat: (NSString *) food;
- (void)print: (NSString *) x :(NSString *) y;
@end


@implementation Person

// 方法实现，声明去掉分号，追加大括号
- (void) run: (int)aa {
    NSLog(@"you run %d kilometers", aa);
}

- (void)eat:(NSString *)food {
    NSLog(@"you eat %@", food);
}

- (void)print: (NSString *) x : (NSString *) y {
    NSLog(@"x=%@, y=%@", x, y);
}

@end
 
// 调用
int main(int argc, const char * argv[]) {
    // 访问对象的属性
    Person *p1 = [Person new];
    p1 -> _name = @"123";
    p1 -> _age = 14;
    (*p1)._height = 173.2;
    [p1 run:321];
    [p1 eat:@"egg"];
    [p1 print:@"12.5" :@"-4.3"];
    return 0;
}
```

**类方法(即静态方法)**

一句话：减号变加号。

也要声明和实现。

**构造函数**

规范：和类名同名的类方法。官方所有类都遵循这个规则。

> 发现除了类名方法，还可以用init。

举例：

`Animal.h`

```objc
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@interface Animal : NSObject
{
    float _width;
    float _color;
}

// 提供一个和类名同名的类方法，返回默认值的对象
+ (Animal *) animal;

// 同样使用with...and...方式，创建自定义对象
+ (Animal *) animalWith: (float) width andColor: (float) color;

// 静态函数，直接用类名调用
+ (void) run;

@end

NS_ASSUME_NONNULL_END
```

`Animal.m`

```objc
#import "Animal.h"
#import <Foundation/Foundation.h>

@implementation Animal

+ (Animal *) animal
{
    return [Animal new];
}

+ (Animal *) animalWith: (float) width andColor: (float) color
{
    Animal *animal = [Animal new];
    animal->_width = width;
    animal->_color = color;
    return animal;
}

+ (void) run
{
    NSLog(@"you are running");
}
@end
```

**self**

`self` 是一个指针，在对象方法中指向当前对象，在类方法中指向当前类。

**点语法**

大部分其他编程语言(C、Java等)都是用 `.` 访问对象方法，Object-c  中使用 `[]` 。

当属性拥有 `setter` 和 `getter` 方法的时候，就可以使用 **点语法**。

本质上还是调用 `setter` 和 `getter` 。

因为手动生成  `setter` 和 `getter` 比较麻烦，就可以使用 `@property` 注解自动生成。

举例：

Student.h

```objective-c
#import <Foundation/Foundation.h>


@interface Student : NSObject
{
    NSString * _name;
    
    int _age;
}

- (void)setName:(NSString *)name;

- (NSString *)name;

// property 注解可以自动生成 setter 和 getter
@property int age;

@end
```

```objective-c
Student *student = [Student new];
student.name = @"ren";
NSString *sname = student.name;
student.age = 12;
int sage = student.age;
```

> XCode4.4版本以后property注解可以自动实现属性的声明、setter和getter声明以及实现。

**初始化**

`Person *p = [Person new]` 完全等价于

`Person *p = [[Person alloc]init]`

### 4.4 继承

OC只能有一个基类但允许多级继承。所有类都派生自超类`NSObject`。定义一个类至少要继承 `NSObjcet`。

用法估计差不多。

### 4.5 内存管理

内存五大区域：

- 栈：存储局部变量，当局部变量的作用域被执行完后，局部变量会被系统立即回收。
- 堆：OC对象和C函数手动申请的字节空间，malloc、calloc、realloc，系统不会自动回收，直到程序结束。
- BSS段：存储未被初始化的全局变量、静态变量，一旦初始化就回收，并转存到数据段中。
- 数据段：存储初始化后的全局变量、静态变量，直到程序结束才被回收。
- 代码段：存储代码，程序结束的时候操作系统回收。

#### 4.5.1 引用计数器

每个对象都有一个属性 `retainCount`，类型是 `unsigned long`，8个字节，称之为 **引用计数器**，用来记录当前对象被引用的次数。

默认情况下，创建一个对象，计数器的值就是1。

被引用一次计数器就加1。所谓被引用，就是有指针指向该对象的地址。

当被引用的时候，发送1条retain消息，取消引用的时候发送1条release消息。

计数器的值等于0的时候，系统就会调用对象的 `dealloc` 方法， 回收该对象。

#### 4.5.2 内存管理分类

- MRC：Manual Reference Counting，手动内存管理
- ARC：Auto Reference Counting，自动内存管理

### 4.6 协议

专门声明方法(不能声明属性，也不能实现方法)，当某个类遵循了这个协议就拥有了这个协议中声明的方法。

**语法**

```
@protocol 协议名称 <NSObject>
方法声明
@end
```

**声明**

```objc
#import <Foundation/Foundation.h>

@protocol Animal <NSObject>

-(void) eat;

-(void) sleep;

@end
```

**遵循协议**

```objc
#import <Foundation/Foundation.h>
#import "Animal.h"
// 导入头文件，遵循即可,不需要再声明
@interface Dog : NSObject <Animal>

@end
```

**实现协议的声明**

```objc
#import "Dog.h"

@implementation Dog {

}

-(void)sleep {
    NSLog(@"I am sleeping");
}

- (void)eat {
    NSLog(@"I am eating");
}

@end
```

> 类似Java中的接口。

## 5.错误处理

捕获错误

```objc
@try
{

}
@catch(NSException *ex)
{

}
@finally
{
  
}
```

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



