# ProGuard

Android代码混淆，又称Android混淆，是一种Android APP保护技术，用于保护APP不被破解和逆向分析。

**ProGuard的三大作用**

- 压缩（Shrinking）：移除未被使用的类、属性、方法等，并且会在优化动作执行之后再次执行（因为优化后可能会再次暴露一些未被使用的类和成员。
- 优化（Optimization）： 优化字节码，并删除未使用的结构。
- 混淆（Obfuscation）：将类名、属性名、方法名混淆为难以读懂的字母，比如a,b,c等，增大反编译难度。

## 开启ProGuard

在 *build.gradle* 文件内相应的构建类型中添加 `minifyEnabled true`。

```
android {
    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    ...
}
```

除了 minifyEnabled 属性外，还有用于定义 ProGuard 规则的 proguardFiles 属性：

- `getDefaultProguardFile('proguard-android.txt')` 方法可从 Android SDK *tools/proguard/* 文件夹获取默认的 ProGuard 设置。
提示：要想做进一步的代码压缩，请尝试使用位于同一位置的*proguard-android-optimize.txt* 文件。它包括相同的 ProGuard 规则，但还包括其他在字节码一级（方法内和方法间）执行分析的优化，以进一步减小 APK 大小和帮助提高其运行速度。

- `proguard-rules.pro` 文件用于添加自定义 ProGuard 规则。默认情况下，该文件位于模块根目录（build.gradle 文件旁）。

> 请注意，代码压缩会拖慢构建速度，因此您应该尽可能避免在调试构建中使用。

每次构建时 ProGuard 都会输出下列文件：

*dump.txt*

说明 APK 中所有类文件的内部结构。

*mapping.txt*

提供原始与混淆过的类、方法和字段名称之间的转换。

*seeds.txt*

列出未进行混淆的类和成员。

*usage.txt*

列出从 APK 移除的代码。

这些文件保存在 *\<module-name\>/build/outputs/mapping/release/* 中。


## 混淆规则

### 保留（keep options）

1.保留类名

```
#一颗星表示只保持该包下的类名，而子包下的类名还是会被混淆
-keep class com.ms.bean.*
#两颗星表示把本包和所含子包下的类名都保持
-keep class com.ms.bean.** 
```

使用上面两个规则都只是保持类名不变，类中的方法和成员都会被混淆

2.保留类名及类的成员

```
#保留 com.ms.bean包下的类及类的成员
-keep class com.ms.bean.*{*;}
#保留具体的某个类及类的成员
-keep class com.ms.bean.Person{*;}
```

如果不希望保留类的所有成员，可以使用：

```
<init>;     //匹配所有构造器
<fields>;   //匹配所有域
<methods>;  //匹配所有方法方法
# 如保留构造方法
-keep class com.ms.bean.Person{
<init>;
}
# 还可以在<fields>或<methods>前面加上private 、public、native等来进一步指定不被混淆的内容。
#如保留public构造方法
-keep class com.ms.bean.Person{
public <init>;
}
```

3.保留指定类的所有子类（implement／extends）

```
# 保留Activity的所有子类
-keep public class * extends android.app.Activity
```

### 压缩（Optimization options）

```
＃关闭压缩
-dontshrink 
-printusage {filename}
-whyareyoukeeping {class_specification}
```

### 优化（Optimization options）

```
#关闭优化
-dontoptimize  
#迭代优化，n表示proguard对代码进行迭代优化的次数，Android一般为5
-optimizationpasses n 
```

总结：暂时只用到了保留的的规则，优化和压缩暂时没有用到，以后做大型APP可以使用。

## 参考

https://www.jianshu.com/p/1b76e4c10495

https://developer.android.com/studio/build/shrink-code