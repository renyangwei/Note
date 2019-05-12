# pyinstaller生成exe

1.下载

    pip install pyinstaller

2.运行

    pyinstaller -F -w xxx.py 

说明：

`-F`：表示生成单个可执行文件

`-w`：表示去掉控制台窗口，这在GUI界面时非常有用

如果有报错要先更新

    pip install --upgrade setuptools

最后会在 *dist* 文件夹内生成 `xxx.exe`