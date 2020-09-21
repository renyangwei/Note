# random 随机数

## 1. random()

用于生成一个 **0到1** 的随机符点数。

```python
import random
random.random()
0.04127678363114562
random.random()
0.9105887531333371
```

## 2. uniform(a, b)

用于生成一个指定范围内的随机符点数。a 和 b大小无所谓，但是一般把小的放前面。结果 `a <=n <=b`。

```python
import random
random.uniform(1, 5)
2.1073219192735704
random.uniform(5, 1)
4.144279193451686
```

## 3. randint(a, b)

用于生成一个指定范围内的整数。其中参数a是下限，参数b是上限，结果 `a <=n <=b`。

```python
import random
random.randint(1, 5)
3
random.randint(1, 5)
1
```

## 4. randrange(start, stop, step)

从指定范围内，按指定基数递增的集合中 获取一个随机数。

```python
import random
# 从[1,3,5,7,9] 中随机获取
random.randrange(1, 10, 2)
1
random.randrange(1, 10, 2)
5
```

## 5. choice(sequence)

从序列中获取一个随机元素。参数sequence表示一个有序类型。list, tuple, 字符串都属于sequence。

> 我理解为可迭代类型。

```python
import random
list3 = ['a', 'b', 'c', '4']
random.choice(list3)
'c'
random.choice(list3)
'4'
random.choice('hello')
'l'
random.choice('hello')
'o'
```

## 6. shuffle(x, random)

用于将一个列表中的元素打乱。

```python
import random
random.shuffle(list3)
print list3
['b', 'c', 'a', '4', '3']
```

## 7. sample(sequence, k)

从指定序列中随机获取指定长度的片断。sample函数不会修改原有序列。

```python
random.sample('abcdefghij',3) 
['e', 'i', 'f']
# 从a-zA-Z0-9生成指定数量的随机字符：
ran_str = ''.join(random.sample(string.ascii_letters + string.digits, 8))
print ran_str
```

