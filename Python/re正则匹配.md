# re正则匹配模块

正则表达式是一种小型、高度专业化的编程语言，由C编写的引擎执行。在 Python 中，我们可以使用内置的 `re` 模块来使用正则表达式。

正则表达式使用 `\` 对特殊字符进行转义，而 Python 的字符串本身也用 `\` 转义，因此，我们建议使用 Python 的原始字符串 `r'python\.org'` 。

## 正则表达式

| 字符    | 含义                                                         |
| ------- | ------------------------------------------------------------ |
| `\d`    | 一个十进制数,[0-9]                                           |
| `\w`    | 一个任意字符，[a-zA-Z0-9]                                    |
| `.`     | 除了\n 之外的任意一个字符                                    |
| `*`     | 任意个（包括0）个字符                                        |
| `+`     | 至少一个字符                                                 |
| `?`     | 0个或1个字符                                                 |
| `{n}`   | n个字符                                                      |
| `{n,m}` | n-m个字符                                                    |
| `\s`    | 相当于 `[\t\n\r\f\v]`                                        |
| `[]`    | 表示范围，[abc]或者[a-c]：匹配abc；[a,b,c]：匹配abc中的任意一个<br>还可以取消元字符的特殊功能 |
| `|`     | 或， `A|B`匹配A或者B                                         |
| `^`     | 行的开头                                                     |
| `$`     | 行的结束                                                     |
| `\b`    | 匹配一个单词边界，也就是单词和特殊字符的位置                 |

`*`  =  `{0, +oo}`

`+` = `{1, +oo}`

`?` = `{0, 1}`



re 模块的一般使用步骤如下：

- 使用 compile 函数将正则表达式的字符串形式编译为一个 Pattern 对象
- 通过 Pattern 对象提供的一系列方法对文本进行匹配查找，获得匹配结果（一个 Match 对象）
- 最后使用 Match 对象提供的属性和方法获得信息，根据需要进行其他的操作

# compile

用于编译正则表达式，生成一个 Pattern 对象。

```python
re.compile(pattern[, flag])
```

pattern 是一个字符串形式的正则表达式，flag 是一个可选参数，表示匹配模式，比如忽略大小写，多行模式等。

举例：

```python
import re

# 将正则表达式编译成 Pattern 对象 
pattern = re.compile(r'\d+')
```

## match

查找字符串的头部（也可以指定起始位置），它是一次匹配，只要找到了一个匹配的结果就返回一个对象，而不是查找所有匹配的结果。

举例：

```python
import re
pattern = re.compile(r'\d+')
# 查找头部
m = pattern.match('one12twothree34four')
print m
# None，没有匹配

# 从'e'的位置开始匹配
m = pattern.match('one12twothree34four', 2, 10)
print m
# None, 没有匹配

# 从'1'的位置开始匹配，正好匹配
m = pattern.match('one12twothree34four', 3, 10)
# 返回一个 Match 对象
print m
# 获得整个匹配的子串
m.group()
# '12'
```

## findall

以列表形式返回全部能匹配的子串，如果没有匹配，则返回一个空列表。

举例：

```python
import re
# w 和 l 之间两个字符
re.findall(r'w\w{2}l', 'world')  # ['worl']
re.findall(r'w..l', 'world')  # ['worl']
re.findall(r'w..l', 'world')  # ['worl']
```

## split

按照能够匹配的子串将字符串分割后返回列表。

举例：

```python
import re

p = re.compile(r'[\s\,\;]+')
print p.split('a,b;; c   d')
# ['a', 'b', 'c', 'd']
```

其他参考 [文档](https://wiki.jikexueyuan.com/project/explore-python/Regular-Expressions/re.html)

举例：

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import re

# [] 字符集：取消元字符的特殊功能， \ ^ - 例外
# 找 w 或者 .
print re.findall('[w, .]', 'awdx.')
# 找 w 或者 ,
print re.findall(r'[w, ,]', 'a,wdx.')
# 会匹配逗号
print re.findall(r'[a-z,0-9,A-Z]', 'asdafa,kjioi')
# 不会匹配逗号
print re.findall(r'[a-z0-9A-Z]', 'asdafa,kjioi')
# ^ 在 [] 里表示取反,除了 4，逗号和5之外
print re.findall('[^4,5]', '4567,89')
# 匹配两个数字
print re.findall(r'\d{2}', 'ab302dg87')
# 匹配一个以上非数字
print re.findall(r'\D+', 'ab302dgau87')
# 匹配回车制表符等等
print re.findall(r'\s', 'ab30\t2dgau87')
# \b
print re.findall(r'\b', '@implementation NNNN_enabledWeaponDataTemp_GGGG-(void)Aa{}')
print re.split(r'[ \-+(){}]', '@implementation NNNN_enabledWeaponDataTemp_GGGG-(void)Aa{}')

# search，返回对象，可以获取位置和匹配的字符
m = re.search('sb', 'gsbihllsbhh')
print m.group()
print m.span()

# 找反斜杠
print re.findall(r'\w\\\w', 'adfasD\p')

# 将as作为一个整体
print re.findall(r'(as)+', 'basasihjgk')

# ?P<> 尖括号里是组名，用来获取
ret = re.search('(?P<id>\d{3})/(?P<name>\w{3})', 'fjghjfa987/dihd')
print ret.group()
print ret.group('id')
print ret.group('name')
```

