# Json

主要使用四个函数。

- `dumps`：把数据类型转换成字符串，反序列化
- `dump`：把数据类型转换成字符串并存储在文件中
- `loads`：把字符串转换成数据类型 ，序列化
- `load`：把文件打开从字符串转换成数据类型



举例：

```python
import json

# 解析字符串用 loads，转为字典(如果是json数组则转为列表)
strs = '{"a": "1", "b": "2"}'
json.loads(strs)
# 解析文件或者网络用 load
with open('config.json') as load_f:
		load_dict = json.load(load_f)
		print(load_dict)
# 同理,解析字符串用dumps
dic = {'a': '1', 'b': 2}
json.dumps(dic)
# 写入文件用 dump
with open("record.json","w") as f:
		json.dump(dic,f)
```

