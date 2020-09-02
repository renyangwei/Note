- [JavaScript](#JavaScript)
  - [依赖](#%E4%BE%9D%E8%B5%96)
  - [调试代码](#%E8%B0%83%E8%AF%95%E4%BB%A3%E7%A0%81)
  - [语法](#%E8%AF%AD%E6%B3%95)
    - [定义赋值](#%E5%AE%9A%E4%B9%89%E8%B5%8B%E5%80%BC)
    - [数据类型](#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [null 和 undefined](#null-%E5%92%8C-undefined)
    - [数组](#%E6%95%B0%E7%BB%84)
    - [对象](#%E5%AF%B9%E8%B1%A1)
    - [操作字符串](#%E6%93%8D%E4%BD%9C%E5%AD%97%E7%AC%A6%E4%B8%B2)
  - [函数](#%E5%87%BD%E6%95%B0)
    - [定义](#%E5%AE%9A%E4%B9%89)
    - [arguments](#arguments)
    - [rest参数](#rest%E5%8F%82%E6%95%B0)
    - [名字空间](#%E5%90%8D%E5%AD%97%E7%A9%BA%E9%97%B4)
    - [常量](#%E5%B8%B8%E9%87%8F)
    - [解构赋值](#%E8%A7%A3%E6%9E%84%E8%B5%8B%E5%80%BC)
    - [方法](#%E6%96%B9%E6%B3%95)
    - [map/reduce](#mapreduce)
    - [排序](#%E6%8E%92%E5%BA%8F)
  - [时间](#%E6%97%B6%E9%97%B4)
  - [正则表达式](#%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [JSON序列化和反序列化](#JSON%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96)
  - [浏览器](#%E6%B5%8F%E8%A7%88%E5%99%A8)
    - [window](#window)
    - [navigator](#navigator)
    - [screen](#screen)
    - [location](#location)
    - [document](#document)
    - [history](#history)
    - [表单操作](#%E8%A1%A8%E5%8D%95%E6%93%8D%E4%BD%9C)
    - [文件操作](#%E6%96%87%E4%BB%B6%E6%93%8D%E4%BD%9C)
    - [AJax](#AJax)
  - [jQuery](#jQuery)
    - [表单相关](#%E8%A1%A8%E5%8D%95%E7%9B%B8%E5%85%B3)
    - [操作DOM](#%E6%93%8D%E4%BD%9CDOM)
    - [修改CSS](#%E4%BF%AE%E6%94%B9CSS)
    - [显示和隐藏](#%E6%98%BE%E7%A4%BA%E5%92%8C%E9%9A%90%E8%97%8F)
    - [获取DOM信息](#%E8%8E%B7%E5%8F%96DOM%E4%BF%A1%E6%81%AF)
    - [添加DOM](#%E6%B7%BB%E5%8A%A0DOM)
    - [删除节点](#%E5%88%A0%E9%99%A4%E8%8A%82%E7%82%B9)
    - [事件](#%E4%BA%8B%E4%BB%B6)
    - [jQuery 实现 AJAX](#jQuery-%E5%AE%9E%E7%8E%B0-AJAX)
  - [错误处理](#%E9%94%99%E8%AF%AF%E5%A4%84%E7%90%86)
    - [try ... catch ... finally](#try--catch--finally)

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

## 时间

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

## 浏览器

JavaScript可以获取浏览器提供的很多对象，并进行操作。

### window

`window` 对象不但充当全局作用域，而且表示浏览器窗口。

```js
// 获取内部宽高，内部宽高是指除去菜单栏、工具栏、边框等占位元素后，用于显示网页的净宽高。
window.innerWidth
window.innerHeight
// 获取浏览器窗口的整个宽高
window.outerWidth
window.outerHeight
```

### navigator

`navigator` 对象表示浏览器的信息，最常用的属性包括

- `navigator.appName`：浏览器名称；
- `navigator.appVersion`：浏览器版本；
- `navigator.language`：浏览器设置的语言；
- `navigator.platform`：操作系统类型；
- `navigator.userAgent`：浏览器设定的User-Agent字符串。

> navigator的信息可以很容易地被用户修改，所以JavaScript读取的值不一定是正确的

所以针对不同的浏览器，正确的方法是充分利用JavaScript对不存在属性返回 `undefined` 的特性，直接用短路运算符 `||` 计算

```js
var width = window.innerWidth || document.body.clientWidth;
```

### screen

`screen` 对象表示屏幕的信息，常用的属性有

- `screen.width`：屏幕宽度，以像素为单位；
- `screen.height`：屏幕高度，以像素为单位；
- `screen.colorDepth`：返回颜色位数，如8、16、24。

### location

location对象表示当前页面的URL信息

比如

    http://www.example.com:8080/path/index.html?a=1&b=2#TOP

要获得URL各个部分的值

```js
location.protocol; // 'http'
location.host; // 'www.example.com'
location.port; // '8080'
location.pathname; // '/path/index.html'
location.search; // '?a=1&b=2'
location.hash; // 'TOP'

//加载新页面
location.assign()
//重新加载界面
location.reload()
```

### document

表示当前页面

由于HTML在浏览器中以DOM形式表示为树形结构，`document` 对象就是整个DOM树的**根节点**

`document` 的 `title` 属性是从HTML文档中的`<title>xxx</title>`读取的，但是可以动态改变

    document.title = '努力学习JavaScript!';

运行这段代码网站的title就会变


操作DOM：

```js
// 返回ID为'test'的节点：
var test = document.getElementById('test');

// 先定位ID为'test-table'的节点，再返回其内部所有tr节点：
var trs = document.getElementById('test-table').getElementsByTagName('tr');

// 先定位ID为'test-div'的节点，再返回其内部所有class包含red的节点：
var reds = document.getElementById('test-div').getElementsByClassName('red');

// 获取节点test下的所有直属子节点:
var cs = test.children;

// 获取节点test下第一个、最后一个子节点：
var first = test.firstElementChild;
var last = test.lastElementChild;
```


### history

浏览器的历史记录

但是任何情况，你都不应该使用 `history` 这个对象

### 表单操作

```js
// <input type="text" id="email">
var input = document.getElementById('email');
input.value; // '用户输入的值'
// <label><input type="radio" name="weekday" id="monday" value="1"> Monday</label>
// <label><input type="radio" name="weekday" id="tuesday" value="2"> Tuesday</label>
var mon = document.getElementById('monday');
var tue = document.getElementById('tuesday');
mon.value; // '1'
tue.value; // '2'
mon.checked; // true或者false
tue.checked; // true或者false
```

### 文件操作

在HTML表单中，可以上传文件的唯一控件就是 `<input type="file">`

当一个表单包含 `<input type="file">` 时，表单的 `enctype` 必须指定为`multipart/form-data`，`method` 必须指定为 `post`，浏览器才能正确编码并以 `multipart/form-data` 格式发送表单的数据

```js
var f = document.getElementById('test-file-upload');
var filename = f.value; // 'C:\fakepath\test.png'
if (!filename || !(filename.endsWith('.jpg') || filename.endsWith('.png') || filename.endsWith('.gif'))) {
    alert('Can only upload image file.');
    return false;
}
```

读取文件内容

```js
var
    fileInput = document.getElementById('test-image-file'),
    info = document.getElementById('test-file-info'),
    preview = document.getElementById('test-image-preview');
// 监听change事件:
fileInput.addEventListener('change', function () {
    // 清除背景图片:
    preview.style.backgroundImage = '';
    // 检查文件是否选择:
    if (!fileInput.value) {
        info.innerHTML = '没有选择文件';
        return;
    }
    // 获取File引用:
    var file = fileInput.files[0];
    // 获取File信息:
    info.innerHTML = '文件: ' + file.name + '<br>' +
                     '大小: ' + file.size + '<br>' +
                     '修改: ' + file.lastModifiedDate;
    if (file.type !== 'image/jpeg' && file.type !== 'image/png' && file.type !== 'image/gif') {
        alert('不是有效的图片文件!');
        return;
    }
    // 读取文件:
    var reader = new FileReader();
    reader.onload = function(e) {
        var
            data = e.target.result; // 'data:image/jpeg;base64,/9j/4AAQSk...(base64编码)...'            
        preview.style.backgroundImage = 'url(' + data + ')';
    };
    // 以DataURL的形式读取文件:
    reader.readAsDataURL(file);
});
```

### AJax

```js
function success(text) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = text;
}

function fail(code) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = 'Error code: ' + code;
}

var request = new XMLHttpRequest(); // 新建XMLHttpRequest对象

request.onreadystatechange = function () { // 状态发生变化时，函数被回调
    if (request.readyState === 4) { // 成功完成
        // 判断响应结果:
        if (request.status === 200) {
            // 成功，通过responseText拿到响应的文本:
            return success(request.responseText);
        } else {
            // 失败，根据响应码判断失败原因:
            return fail(request.status);
        }
    } else {
        // HTTP请求还在继续...
    }
}

// 发送请求:
request.open('GET', '/api/categories');
request.send();

alert('请求已发送，请等待响应...');
```

## jQuery

 引入 jQuery 文件

 ```html
 <head>
    <script src="//code.jquery.com/jquery-1.11.3.min.js"></script>
</head>
 ```

 ### 选择器

 ```js
 // 按ID查找
 // 查找<div id="abc">:
 var div = $('#abc');

 //按tag查找
 var ps = $('p'); // 返回所有<p>节点
 ps.length; // 数一数页面有多少个<p>节点

 //按class查找
 var a = $('.red'); // 所有节点包含`class="red"`都将返回
// 例如:
// <div class="red">...</div>
// <p class="green red">...</p>

//组合查找
var tr = $('tr.red'); // 找出<tr class="red ...">...</tr>

//多项选择
$('p,div'); // 把<p>和<div>都选出来
$('p.red,p.green'); // 把<p class="red">和<p class="green">都选出来

//前缀查找或者后缀查
var icons = $('[name^=icon]'); // 找出所有name属性值以icon开头的DOM
// 例如: name="icon-1", name="icon-2"
var names = $('[name$=with]'); // 找出所有name属性值以with结尾的DOM
// 例如: name="startswith", name="endswith"
 $('p[class^="color-"]')//p元素color-前缀

 //层级选择器 用空格分开
 $('ul.lang li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
$('div.testing li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
$('form.test p input'); // 在form表单选择被<p>包含的<input>

//子选择器,类似层级选择器
$('ul.lang>li.lang-javascript'); // 可以选出[<li class="lang-javascript">JavaScript</li>]
$('div.testing>li.lang-javascript'); // [], 无法选出，因为<div>和<li>不构成父子关系

//过滤器,一般不单独使用，它通常附加在选择器上
$('ul.lang li'); // 选出JavaScript、Python和Lua 3个节点
$('ul.lang li:first-child'); // 仅选出JavaScript
$('ul.lang li:last-child'); // 仅选出Lua
$('ul.lang li:nth-child(2)'); // 选出第N个元素，N从1开始
$('ul.lang li:nth-child(even)'); // 选出序号为偶数的元素
$('ul.lang li:nth-child(odd)'); // 选出序号为奇数的元素
 ```

### 表单相关

针对表单元素，jQuery还有一组特殊的选择器

- `:input`：可以选择`<input>，<textarea>，<select>`和`<button>`；
- `:file`：可以选择`<input type="file">`，和`input[type=file]`一样；
- `:checkbox`：可以选择复选框，和`input[type=checkbox]`一样；
- `:radio`：可以选择单选框，和`input[type=radio]`一样；
- `:focus`：可以选择当前输入焦点的元素，例如把光标放到一个`<input>`上，用`$('input:focus')`就可以选出；
- `:checked`：选择当前勾上的单选框和复选框，用这个选择器可以立刻获得用户选择的项目，如`$('input[type=radio]:checked')`；
- `:enabled`：可以选择可以正常输入的`<input>、<select>` 等，也就是没有灰掉的输入；
- `:disabled`：和`:enabled`正好相反，选择那些不能输入的。

### 操作DOM

举例

```html
<!-- HTML结构 -->
<ul id="test-ul">
    <li class="js">JavaScript</li>
    <li name="book">Java &amp; JavaScript</li>
</ul>
```

无参数调用`text()`是获取文本，传入参数就变成设置文本，HTML也是类似操作

```js
//获取
$('#test-ul li[name=book]').text(); // 'Java & JavaScript'
$('#test-ul li[name=book]').html(); // 'Java &amp; JavaScript'
//设置
$('#test-ul li[name=book]').text("Python"); 
$('#test-ul li[name=book]').html("CSS");
```

一个jQuery对象可以包含0个或任意个DOM对象,即使获取的节点不存在也不会报错

### 修改CSS

jQuery对象的`css('name', 'value')`

举例

```html
<!-- HTML结构 -->
<ul id="test-css">
    <li class="lang dy"><span>JavaScript</span></li>
    <li class="lang"><span>Java</span></li>
    <li class="lang dy"><span>Python</span></li>
    <li class="lang"><span>Swift</span></li>
    <li class="lang dy"><span>Scheme</span></li>
</ul>
```

```js
$('#test-css li.dy span').css('background-color', '#ffd351').css('color', 'red');
```

其他用法

```js
//修改属性
var div = $('#test-div');
div.css('color'); // '#000033', 获取CSS属性
div.css('color', '#336699'); // 设置CSS属性
div.css('color', ''); // 清除CSS属性

//修改CSS
var div = $('#test-div');
div.hasClass('highlight'); // false， class是否包含highlight
div.addClass('highlight'); // 添加highlight这个class
div.removeClass('highlight'); // 删除highlight这个class
```

### 显示和隐藏

```js
var a = $('a[target=_blank]');
a.hide(); // 隐藏
a.show(); // 显示
```

### 获取DOM信息

```js
// 浏览器可视窗口大小:
$(window).width(); // 800
$(window).height(); // 600

// HTML文档大小:
$(document).width(); // 800
$(document).height(); // 3500

// 某个div的大小:
var div = $('#test-div');
div.width(); // 600
div.height(); // 300
div.width(400); // 设置CSS属性 width: 400px，是否生效要看CSS是否有效
div.height('200px'); // 设置CSS属性 height: 200px，是否生效要看CSS是否有效
```

### 添加DOM

```js
//方式一
var ul = $('#test-div>ul');
ul.append('<li><span>Haskell</span></li>');

//方式二
// 创建DOM对象:
var ps = document.createElement('li');
ps.innerHTML = '<span>Pascal</span>';
// 添加DOM对象:
ul.append(ps);
// 添加jQuery对象:
ul.append($('#scheme'));
// 添加函数对象:
ul.append(function (index, html) {
    return '<li><span>Language - ' + index + '</span></li>';
});
```

### 删除节点

```js
var li = $('#test-div>ul>li');
li.remove(); // 所有<li>全被删除
```

### 事件

**点击**

```js
/* HTML:
 *
 * <a id="test-link" href="#0">点我试试</a>
 *
 */

// 获取超链接的jQuery对象:
var a = $('#test-link');
a.on('click', function () {
    alert('Hello!');
});

// 更常见的写法
a.click(function () {
    alert('Hello!');
});
```

**绑定 from 表单**

```html
<html>
<head>
    <script>
        $(document).on('ready', function () {
            $('#testForm).on('submit', function () {
                alert('submit!');
            });
        });
        // 更常见的写法
        $(function () {
            // init...
        });
    });
    </script>
    
</head>
<body>
    <form id="testForm">
        ...
    </form>
</body>
```

**取消绑定**

```js
function hello() {
    alert('hello!');
}

a.click(hello); // 绑定事件

// 10秒钟后解除绑定:
setTimeout(function () {
    a.off('click', hello);
}, 10000);
```

### jQuery 实现 AJAX

    $.ajax(url, settings)

`settings`对象:

- `async`：是否异步执行AJAX请求，默认为true，千万不要指定为false
- `method`：发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等
- `contentType`：发送POST请求的格式，默认值为`'application/x-www-form-urlencoded; charset=UTF-8'`，也可以指定为`text/plain`、`application/json`
- `data`：发送的数据，可以是字符串、数组或object。如果是`GET`请求，data将被转换成query附加到URL上，如果是POST请求，根据contentType把data序列化成合适的格式
- `headers`：发送的额外的HTTP头，必须是一个object
- `dataType`：接收的数据格式，可以指定为`'html'`、`'xml'`、`'json'`、`'text'`等，缺省情况下根据响应的Content-Type猜测

举例：

```js
var jqxhr = $.ajax('/api/categories', {
    dataType: 'json'
}).done(function (data) {
    ajaxLog('成功, 收到的数据: ' + JSON.stringify(data));
}).fail(function (xhr, status) {
    ajaxLog('失败: ' + xhr.status + ', 原因: ' + status);
}).always(function () {
    ajaxLog('请求完成: 无论成功或失败都会调用');
});
```

**Get**

第二个参数如果是object，jQuery自动把它变成query string然后加到URL后面

    /path/to/resource?name=Bob%20Lee&check=1

举例：

```js
var jqxhr = $.get('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```

**Post**

第二个参数默认被序列化为`application/x-www-form-urlencoded`

```js
var jqxhr = $.post('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```

**getJson**

```js
var jqxhr = $.getJSON('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
}).done(function (data) {
    // data已经被解析为JSON对象了
});
```

## 错误处理

### try ... catch ... finally

```js
var r1, r2, s = null;
try {
    r1 = s.length; // 此处应产生错误
    r2 = 100; // 该语句不会执行
} catch (e) {
    console.log('出错了：' + e);
} finally {
    console.log('finally');
}
console.log('r1 = ' + r1); // r1应为undefined
console.log('r2 = ' + r2); // r2应为undefined
```

