# 关于so文件的版本问题

解决方案：

1. 为了减小 apk 体积，只保留 **armeabi** 和**armeabi-v7a**两个文件夹，并保证这两个文件夹中so文件数量一致


2. 对只提供**armeabi**版本的第三方so，原样复制一份到 **armeabi-v7a** 文件夹