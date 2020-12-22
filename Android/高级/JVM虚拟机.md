# JVM虚拟机

## 1.Java技术体系

C语言是通过编译器先编译成汇编，然后编译成机器码给机器执行。使用CPU提供的指令。

Java则是通过编译器编译成class文件给虚拟机执行。使用虚拟机提供的指令。

所以我们甚至可以自定义编译器，只要能编译成class文件就可以给虚拟机。

## 2.Lanmbda表达式

Java 1.8 加入。

用于简化只有一个实现函数的匿名内部类，比如OnClickListener：

```java
Button button = new Button(activity);
// 直接写参数，箭头后跟上自己的逻辑
button.setOnClickListener(click -> {
    Log.d(TAG, "addBtn: you click me");
    // do other things
});
```

## 3.内存区域

### 程序计数器

存放下一个将要执行的字节码指令的地址，字节码解释器负责改变该值。

每个线程都有单独的程序计数器。

### Java虚拟机栈

Java方法执行的动态内存模型。执行每个方法都会创建一个栈帧，伴随方法从创建到执行完成。栈帧放到栈里。

如果栈帧不停的入栈，即一个方法调用子方法，子方法再调用子方法，超出栈的范围，就会报 **StackOverflowError** (栈溢出错误)。

如果栈没有限制大小，则会报 **OutOfMemery** (内存溢出) 。

栈的大小可以自己设定，默认只有几百KB，比如128KB。

### Java堆

存放对象实例

### 方法区

存储加载的类信息，常量，静态变量，即时编译器编译后的代码等数据。

举例：

```java
String a = "abc";
String b = "abc";
// true，在常量池中，不会重复
System.out.print(a == b);
String c = new String("abc");
System.out.println();
// false，在堆中新开辟了一块内存空间
System.out.print(a == c);
```

