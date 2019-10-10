# 一直卡在Gradle:Build Running的解决办法

## 方法一：

在 *C:\User\<用户名>\.gradle* 目录下新建一个gradle.properties文件，并在里面添加一行：`org.gradle.daemon=true`

## 方法二：

找到路径 *C:\Users\admin\.gradle\wrapper\dists*，在此文件夹下有一个gradle版本文件夹，打开后是一个名字很长的文件夹吗，下载对应版本的gradle，将下载的压缩包直接放进名字很长的文件夹中即可，不需要解压

## 方法三：

可能是由于国内的某些杀毒软件禁用了aapt.exe进程导致，关掉杀毒软件。

## 方法四（未验证）：

需要在android studio 中配置gradle的代理，
打开 *setting->gradle->Gradle VM Options*：
添加 `-Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=8087`
设置生成功后，重启androidstudio ，速度会非常快。