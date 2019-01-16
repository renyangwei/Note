# Python执行系统命令

## os.system

os.system用来执行cmd指令，在cmd输出的内容会直接在控制台输出，返回结果为0表示执行成功

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import os
ret = os.system("ls")
if ret != 0:
    os._exit(0)
```

## os.popen

如果想获取控制台输出的内容，那就用os.popen的方法了，popen返回的是一个file对象，跟open打开文件一样操作了，r是以读的方式打开

```python
# coding:utf-8
import os

# popen返回文件对象，跟open操作一样
f = os.popen("ls", "r")
d = f.read()  # 读文件
print(d)
print(type(d))
f.close()
```