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

### 4.2 布局和绑定表达式

借助表达式语言，您可以编写将变量关联到布局中的视图的表达式。数据绑定库会自动生成将布局中的视图与您的数据对象绑定所需的类。该库提供了可在布局中使用的导入、变量和头文件等功能。

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

User对象

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

绑定数据

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
   User user = new User("Test", "User");
   binding.setUser(user);
}
```