# zip命令.md

可以用来解压缩文件，或者对文件进行打包操作。zip是个使用广泛的压缩程序，文件经它压缩后会另外产生具有“.zip”扩展名的压缩文件。

如要在Windows系统上使用，请下载 [Zip for Windows](http://gnuwin32.sourceforge.net/packages/zip.htm) 及其依赖 [Bzip2 for Windows](http://gnuwin32.sourceforge.net/packages/bzip2.htm)，将bin目录添加到path环境变量。

## 实例

将 */home/Blinux/html/* 这个目录下所有文件和文件夹打包为当前目录下的html.zip：

    zip -q -r html.zip /home/Blinux/html

比如现在我的html目录下，我操作的zip压缩命令是：

    zip -q -r html.zip *
