# HJSON

`JSON` 是我们平时使用非常频繁的数据格式，尤其在网络传输中非常受欢迎。大部分编程语言都支持各种格式。

但是作为配置文件还是有些许不足，最主要的一点是缺乏注释（其他比如低信噪比其实还可以接受），所以在 `JSON` 的基础上衍生出了更方便的作为配置文件的格式 [HJSON](https://hjson.github.io/) 。

## 格式

`HJSON` 是 `JSON` 格式的扩展，增加了注释，并去掉多余的标识符。

注释支持单行和多行，也支持Python脚本的#注释。

```HJSON
{
  // 注释
  // 可以使用 #, // 或者 /**/,
  // 数字
  key: 1
  // 字符串
  contains: everything on this line
  // 集合
  cool: {
    foo: 1
    bar: 2
  }
  // 数组
  list: [
    1,
    2,
  ]
  // 多行字符串
  realist:
    '''
    My half empty glass,
    I will fill your empty half.
    Now you are half full.
    '''
}
```

## 解析

[HJSON的Github主页](https://github.com/hjson/)已经开发了很多编程语言的第三库来帮助我们解析，比如 C++、Java、PHP、Python、Js、Go、C#等等，也提供了许多编译器插件，比如IntelliJ、VsCode、Visual Studio、Sublime Text、Vim等等。

下面使用Python举例：

`HJSON` 支持 Python 2.5+ 和 Python 3.3+ 。

### 安装

    pip install hjson

### 使用

和json库的API基本一致。

**解析字符串**

```python
import hjson
text = """{
  foo: a
  bar: 1
}"""

r = hjson.loads(text)
print r
# 结果返回一个字典
# OrderedDict([('foo', 'a'), ('bar', 1)])
```

**解析文件**

```python
import hjson
CONFIG_FILE = 'config.hjson'
with open(CONFIG_FILE) as f:
    json_dic = hjson.load(f)
    print json_dic
```

**字典转HJSON**

```python
import hjson
print hjson.dumps({'foo': 'text', 'bar': (1, 2)})
```

结果

```
{
  foo: text
  bar:
  [
    1
    2
  ]
}
```

**字典转JSON**

兼容Json，所以也提供了转化方法。

    print hjson.dumpsJSON(['foo', {'bar': ('baz', None, 1.0, 2)}])

结果

    '["foo", {"bar": ["baz", null, 1.0, 2]}]'

## 总结

总的来说 `HJSON` 作为配置文件还是很不错的，值得使用。