- [Android Jetpack](#android-jetpack)
  - [1. 在应用中使用 Jetpack 库](#1-%e5%9c%a8%e5%ba%94%e7%94%a8%e4%b8%ad%e4%bd%bf%e7%94%a8-jetpack-%e5%ba%93)
  - [2. Android KTX](#2-android-ktx)
  - [3. v7 支持库](#3-v7-%e6%94%af%e6%8c%81%e5%ba%93)
    - [3.1 v7 appcompat库](#31-v7-appcompat%e5%ba%93)
    - [3.2 v7 Cardview库](#32-v7-cardview%e5%ba%93)
    - [3.3 v7网格布局库](#33-v7%e7%bd%91%e6%a0%bc%e5%b8%83%e5%b1%80%e5%ba%93)
    - [3.4 v7调色板库](#34-v7%e8%b0%83%e8%89%b2%e6%9d%bf%e5%ba%93)
    - [3.5 v7 recyclerview库](#35-v7-recyclerview%e5%ba%93)
    - [3.6 v13支持库](#36-v13%e6%94%af%e6%8c%81%e5%ba%93)
    - [3.7 矢量可绘制库](#37-%e7%9f%a2%e9%87%8f%e5%8f%af%e7%bb%98%e5%88%b6%e5%ba%93)
    - [3.8 动画矢量可绘制库](#38-%e5%8a%a8%e7%94%bb%e7%9f%a2%e9%87%8f%e5%8f%af%e7%bb%98%e5%88%b6%e5%ba%93)
    - [3.9 注释支持库](#39-%e6%b3%a8%e9%87%8a%e6%94%af%e6%8c%81%e5%ba%93)
    - [3.10 设计支持库](#310-%e8%ae%be%e8%ae%a1%e6%94%af%e6%8c%81%e5%ba%93)
    - [3.11 自定义标签支持库](#311-%e8%87%aa%e5%ae%9a%e4%b9%89%e6%a0%87%e7%ad%be%e6%94%af%e6%8c%81%e5%ba%93)
  - [4. 数据绑定库](#4-%e6%95%b0%e6%8d%ae%e7%bb%91%e5%ae%9a%e5%ba%93)
    - [4.1 搭建环境](#41-%e6%90%ad%e5%bb%ba%e7%8e%af%e5%a2%83)
    - [4.2 布局和绑定表达式](#42-%e5%b8%83%e5%b1%80%e5%92%8c%e7%bb%91%e5%ae%9a%e8%a1%a8%e8%be%be%e5%bc%8f)
    - [4.3 使用可观察的数据对象](#43-%e4%bd%bf%e7%94%a8%e5%8f%af%e8%a7%82%e5%af%9f%e7%9a%84%e6%95%b0%e6%8d%ae%e5%af%b9%e8%b1%a1)
    - [4.4 生成绑定类](#44-%e7%94%9f%e6%88%90%e7%bb%91%e5%ae%9a%e7%b1%bb)
  
# Android Jetpack

Jetpack 是一套库、工具和指南，可帮助开发者更轻松地编写优质应用。这些组件可帮助您遵循最佳做法、让您摆脱编写样板代码的工作并简化复杂任务，以便您将精力集中放在所需的代码上。

## 1. 在应用中使用 Jetpack 库

打开您的项目的 build.gradle 文件并添加 google() 代码库，如下所示：

```
allprojects {
    repositories {
        google()
        jcenter()
    }
}
```

然后，您可以添加 Jetpack 组件，例如作为 Lifecycles 库的一部分的 LiveData 和 ViewModel 等架构组件，如下所示：

```
    dependencies {
        def lifecycle_version = "2.0.0"
        implementation "androidx.lifecycle:lifecycle-extensions:$lifecycle_version"
        // Optional : Kotlin extension (https://d.android.com/kotlin/ktx)
        implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycle_version"
        ...
    }
```

## 2. Android KTX

Android KTX 是一组 Kotlin 扩展程序，属于 Android Jetpack 系列。它优化了供 Kotlin 使用的 Jetpack 和 Android 平台 API。Android KTX 旨在让您利用 Kotlin 语言功能（例如扩展函数/属性、lambda、命名参数和参数默认值），以更简洁、更愉悦、更惯用的方式使用 Kotlin 进行 Android 开发。Android KTX 不会向现有的 Android API 添加任何新功能。


## 3. v7 支持库  

### 3.1 v7 appcompat库

该库增加了对 操作栏用户界面设计模式的支持。

添加依赖

    com.android.support:appcompat-v7:28.0.0

以下是v7 appcompat库中包含的一些关键类：

- [ActionBar](https://developer.android.com/reference/androidx/appcompat/app/ActionBar.html)-提供操作栏 用户界面模式的实现
- [AppCompatActivity](https://developer.android.com/reference/androidx/appcompat/app/AppCompatActivity.html) -添加了一个应用程序活动类，该类可以用作使用支持库操作栏实现的活动的基类
- [AppCompatDialog](https://developer.android.com/reference/androidx/appcompat/app/AppCompatDialog.html) -添加一个对话框类，可用作AppCompat主题对话框的基类
- [ShareActionProvider](https://developer.android.com/reference/androidx/appcompat/widget/ShareActionProvider.html) -添加了对可包含在操作栏中的标准化共享操作（例如电子邮件或发布到社交应用程序）的支持

### 3.2 v7 Cardview库

该库增加了对 `CardView` 小部件的支持，使您可以在卡片上显示信息，这些卡片在任何应用程序上的外观都一致。

添加依赖：

    com.android.support:cardview-v7:28.0.0

### 3.3 v7网格布局库

该库添加对 `GridLayout` 类的支持 ，使您可以使用矩形单元格的网格来排列用户界面元素。

添加依赖：

    com.android.support:gridlayout-v7:28.0.0

### 3.4 v7调色板库

v7调色板支持库包括 `Palette` 类，该类使您可以从图像中提取突出的颜色。例如，音乐应用程序可以使用一个 Palette对象从专辑封面中提取主要颜色，然后使用这些颜色构建颜色协调的歌曲标题卡。

添加依赖：

    com.android.support:palette-v7:28.0.0

### 3.5 v7 recyclerview库

recyclerview库添加了 `RecyclerView` 该类。此类提供对RecyclerView 小部件的支持，该小部件是通过提供有限的数据项窗口来有效显示大型数据集的视图。

添加依赖：

    com.android.support:recyclerview-v7:28.0.0

### 3.6 v13支持库

V4片段库提供了一个Fragment类。v4 Fragment类是一个独立的类，提供了在更高平台版本中添加的错误修复，而v13 `FragmentCompat` 类为该类的框架实现提供了兼容性修补程序Fragment。

添加依赖：

    com.android.support:support-v13:28.0.0

### 3.7 矢量可绘制库

提供对静态矢量图形的支持。

    com.android.support:support-vector-drawable:28.0.0

### 3.8 动画矢量可绘制库

提供对动画矢量图形的支持。

    com.android.support:animated-vector-drawable:28.0.0

### 3.9 注释支持库

该注释包提供的API来支持添加注释元数据您的应用程序。

    com.android.support:support-annotations:28.0.0

### 3.10 设计支持库

设计支持库为应用程序开发人员添加了对各种材料设计组件和模式的支持，例如navigation drawers, floating action buttons (FAB), snackbars, and tabs

    com.android.support:design:28.0.0

### 3.11 自定义标签支持库

在 自定义选项卡 包提供的API支持添加和您的应用程序管理的自定义选项卡。

    com.android.support:customtabs:28.0.0

## 4. 数据绑定库

数据绑定库是一种支持库，借助该库，您可以使用声明性格式（而非程序化地）将布局中的界面组件绑定到应用中的数据源。


### 4.1 搭建环境

要将应用程序配置为使用数据绑定，请将dataBinding元素添加到 *build.gradle* 应用程序模块中的文件中：

```
android {
    ...
    dataBinding {
        enabled = true
    }
}
```

然后导入包

```
    def lifecycle_version = "2.0.0"
    implementation "androidx.lifecycle:lifecycle-extensions:$lifecycle_version"
    // Optional : Kotlin extension (https://d.android.com/kotlin/ktx)
    implementation "androidx.lifecycle:lifecycle-viewmodel:$lifecycle_version"
```

### 4.2 布局和绑定表达式

借助表达式语言，您可以编写将变量关联到布局中的视图的表达式。数据绑定库会自动生成将布局中的视图与您的数据对象绑定所需的类。该库提供了可在布局中使用的导入、变量和头文件等功能。

就是在原有的布局上增加layout根目录，然后使用data标签定义变量

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android">
   <data>
       <variable name="user" type="com.example.User"/>
   </data>
   <LinearLayout
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.firstName}"/>
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.lastName}"/>
   </LinearLayout>
</layout>
```

其中data描述了可以在此布局中使用的属性， `@{}` 语法则将布局内的表达式写入属性属性中。

**User对象**

```java
public class User {
  private final String firstName;
  private final String lastName;
  public User(String firstName, String lastName) {
      this.firstName = firstName;
      this.lastName = lastName;
  }
  public String getFirstName() {
      return this.firstName;
  }
  public String getLastName() {
      return this.lastName;
  }
}
```

**绑定数据**

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
   User user = new User("Test", "User");
   binding.setUser(user);
}
```

**表达语言**

您可以在表达式语言中使用以下运算符和关键字

- 数学的 `+ - / * %`
- 字符串串联 `+`
- 逻辑上 `&& ||`
- 二元 `& | ^`
- 一元 `+ - ! ~`
- 转移 `>> >>> <<`
- 比较` == > < >= <=`（请注意，<必须转义为&lt;）
- instanceof
- 分组 ()
- 文字-字符，字符串，数字， null
- 投
- 方法调用
- 现场访问
- 阵列存取 []
- 三元运算符 `?:`

举例

```
android:text="@{String.valueOf(index + 1)}"
android:visibility="@{age > 13 ? View.GONE : View.VISIBLE}"
android:transitionName='@{"image_" + id}'
```

**空合并运算符**

如果前一个是null则选择后一个，等效与三目运算符 `a==null?a:b`

    android:text="@{user.displayName ?? user.lastName}"

为了方便起见，可以使用运算符来访问常见集合，例如数组，列表，稀疏列表和映射

```
<data>
    <import type="android.util.SparseArray"/>
    <import type="java.util.Map"/>
    <import type="java.util.List"/>
    <variable name="list" type="List&lt;String>"/>
    <variable name="sparse" type="SparseArray&lt;String>"/>
    <variable name="map" type="Map&lt;String, String>"/>
    <variable name="index" type="int"/>
    <variable name="key" type="String"/>
</data>
…
android:text="@{list[index]}"
…
android:text="@{sparse[index]}"
…
android:text="@{map[key]}"
```

**字符串文字**

字符串文字应该用反引号引起来,而不是单引号（这么奇怪的吗）

    android:text="@{map[`firstName`]}"

**资源资源**

您可以使用以下语法访问表达式中的资源

    android:padding="@{large? @dimen/largePadding : @dimen/smallPadding}"

**导入，变量和包括**

导入使您可以轻松引用布局文件中的类。变量使您能够描述可在绑定表达式中使用的属性。包括让您在整个应用程序中重复使用复杂的布局。

1.导入

```xml
<data>
    <import type="android.view.View"/>
    <variable name="user" type="com.dyb.User" />
    <import type="com.example.MyStringUtils"/>
</data>
<TextView
   android:text="@{user.lastName}"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:visibility="@{user.isAdult ? View.VISIBLE : View.GONE}"/>

<TextView
   android:text="@{MyStringUtils.capitalize(user.lastName)}"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```

也可以使用别名

```xml
<import type="com.example.real.estate.View"
        alias="Vista"/>
```

感觉 `import` 和 `variable` 没什么区别，导入一个类和定义一个变量不是一个意思吗


### 4.3 使用可观察的数据对象

可观察性是指对象将其数据更改通知他人的能力。数据绑定库使您可以观察对象，字段或集合。

任何普通的旧对象都可以用于数据绑定，但是修改对象不会自动导致UI更新。数据绑定可用于使您的数据对象在数据更改时通知其他对象（称为侦听器）。

有三种不同类型的可观察类： 对象，字段和 集合。

当这些可观察数据对象之一绑定到UI且数据对象的属性更改时，UI将自动更新。

1.字段

可观察字段是具有单个字段的自包含可观察对象。请使用public finalJava编程语言创建一个属性。

- ObservableBoolean
- ObservableByte
- ObservableChar
- ObservableShort
- ObservableInt
- ObservableLong
- ObservableFloat
- ObservableDouble
- ObservableParcelable

> 注意：Android Studio 3.1及更高版本允许您用LiveData对象替换可观察字段，这为您的应用程序提供了更多好处。有关更多信息，请参见使用LiveData通知UI有关数据更改。

举例：

内部字段改成只读的ObservableField

```java
public class User {
    public final ObservableField<String> firstName = new ObservableField<>();
    public final ObservableField<String> lastName = new ObservableField<>();
}
```

```xml
<data>
    <variable
        name="user"
        type="ren.bottomnavigation.User" />
</data>

<TextView
    android:id="@+id/message"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@{user.firstName}"
/>
```

只需要改字段就能自动改控件的内容

```java
user.firstName.set("Google");
```

2.集合

一些应用程序使用动态结构来保存数据。可观察的集合允许使用密钥访问这些结构。

```java
ObservableArrayMap<String, Object> user = new ObservableArrayMap<>();
user.put("firstName", "Google");
user.put("lastName", "Inc.");
user.put("age", 17);
```

在布局中，可以使用字符串键找到Map的值

```xml
<data>
    <import type="android.databinding.ObservableMap"/>
    <variable name="user" type="ObservableMap<String, Object>"/>
</data>
…
<TextView
    android:text="@{user.lastName}"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
<TextView
    android:text="@{String.valueOf(1 + (Integer)user.age)}"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

3.对象

实现Observable接口的类 允许注册要在可观察对象上进行属性更改通知的侦听器。

```java
private static class User extends BaseObservable {
    private String firstName;
    private String lastName;

    @Bindable
    public String getFirstName() {
        return this.firstName;
    }

    @Bindable
    public String getLastName() {
        return this.lastName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
        notifyPropertyChanged(BR.firstName);
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
        notifyPropertyChanged(BR.lastName);
    }
}
```

### 4.4 生成绑定类

