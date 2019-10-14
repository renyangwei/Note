# 为方法数超过 64K 的应用启用多 dex 文件

Dalvik Executable 规范将可在单个 DEX 文件内引用的方法总数限制为 65,536，其中包括 Android 框架方法、库方法以及您自己的代码中的方法。

当您的应用及其引用的库超过 65,536 种方法时，您会遇到编译错误

```
trouble writing output:
    Too many field references: 131000; max is 65536.
    You may try using --multi-dex option.
```

由于 65,536 等于 64 X 1024，因此这一限制称为“64K 引用限制”。

## Android 5.0 之前版本的多 dex 文件支持

Android 5.0（API 级别 21）之前的平台版本使用 Dalvik 运行时来执行应用代码。您可以在您的项目中添加多 dex 文件支持库：

```
dependencies {
    implementation 'androidx.multidex:multidex:2.0.1'
}       
```

如果您不使用 AndroidX，请改为添加以下支持库依赖项：

```
dependencies {
    implementation 'com.android.support:multidex:1.0.3'
}    
```

操作步骤如下：

1.修改模块级 build.gradle 文件以启用多 dex 文件，并将多 dex 文件库添加为依赖项，如下所示：

```
    android {
        defaultConfig {
            ...
            minSdkVersion 15
            targetSdkVersion 28
            multiDexEnabled true
        }
        ...
    }

    dependencies {
      compile 'com.android.support:multidex:1.0.3'
    }
    
```

2.根据是否替换 Application 类，执行以下某项操作：

2.1 如果您不替换 Application 类，请修改清单文件以设置 `<application>` 标记中的 android:name，如下所示：

```xml
    <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="com.example.myapp">
        <application
                android:name="android.support.multidex.MultiDexApplication" >
            ...
        </application>
    </manifest>
    
```

2.2 如果您替换 Application 类，请对其进行更改以扩展 MultiDexApplication（如果可能），如下所示：

```java
    public class MyApplication extends MultiDexApplication {
        ... 
    }
```

或者，如果您替换 Application 类，但无法更改基类，则可以改为替换 `attachBaseContext() `方法并调用 `MultiDex.install(this)` 来启用多 dex 文件：

```java
    public class MyApplication extends SomeOtherApplication {
      @Override
      protected void attachBaseContext(Context base) {
         super.attachBaseContext(base);
         MultiDex.install(this);
      }
    }
```

## Android 5.0 及更高版本的多 dex 文件支持

Android 5.0（API 级别 21）及更高版本使用名为 ART 的运行时，它本身支持从 APK 文件加载多个 DEX 文件。ART 在应用安装时执行预编译，扫描 classesN.dex 文件，并将它们编译成单个 .oat 文件，以供 Android 设备执行。

因此，如果您的 minSdkVersion 为 21 或更高的值，则不需要多 dex 文件支持库,只需在模块级 build.gradle 文件中将 `multiDexEnabled` 设为 true，如下所示：

```
android {
    defaultConfig {
        ...
        minSdkVersion 21
        targetSdkVersion 28
        multiDexEnabled true
    }
    ...
}    
```

## 规避 64K 限制

- 减少依赖项
- 通过 ProGuard 移除未使用的代码