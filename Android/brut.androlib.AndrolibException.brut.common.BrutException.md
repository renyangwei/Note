# 回编译报错：brut.androlib.AndrolibException: brut.common.BrutException

参考 [出处](https://www.jianshu.com/p/8876d84d18e7)

## 原因

cmd命令行长度有限制，Windows XP或更高版本，最大长度 **8191** 个字符。如果超过8191就会有问题。一般apk回编是没得问题，如果apk中不压缩的资源太多就会造成回编失败的问题，不压缩资源目录在apktool.yml中。

Linux中则不会有这样的问题。


## 解决

修改Apktool命令执行长度，即减少不压缩的资源。

```
!!brut.androlib.meta.MetaInfo
apkFileName: app-release-unsigned.apk
compressionType: false
doNotCompress:
- arsc
...
isFrameworkApk: false
```