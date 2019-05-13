# JavaScript

## 依赖

同 `css` 一样，放到 `head` 标签里

main.js

```js
alert("Hello")
```

```html
<head>
  <script src="/static/js/abc.js"></script>
</head>
```

## 调试代码

在 Chrome 浏览器里按 **F12**，找到 Console 控制台，就可以直接输入JavaScript代码

## 语法

### 定义赋值

```js
var a = 1
var b = 2
var c = 0
d = 3 //全局变量，但是不要这么用
```

### 数据类型

- Number：不区分整型和浮点型
- 字符串：不区分单引号和双引号
- 布尔值：true/false
- 比较运算符：>,>=,==,===

`==`：自动转换数据类型再比较，很多时候，会得到非常诡异的结果

`===`：它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较

始终坚持使用 `===` 比较

`NaN` 这个特殊的Number与所有其他值都不相等，包括它自己

```js
NaN === NaN; // false
```

浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小数。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值

```js
Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true
```

多行字符串用反引号

```js
`这是
多行
字符串`
```

### null 和 undefined

JavaScript的设计者希望用 `null` 表示一个空的值，而 `undefined` 表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用 `null` 。`undefined` 仅仅在判断函数参数是否传递的情况下有用。

### 数组

JavaScript的数组可以包括任意数据类型。

```js
var arr = [1, 2, 3.14, 'Hello', null, true];
arr[0]; // 返回索引为0的元素，即1
arr[5]; // 返回索引为5的元素，即true
arr[6]; // 索引超出了范围，返回undefined
// 长度
arr.length // 6
arr.length = 7 //[1, 2, 3.14, 'Hello', null, true, nudefind]
aar.length = 2 // [1, 2]

```

直接给Array的length赋一个新的值会导致Array大小的变化

```js
var arr = [1, 2, 3.14, 'Hello', null, true];
arr.length = 7 //[1, 2, 3.14, 'Hello', null, true, nudefind]
aar.length = 2 // [1, 2]
```

Array可以通过索引把对应的元素修改为新的值，因此，对Array的索引进行赋值会直接修改这个Array

```js
var arr = ['A', 'B', 'C'];
arr[1] = 99;
arr; // arr现在变为['A', 99, 'C']
```

如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化

```js
var arr = [1, 2, 3];
arr[5] = 'x';
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

大多数其他编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何错误。在编写代码时，不建议直接修改Array的大小，访问索引时要确保索引不会越界。

**索引**

```js
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```

**切片**

```js
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
// 复制
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
// 起止参数包括开始索引，不包括结束索引
```

**push和pop**

`push()` 向Array的末尾添加若干元素，`pop()` 则把Array的最后一个元素删除掉

```js
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

**unshift和shift**

如果要往Array的头部添加若干元素，使用 `unshift()` 方法，`shift()` 方法则把Array的第一个元素删掉

```js
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

**sort**

`sort()` 可以对当前Array进行排序，它会直接修改当前Array的元素位置，直接调用时，按照默认顺序排序

```js
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
```

**reverse**

`reverse()` 把整个Array的元素反转

```js
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```

**splice**

`splice()` 方法是修改Array的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素

```js
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

**concat**

`concat()` 方法把当前的Array和另一个Array连接起来，并返回一个新的Array

```js
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```

`concat()` 方法并没有修改当前Array，而是返回了一个新的Array

**join**

`join()` 方法是一个非常实用的方法，它把当前Array的每个元素都用指定的字符串连接起来

```js
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```

如果Array的元素不是字符串，将自动转换为字符串后再连接

### 对象

JavaScript的对象是一组由键-值组成的无序集合,对象的键都是字符串类型，值可以是任意数据类型。

```js
var person = {
    name: "Bob",
    age: 20,
    hasCar: true,
    zipcode: null
}
person.name; // 'Bob'
person.zipcode; // null
```

还可以增加删除修改属性

```js
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

判断是否有某个属性

```js
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

**遍历对象**

貌似只能通过 `[]` 访问，不能通过 `.`
```js
for (var k in person) {
    console.log(k + ":" + person[k])
}
// name:Kury
// age:20
// hasCar:true
// zipcode:null
// d:1
```


### 操作字符串

```js
var s = "hello world"
// 长度
s.length// 11
// 索引
s[0]; // 'H'
s[6]; // ' '
s[7]; // 'w'
s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
// 转大小写
s.toUpperCase()
s.toLowerCase()
// 字符串位置
s.indexOf('world'); // 返回7
// 切割字符串
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
```

## 函数

### 定义

```js
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```

### arguments

指向当前函数的调用者传入的所有参数

```js
function foo(x) {
    console.log('x = ' + x); // 10
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10, 20, 30);
```

### rest参数

用于获得额外参数

```js
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]
```

### 名字空间

全局变量会绑定到window上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。

减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中

```js
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```

### 常量

```js
const PI = 3.14;
```

### 解构赋值

从ES6开始，JavaScript引入了解构赋值，可以同时对一组变量进行赋值

```js
var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
```

### 方法

```js
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
    }
};
xiaoming.age; // function xiaoming.age()
xiaoming.age(); // 今年调用是25,明年调用就变成26了
```

关于 `this`的处理，`getAgeFromBirth` 内部的 `this` 是 `undefined`，所以要处理。

```js
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var that = this; // 在方法内部一开始就捕获this
        function getAgeFromBirth() {
            var y = new Date().getFullYear();
            return y - that.birth; // 用that而不是this
        }
        return getAgeFromBirth();
    }
};

xiaoming.age(); // 25
```

### map/reduce

传入一个函数，将数组作为函数的参数

```js
function pow(x) {
    return x * x;
}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
var results = arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
console.log(results);
```

### 排序

`sort()` 方法会直接对Array进行修改，它返回的结果仍是当前Array

1.全是大写或者小写

```js
['Google', 'Apple', 'Microsoft'].sort(); 
// ['Apple', 'Google', 'Microsoft'];
```

2.不区分大小写

```js
var arr = ['Google', 'apple', 'Microsoft'];
arr.sort(function (s1, s2) {
    x1 = s1.toUpperCase();
    x2 = s2.toUpperCase();
    if (x1 < x2) {
        return -1;
    }
    if (x1 > x2) {
        return 1;
    }
    return 0;
});
// ['apple', 'Google', 'Microsoft']
```

3.数字

```js
var arr = [10, 20, 1, 2];
arr.sort(function (x, y) {
    if (x < y) {
        return 1;
    }
    if (x > y) {
        return -1;
    }
    return 0;
});
// [20, 10, 2, 1]
```

### 时间

```js
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2015, 年份
now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 24, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳

var d = new Date(1435146562875);
d; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
d.getMonth(); // 5
```

 > JavaScript的Date对象月份值从0开始，牢记0=1月，1=2月，2=3月，……，11=12月


### 正则表达式

| 字符 | 含义 |
|------|------|
| `\d` | 一个数字 |
| `\w` | 一个任意字符 |
| `.` | 一个字母或者数字 |
| `*` | 任意个（包括0）个字符 |
| `+` | 至少一个字符 |
| `?` | 0个或1个字符 |
| `{n}` | n个字符 |
| `{n,m}` | n-m个字符 |
| `\s` | 一个空格（也包括Tab等空白符） |
| `[]` | 表示范围 |
| `|` | 或， `A|B`匹配A或者B |
| `^` | 行的开头 |
| `$` | 行的结束 |


举例：

`\d{3}\s+\d{3,8}`

 三个数字，至少一个空格，三至八个数字

`[a-zA-Z\_\$][0-9a-zA-Z\_\$]{0, 19}`

1-20个字符（前面1个字符+后面最多19个字符）

`\_`表示 `_`，属于转义字符

```js
var re = /^\d{3}\-\d{3,8}$/;
re.test('010-12345'); // true
re.test('010-1234x'); // false
re.test('010 12345'); // false
```

### JSON序列化和反序列化

```js
// 序列化
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};
var s = JSON.stringify(xiaoming);

// 反序列化
JSON.parse('{"name":"小明","age":14}'); 
// Object {name: '小明', age: 14}
```

