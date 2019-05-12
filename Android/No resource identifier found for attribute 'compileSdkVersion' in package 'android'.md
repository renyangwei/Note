# apktool 反编译报错：No resource identifier found for attribute 'compileSdkVersion' in package 'android'

反编译的时候报错

```
AndroidManifest.xml:1: error: No resource identifier found for attribute 'compileSdkVersion' in package 'android'
AndroidManifest.xml:1: error: No resource identifier found for attribute 'compileSdkVersionCodename' in package 'android'
```

在 Android Studio 3.2 上开发的程序反编译的时候好像会发生这种情况

解决方法：

1.新建任意空文件，比如:

    mkdir framework

2.输入

    apktool b apkDir -p framework -o apkDir_build.apk

`apkDir`：要编译的目录

参考 [这里](https://github.com/iBotPeaches/Apktool/issues/1842)