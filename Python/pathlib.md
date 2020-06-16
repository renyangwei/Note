# pathlib

在Python 3.4，标准库添加了新的模块 `pathlib`，它使用面向对象的编程方式来表示文件系统路径。

**如果你想全面使用pathlib模块，应该使用Python3.6或者更高版本！**

### 基本用法

```python
from pathlib import Path

# 创建目录对象
p = Path(Path.cwd()) # 当前目录

# 将对象转化成字符
print('p=', str(p))

# 拼接路径
p = p.joinpath('a', 'b', 'cpython.txt')
print('path=', str(p))

# 获取文件名
print('filename=', p.name)

# 文件后缀名,多个后缀名 p.suffixes
print('suffix=', p.suffix)

# 去掉后缀名的文件名
print('stem=', p.stem)

# 修改文件名、后缀名
print('change name=', p.with_name('cgo.py'))
print('change suffix=', p.with_suffix('.java'))

# 是否存在
print(p.is_dir())
print(p.is_file())

# 父级目录,返回的也是path对象
print('parent dir=', p.parent)

# 多级父目录
print('parent dirs=', p.parents[1])
p.mkdir()

# 创建文件,接收参数，权限和能否重复创建
p.touch()

```

