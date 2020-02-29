# apktool 反编译报错：Encountered small uint that is out of range at offset 0x38

**报错信息：**

```
Exception in thread "main" org.jf.util.ExceptionWithContext: Encountered small uint that is out of range at offset 0x38
at org.jf.dexlib2.dexbacked.BaseDexBuffer.readSmallUint(BaseDexBuffer.java:58)
at org.jf.dexlib2.dexbacked.DexBackedDexFile.(DexBackedDexFile.java:90)
at org.jf.dexlib2.dexbacked.DexBackedDexFile.(DexBackedDexFile.java:110)
at org.jf.dexlib2.dexbacked.ZipDexContainer$ZipDexFile.(ZipDexContainer.java:146)
at org.jf.dexlib2.dexbacked.ZipDexContainer.loadEntry(ZipDexContainer.java:188)
at org.jf.dexlib2.dexbacked.ZipDexContainer.getEntry(ZipDexContainer.java:115)
at org.jf.dexlib2.dexbacked.ZipDexContainer.getEntry(ZipDexContainer.java:58)
at org.jf.dexlib2.DexFileFactory$DexEntryFinder.findEntry(DexFileFactory.java:382)
at org.jf.dexlib2.DexFileFactory.loadDexEntry(DexFileFactory.java:186)
at brut.androlib.src.SmaliDecoder.decode(SmaliDecoder.java:72)
at brut.androlib.src.SmaliDecoder.decode(SmaliDecoder.java:38)
at brut.androlib.Androlib.decodeSourcesSmali(Androlib.java:98)
at brut.androlib.ApkDecoder.decode(ApkDecoder.java:163)
at brut.apktool.Main.cmdDecode(Main.java:167)
at brut.apktool.Main.main(Main.java:76)
```

**原因：**

classes.dex文件里可能包含无法反编译的内容，比如 A3AEECD8.dex 。

**解决方法：**

1. 更新 apktool 到最新版本，本人更新到的是 2.4.1;
2. 使用参数 `--only-main-classes `

举例：

    apktool d app-debug.apk --only-main-classes


参考：[apktool issues](https://github.com/iBotPeaches/Apktool/issues/2215)