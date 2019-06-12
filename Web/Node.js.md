# Node.js

一个基于`JavaScript`语言和`V8`引擎的开源Web服务器项目

## 安装

[官网](https://nodejs.org/en/)

Windows勾选 `Add to Path`

输入

    node -v

看到版本信息表示安装成功

## npm

npm其实是Node.js的包管理工具（package manager）

## 第一个Node程序

hello.js

```js
'use strict';
console.log('Hello, world.');
```

执行

    node hello.js

让Node直接为所有js文件开启严格模式

    node --use_strict calc.js

