# 导入aar

## 方式一

```gradle
android{
    repositories {
        flatDir {
            dirs 'libs'
        }
    }
}
dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation (name: 'xxxx', ext: 'aar')
}
```

## 方式二

```gradle
android{
   //不用写
   /* repositories {
        flatDir {
            dirs 'libs'
        }
    }*/
}
dependencies {
　    // 将
     implementation fileTree(dir: 'libs', include: ['*.jar'])
     // 改为
     implementation fileTree(dir: 'libs', include: ['*.jar','*.aar'])
}
```

这样就可以把 aar 文件放到 libs 目录，注意导入后要点击 **Sync Project with Gradle Files**，而不是 **Build -> Make Project**，后者不能正确找到导入的类。