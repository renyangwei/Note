# MD5

```python
# Python3
# 导入
import hashlib
# 创建md5对象
str = 'hello'
str_md5 = hashlib.md5(str.encode(encoding='utf-8')).hexdigest()
```

