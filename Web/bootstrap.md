- [bootstrap](#bootstrap)
  - [1.1 下载](#11-%E4%B8%8B%E8%BD%BD)
  - [1.2 Bootstrap CSS](#12-Bootstrap-CSS)
    - [1.2.1 概览](#121-%E6%A6%82%E8%A7%88)
    - [1.2.2 排版](#122-%E6%8E%92%E7%89%88)
    - [1.2.3 表格](#123-%E8%A1%A8%E6%A0%BC)
    - [1.2.4 表单](#124-%E8%A1%A8%E5%8D%95)
    - [1.2.5 按钮](#125-%E6%8C%89%E9%92%AE)
    - [1.2.6 图片](#126-%E5%9B%BE%E7%89%87)
  - [1.3 布局组件](#13-%E5%B8%83%E5%B1%80%E7%BB%84%E4%BB%B6)
    - [1.3.1 下拉菜单](#131-%E4%B8%8B%E6%8B%89%E8%8F%9C%E5%8D%95)
    - [1.3.2 按钮下拉菜单](#132-%E6%8C%89%E9%92%AE%E4%B8%8B%E6%8B%89%E8%8F%9C%E5%8D%95)
    - [1.3.3 输入框组](#133-%E8%BE%93%E5%85%A5%E6%A1%86%E7%BB%84)
    - [1.3.4 导航元素](#134-%E5%AF%BC%E8%88%AA%E5%85%83%E7%B4%A0)
    - [1.3.6 分页](#136-%E5%88%86%E9%A1%B5)
    - [1.3.7 超大屏幕（Jumbotron）](#137-%E8%B6%85%E5%A4%A7%E5%B1%8F%E5%B9%95Jumbotron)
    - [1.3.8 页面标题（Page Header）](#138-%E9%A1%B5%E9%9D%A2%E6%A0%87%E9%A2%98Page-Header)
    - [1.3.9 警告（Alerts）](#139-%E8%AD%A6%E5%91%8AAlerts)
  - [1.4 插件](#14-%E6%8F%92%E4%BB%B6)
    - [1.4.1 过渡效果（Transition）插件](#141-%E8%BF%87%E6%B8%A1%E6%95%88%E6%9E%9CTransition%E6%8F%92%E4%BB%B6)
    - [1.4.2 模态框（Modal）插件](#142-%E6%A8%A1%E6%80%81%E6%A1%86Modal%E6%8F%92%E4%BB%B6)
    - [1.4.3 滚动监听（Scrollspy）](#143-%E6%BB%9A%E5%8A%A8%E7%9B%91%E5%90%ACScrollspy)

# bootstrap

Bootstrap 是最受欢迎的 HTML、CSS 和 JS 框架，用于开发响应式布局、移动设备优先的 WEB 项目。

## 1.1 下载

[官网下载地址](https://v3.bootcss.com/getting-started/#download)

下载页有很多模版可供选择，我们下载下来，然后修修改改基本可以搞定一个简单的网站

或者使用线上资源

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" rel="stylesheet">

     <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"></script>

    <!-- 建议使用国内CDN -->
     <!-- 新 Bootstrap 核心 CSS 文件 -->
  <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
  <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
  <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
  <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
  <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
      <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

   
  </body>
</html>
```

## 1.2 Bootstrap CSS

### 1.2.1 概览

Bootstrap 使用了一些 HTML5 元素和 CSS 属性，所以请使用HTML5 文档类型（Doctype）

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
</html>
```

为了让 Bootstrap 开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 `viewport meta` 标签

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`width` 属性控制设备的宽度

`initial-scale=1.0` 确保网页加载时，以 1:1 的比例呈现，不会有任何的缩放

通过添加 `img-responsive` 可以让 Bootstrap 3 中的图像对响应式布局的支持更友好

```html
<img src="..." class="img-responsive" alt="响应式图像">
```

`img-responsive` 的属性 ：

```css
.img-responsive {
  display: inline-block;
  height: auto;
  max-width: 100%;
}
```

### 1.2.2 排版

如果需要向任何标题添加一个内联子标题，只需要简单地在元素两旁添加 `<small>`，或者添加 `.small class`，这样子您就能得到一个字号更小的颜色更浅的文本

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 内联子标题</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>
   <h1>我是标题1 h1. <small>我是副标题1 h1</small></h1> 
   <h2>我是标题2 h2. <small>我是副标题2 h2</small></h2>
   <h3>我是标题3 h3. <small>我是副标题3 h3</small></h3>
   <h4>我是标题4 h4. <small>我是副标题4 h4</small></h4>
   <h5>我是标题5 h5. <small>我是副标题5 h5</small></h5>
   <h6>我是标题6 h6. <small>我是副标题6 h6</small></h6>
</body>
</html>
```

Bootstrap 提供了一些用于强调文本的类

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 强调</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<small>本行内容是在标签内</small>

<strong>本行内容是在标签内</strong>

<em>本行内容是在标签内，并呈现为斜体</em>

<p class="text-left">向左对齐文本</p>
<p class="text-center">居中对齐文本</p>
<p class="text-right">向右对齐文本</p>
<p class="text-muted">本行内容是减弱的</p>
<p class="text-primary">本行内容带有一个 primary class</p>
<p class="text-success">本行内容带有一个 success class</p>
<p class="text-info">本行内容带有一个 info class</p>
<p class="text-warning">本行内容带有一个 warning class</p>
<p class="text-danger">本行内容带有一个 danger class</p>

</body>
</html>
```

使用 `<address>` 标签，您可以在网页上显示联系信息

```html
<!DOCTYPE html><html><head>
   <title>Bootstrap 实例 - 地址</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script></head><body><address>
  <strong>Some Company, Inc.</strong>

  007 street

  Some City, State XXXXX

  <abbr title="Phone">P:</abbr> (123) 456-7890</address><address>
  <strong>Full Name</strong>

  <a href="mailto:#">mailto@somedomain.com</a></address>
</body>
</html>
```

您可以在任意的 HTML 文本旁使用默认的 `<blockquote>`

```html
<!DOCTYPE html><html><head>
   <title>Bootstrap 实例 - 引用</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>
<blockquote><p>这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。这是一个默认的引用实例。</p></blockquote>
<blockquote>这是一个带有源标题的引用。<small>Someone famous in <cite title="Source Title">Source Title</cite></small></blockquote>
<blockquote class="pull-right">这是一个向右对齐的引用。<small>Someone famous in <cite title="Source Title">Source Title</cite></small></blockquote>
</body>
</html>
```

Bootstrap 支持有序列表、无序列表和定义列表

```html
<!DOCTYPE html><html><head>
   <title>Bootstrap 实例 - 列表</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script></head><body><h4>有序列表</h4><ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li></ol><h4>无序列表</h4><ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li></ul><h4>未定义样式列表</h4><ul class="list-unstyled">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li></ul><h4>内联列表</h4><ul class="list-inline">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li></ul><h4>定义列表</h4><dl>
  <dt>Description 1</dt>
  <dd>Item 1</dd>
  <dt>Description 2</dt>
  <dd>Item 2</dd></dl><h4>水平的定义列表</h4><dl class="dl-horizontal">
  <dt>Description 1</dt>
  <dd>Item 1</dd>
  <dt>Description 2</dt>
  <dd>Item 2</dd></dl></body></html>
```

Bootstrap 允许您以两种方式显示代码： `<code>` 和 `<pre>` 标签

```html
<!DOCTYPE html>
<html>
<head>
  <title>Bootstrap 实例 - 代码</title>
  <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
  <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
  <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<p><code>&lt;header&gt;</code> 作为内联元素被包围。</p>
<p>如果需要把代码显示为一个独立的块元素，请使用 <pre> 标签：</p>
<pre>
  &lt;article&gt;
    &lt;h1&gt;Article Heading&lt;/h1&gt;
  &lt;/article&gt;
</pre>
</body>
</html>
```

### 1.2.3 表格

Bootstrap 提供了一个清晰的创建表格的布局

| 类  | 描述 |
|---|---|
| .table  | 为任意 `<table>` 添加基本样式 (只有横向分隔线) |
| .table-striped  | 在 `<tbody>` 内添加斑马线形式的条纹 ( IE8 不支持) |
| .table-bordered  | 为所有表格的单元格添加边框 |
| .table-hover  | 在 `<tbody>` 内的任一行启用鼠标悬停状态 |
| .table-condensed  | 让表格更加紧凑 |

下表的类可用于表格的行或者单元格，`<tr>`, `<th>` 和 `<td>`

| 类  | 描述  |
|---|---|
| .active  | 将悬停的颜色应用在行或者单元格上  |
| .success  | 表示成功的操作  |
| .info  | 表示信息变化的操作  |
| .warning  | 表示一个警告的操作  |
| .danger  | 	表示一个危险的操作  |

通过把任意的 .table 包在 .table-responsive class 内，您可以让表格水平滚动以适应小型设备

举例：

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 悬停表格</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <div class="table-responsive">
        <table class="table table-hover table-striped">
            <caption>悬停表格布局</caption>
            <thead>
                <tr>
                    <th>名称</th>
                    <th>城市</th>
                    <th>密码</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Tanmay</td>
                    <td>Bangalore</td>
                    <td>560001</td>
                </tr>
                <tr class="success">
                    <td>Sachin</td>
                    <td>Mumbai</td>
                    <td>400003</td>
                </tr>
                <tr>
                    <td>Uma</td>
                    <td>Pune</td>
                    <td>411027</td>
                </tr>
                <tr>
                    <td>Tan</td>
                    <td>Shenz</td>
                    <td>411956</td>
                </tr>
            </tbody>
        </table>
    </div>
</body>

</html>
```

### 1.2.4 表单

Bootstrap 提供了下列类型的表单布局：

- 垂直表单（默认）
- 内联表单
- 水平表单

创建基本表单的步骤：

- 向父 `<form>` 元素添加 role="form"。
- 把标签和控件放在一个带有 `class .form-group` 的 `<div>` 中。这是获取最佳间距所必需的。
- 向所有的文本元素 `<input>`、`<textarea>` 和 `<select>` 添加 `class .form-control`。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 基本表单</title>
    <link rel="stylesheet" href="//apps.bdimg.com/libs/bootstrap/3.3.0/css/bootstrap.min.css">
    <script src="//apps.bdimg.com/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="//apps.bdimg.com/libs/bootstrap/3.3.0/js/bootstrap.min.js"></script>
</head>

<body>
    <form role="form">
        <div class="form-group">
            <label for="name">名称</label>
            <input type="text" class="form-control" id="name" placeholder="请输入名称">
        </div>
        <div class="form-group">
            <label for="inputfile">文件输入</label>
            <input type="file" id="inputfile">
            <p class="help-block">这里是块级帮助文本的实例。</p>
        </div>
        <div class="checkbox">
            <label>
                <input type="checkbox"> 请打勾 </label>
        </div>
        <button type="submit" class="btn btn-default">提交</button>
    </form>
</body>

</html>
```

### 1.2.5 按钮

任何带有 `class .btn` 的元素都会继承圆角灰色按钮的默认外观。但是 Bootstrap 提供了一些选项来定义按钮的样式

以下样式可用于 `<a>`, `<button>`, 或 `<input>` 元素上， 但是建议您在 `<button>` 元素上使用按钮 class，避免跨浏览器的不一致性问题

| 类  | 描述  |
|---|---|
| .btn  | 为按钮添加基本样式  |
| .btn-default  | 默认/标准按钮  |
| .btn-primary  | 原始按钮样式（未被操作）  |
| .btn-success  | 表示成功的动作  |
| .btn-info  | 该样式可用于要弹出信息的按钮  |
| .btn-warning  | 表示需要谨慎操作的按钮  |
| .btn-danger  | 表示一个危险动作的按钮操作  |
| .btn-link  | 让按钮看起来像个链接 (仍然保留按钮行为)  |
| .btn-lg  | 	制作一个大按钮  |
| .btn-sm  | 制作一个小按钮  |
| .btn-xs  | 制作一个超小按钮  |
| .btn-block  | 块级按钮(拉伸至父元素100%的宽度)  |
| .active  | 按钮被点击  |
| .disabled | 	禁用按钮 |
| .btn-block | 这会创建块级的按钮，会横跨父元素的全部宽度 |

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 按钮选项</title>
    <link rel="stylesheet" href="//apps.bdimg.com/libs/bootstrap/3.3.0/css/bootstrap.min.css">
    <script src="//apps.bdimg.com/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="//apps.bdimg.com/libs/bootstrap/3.3.0/js/bootstrap.min.js"></script>
    <script type="text/javascript">
        function callme() {
            $(".btn-success").addClass("disabled")
        }
    </script>
</head>

<body>
    <!-- 标准的按钮 -->
    <button type="button" class="btn btn-default" onclick="callme()">默认按钮</button>
    <!-- 提供额外的视觉效果，标识一组按钮中的原始动作 -->
    <button type="button" class="btn btn-primary">原始按钮</button>
    <!-- 表示一个成功的或积极的动作 -->
    <button type="button" class="btn btn-success">成功按钮</button>
    <!-- 信息警告消息的上下文按钮 -->
    <button type="button" class="btn btn-info">信息按钮</button>
    <!-- 表示应谨慎采取的动作 -->
    <button type="button" class="btn btn-warning">警告按钮</button>
    <!-- 表示一个危险的或潜在的负面动作 -->
    <button type="button" class="btn btn-danger">危险按钮</button>
    <!-- 并不强调是一个按钮，看起来像一个链接，但同时保持按钮的行为 -->
    <button type="button" class="btn btn-link">链接按钮</button>

    <button type="button" class="btn disabled">不可点击按钮</button>

    <button type="button" class="btn btn-info active">被点击按钮</button>
</body>

</html>
```

### 1.2.6 图片

Bootstrap 提供了三个可对图片应用简单样式的 class：

- `.img-rounded`：添加 border-radius:6px 来获得图片圆角。
- `.img-circle`：添加 border-radius:500px 来让整个图片变成圆形。
- `.img-thumbnail`：添加一些内边距（padding）和一个灰色的边框，可用于缩略图。
- `.img-responsive`：让图片支持响应式设计

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 图片</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<img src="https://www.w3cschool.cn/statics/demosource/download.png" class="img-rounded">
<img src="https://www.w3cschool.cn/statics/demosource/download.png" class="img-circle">
<img src="https://www.w3cschool.cn/statics/demosource/download.png" class="img-thumbnail">
<img src="cinqueterre.jpg" class="img-responsive" alt="Cinque Terre">

</body>
</html>
```

## 1.3 布局组件

### 1.3.1 下拉菜单

下拉菜单是可切换的，以列表格式显示链接的上下文菜单

如需使用下拉菜单，只需要在 `class .dropdown` 内加上下拉菜单即可

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 下拉菜单（Dropdowns）</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <div class="dropdown">
        <button type="button" class="btn dropdown-toggle" id="dropdownMenu1" data-toggle="dropdown">
            主题 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
            <li role="presentation">
                <a role="menuitem" tabindex="-1" href="#">Java</a>
            </li>
            <li role="presentation">
                <a role="menuitem" tabindex="-1" href="#">数据挖掘</a>
            </li>
            <li role="presentation">
                <a role="menuitem" tabindex="-1" href="#">
                    数据通信/网络 </a>
            </li>
            <li role="presentation" class="divider"></li>
            <li role="presentation">
                <a role="menuitem" tabindex="-1" href="#">分离的链接</a>
            </li>
        </ul>
    </div>
</body>

</html>
```

### 1.3.2 按钮下拉菜单

如需向按钮添加下拉菜单，只需要简单地在在一个 `.btn-group` 中放置按钮和下拉菜单即可。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 基本的按钮下拉菜单</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>

    <div class="btn-group">
        <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            默认 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" role="menu">
            <li><a href="#">功能</a></li>
            <li><a href="#">另一个功能</a></li>
            <li><a href="#">其他</a></li>
            <li class="divider"></li>
            <li><a href="#">分离的链接</a></li>
        </ul>
    </div>
    <div class="btn-group">
        <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
            原始 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" role="menu">
            <li><a href="#">功能</a></li>
            <li><a href="#">另一个功能</a></li>
            <li><a href="#">其他</a></li>
            <li class="divider"></li>
            <li><a href="#">分离的链接</a></li>
        </ul>
    </div>

</body>

</html>
```

### 1.3.3 输入框组

输入框组扩展自 表单控件。使用输入框组，您可以很容易地向基于文本的输入框添加作为前缀和后缀的文本或按钮。

向 `.form-control` 添加前缀或后缀元素的步骤如下：

- 把前缀或后缀元素放在一个带有 `class .input-group` 的 `<div>` 中。
- 接着，在相同的 `<div>` 内，在 class 为 .input-group-addon 的 `<span>` 内放置额外的内容。
- 把该 `<span>` 放置在 `<input>` 元素的前面或者后面。

请避免使用 `<select>` 元素，因为它们在 WebKit 浏览器中不能完全渲染出效果

您可以通过向 .input-group 添加相对表单大小的 class（比如 `.input-group-lg`、`input-group-sm`、`input-group-xs`）来改变输入框组的大小

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 基本的输入框组</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>

    <script type="text/javascript">
        function changeText() {
            // 获取输入内容
            console.log($("#twitter").val())
        }
    </script>
</head>

<body>
    <div style="padding: 100px 100px 10px">
        <form class="bs-example bs-example-form" role="form">
            <div class="input-group input-group-lg">
                <span class="input-group-addon">@</span>
                <input id="twitter" type="text" class="form-control" placeholder="twitterhandle" onchange="changeText()">
            </div>

            <div class="input-group">
                <input type="text" class="form-control">
                <span class="input-group-addon">.00</span>
            </div>

            <div class="input-group">
                <span class="input-group-addon">$</span>
                <input type="text" class="form-control">
                <span class="input-group-addon">.00</span>
            </div>
        </form>
    </div>
</body>

</html>
```

### 1.3.4 导航元素

创建一个标签式的导航菜单：

- 以一个带有 class `.nav` 的无序列表开始
- 添加 class `.nav-tabs`

 ```html
 <!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 标签式的导航菜单</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <p>标签式的导航菜单</p>
    <ul class="nav nav-tabs">
        <li class="active"><a href="#">Home</a></li>
        <li><a href="#">SVN</a></li>
        <li><a href="#">iOS</a></li>
        <li><a href="#">VB.Net</a></li>
        <li><a href="#">Java</a></li>
        <li><a href="#">PHP</a></li>
    </ul>
</body>

</html>
 ```

 ### 1.3.5 导航栏

 导航栏是一个很好的功能，是 Bootstrap 网站的一个突出特点。导航栏在您的应用或网站中作为导航页头的响应式基础组件。

 创建一个默认的导航栏的步骤如下：

- 向 `<nav>` 标签添加 class `.navbar`、`.navbar-default`。
- 向上面的元素添加 `role="navigation"`，有助于增加可访问性。
- 向 `<div>` 元素添加一个标题 class `.navbar-header`，内部包含了带有 class navbar-brand 的 `<a>` 元素。这会让文本看起来更大一号。
- 为了向导航栏添加链接，只需要简单地添加带有 class `.nav`、`.navbar-nav` 的无序列表即可。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 默认的导航栏</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <nav class="navbar navbar-default" role="navigation">
        <div class="navbar-header">
            <a class="navbar-brand" href="#">W3Cschool</a>
        </div>
        <div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">iOS</a></li>
                <li><a href="#">SVN</a></li>
                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                        Java
                        <b class="caret"></b>
                    </a>
                    <ul class="dropdown-menu">
                        <li><a href="#">jmeter</a></li>
                        <li><a href="#">EJB</a></li>
                        <li><a href="#">Jasper Report</a></li>
                        <li class="divider"></li>
                        <li><a href="#">分离的链接</a></li>
                        <li class="divider"></li>
                        <li><a href="#">另一个分离的链接</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </nav>
</body>

</html>
```

### 1.3.6 分页

分页（Pagination），是一种无序列表，Bootstrap 像处理其他界面元素一样处理分页。

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 分页的状态</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<ul class="pagination">
  <li><a href="#">&laquo;</a></li>
  <li class="active"><a href="#">1</a></li>
  <li class="disabled"><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>

</body>
</html>
```

class列表

| Class  | 描述  |
|---|---|
| .pagination  | 添加该 class 来在页面上显示分页 |
| .disabled, .active | 您可以自定义链接，通过使用 .disabled 来定义不可点击的链接，通过使用 .active 来指示当前的页面。 |
| .pagination-lg, .pagination-sm | 使用这些 class 来获取不同大小的项。 |


### 1.3.7 超大屏幕（Jumbotron）

顾名思义该组件可以增加标题的大小，并为登陆页面内容添加更多的外边距（margin）。使用超大屏幕（Jumbotron）的步骤如下：

- 创建一个带有 class `.jumbotron` 的容器 `<div>`。
- 除了更大的 `<h1>`，字体粗细` font-weight` 被减为200px。

举例：居中的登陆页

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 超大屏幕（Jumbotron）</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<div class="container">
   <div class="jumbotron">
      <h1>欢迎登陆页面！</h1>
      <p>这是一个超大屏幕（Jumbotron）的实例。</p>
      <p><a class="btn btn-primary btn-lg" role="button">
         学习更多</a>
      </p>
   </div>
</div>

</body>
</html>
```

占满全屏的登陆页

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 超大屏幕（Jumbotron）</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<div class="jumbotron">
   <div class="container">
      <h1>欢迎登陆页面！</h1>
      <p>这是一个超大屏幕（Jumbotron）的实例。</p>
      <p><a class="btn btn-primary btn-lg" role="button">
         学习更多</a>
      </p>
   </div>
</div>

</body>
</html>
```

### 1.3.8  页面标题（Page Header）

当一个网页中有多个标题且每个标题之间需要添加一定的间距时，页面标题这个功能就显得特别有用。

```html
<!DOCTYPE html>
<html>
<head>
   <title>Bootstrap 实例 - 页面标题</title>
   <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
   <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
   <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>
<body>

<div class="page-header">
   <h1>页面标题实例
      <small>子标题</small>
   </h1>
</div>
<p>这是一个示例文本。这是一个示例文本。这是一个示例文本。这是一个示例文本。这是一个示例文本。</p>


</body>
</html>
```

### 1.3.9 警告（Alerts）

警告（Alerts）向用户提供了一种定义消息样式的方式。

您可以通过创建一个 `<div>`，并向其添加一个 `.alert` class 和四个上下文 class（即 `.alert-success`、`.alert-info`、`.alert-warning`、`.alert-danger`）之一，来添加一个基本的警告框，添加 `alert-dismissable` 可以为其添加关闭按钮。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 可取消的警告（Dismissal Alerts）</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <div class="alert alert-success alert-dismissable">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">
            &times; </button>
        成功！很好地完成了提交。</div>
    <div class="alert alert-info alert-dismissable">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">
            &times; </button>
        信息！请注意这个信息。</div>
    <div class="alert alert-warning alert-dismissable">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">
            &times; </button>
        警告！请不要提交。</div>
    <div class="alert alert-danger alert-dismissable">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">
            &times; </button>
        错误！请进行一些更改。</div>
</body>

</html>
```

## 1.4 插件

Bootstrap 自带 12 种 jQuery 插件，扩展了功能，可以给站点添加更多的互动。

### 1.4.1 过渡效果（Transition）插件

Bootstrap 的 Transition 插件可以实现过渡效果，Transition 动画比较平滑，使用起来比较方便和灵活，并且对资源的消耗比较少。

过渡效果（Transition）插件提供了简单的过渡效果。


### 1.4.2 模态框（Modal）插件

模态框（Modal）是覆盖在父窗体上的子窗体。通常，目的是显示来自一个单独的源的内容，可以在不离开父窗体的情况下有一些互动。子窗体可提供信息、交互等。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 模态框（Modal）插件事件</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>
    <h2>模态框（Modal）插件事件</h2><!-- 按钮触发模态框 --><button class="btn btn-primary btn-lg" data-toggle="modal"
        data-target="#myModal">
        开始演示模态框</button><!-- 模态框（Modal） -->
    <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-hidden="true">× </button>
                    <h4 class="modal-title" id="myModalLabel">
                        模态框（Modal）标题 </h4>
                </div>
                <div class="modal-body">
                    点击关闭按钮检查事件功能。 </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">
                        关闭 </button>
                    <button type="button" class="btn btn-primary">
                        提交更改 </button>
                </div>
            </div><!-- /.modal-content -->
        </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
    <script>
        $(function () { $('#myModal').modal('hide') });</script>
    <script>
        $(function () {
            $('#myModal').on('hide.bs.modal', function () {
                alert('嘿，我听说您喜欢模态框...');
            })
        });</script>
</body>

</html>
```

代码讲解：

- 触发器是按钮，`data-target="#myModal"` 是您想要在页面上加载的模态框的目标
- `.modal`用来把 `<div>` 的内容识别为模态框
- 当模态框被切换时，`.fade` 会引起内容淡入淡出
- `aria-labelledby="myModalLabel"`，该属性引用模态框的标题
- 属性 `aria-hidden="true"` 用于保持模态窗口不可见，直到触发器被触发为止（比如点击在相关的按钮上）
- `class="close"`，close 是一个 CSS class，用于为模态窗口的关闭按钮设置样式
- `data-dismiss="modal"`，是一个自定义的 HTML5 data 属性，在这里它被用于关闭模态窗口
- `data-toggle="modal"`，HTML5 自定义的 data 属性 data-toggle 用于打开模态窗口。

下表列出了模态框中要用到事件。这些事件可在函数中当钩子使用。

| 事件  | 	描述  |
|---|---|
| show.bs.modal  | 在调用 show 方法后触发。  |
| shown.bs.modal | 当模态框对用户可见时触发（将等待 CSS 过渡效果完成）。 |
| hide.bs.modal | 当调用 hide 实例方法时触发。 |
| hidden.bs.modal | 当模态框完全对用户隐藏时触发。 |


### 1.4.3 滚动监听（Scrollspy）

滚动监听（Scrollspy）插件，即自动更新导航插件，会根据滚动条的位置自动更新对应的导航目标。其基本的实现是随着您的滚动，基于滚动条的位置向导航栏添加 `.active` class。

**用法**

通过 data 属性：向您想要监听的元素（通常是 body）添加 `data-spy="scroll"`。然后添加带有 Bootstrap `.nav` 组件的父元素的 ID 或 class 的属性` data-target`。为了它能正常工作，您必须确保页面主体中有匹配您所要监听链接的 ID 的元素存在。

```html
<!DOCTYPE html>
<html>

<head>
    <title>Bootstrap 实例 - 滚动监听（Scrollspy）插件</title>
    <link href="//cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    <script src="//cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="//cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</head>

<body>

    <nav id="navbar-example" class="navbar navbar-default navbar-static" role="navigation">
        <div class="navbar-header">
            <button class="navbar-toggle" type="button" data-toggle="collapse" data-target=".bs-js-navbar-scrollspy">
                <span class="sr-only">切换导航</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">教程名称</a>
        </div>
        <div class="collapse navbar-collapse bs-js-navbar-scrollspy">
            <ul class="nav navbar-nav">
                <li><a href="#ios">iOS</a></li>
                <li><a href="#svn">SVN</a></li>
                <li class="dropdown">
                    <a href="#" id="navbarDrop1" class="dropdown-toggle" data-toggle="dropdown">Java
                        <b class="caret"></b>
                    </a>
                    <ul class="dropdown-menu" role="menu" aria-labelledby="navbarDrop1">
                        <li><a href="#jmeter" tabindex="-1">jmeter</a></li>
                        <li><a href="#ejb" tabindex="-1">ejb</a></li>
                        <li class="divider"></li>
                        <li><a href="#spring" tabindex="-1">spring</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </nav>
    <div data-spy="scroll" data-target="#navbar-example" data-offset="0"
        style="height:200px;overflow:auto; position: relative;">
        <h4 id="ios">iOS</h4>
        <p>iOS 是一个由苹果公司开发和发布的手机操作系统。最初是于 2007 年首次发布 iPhone、iPod Touch 和 Apple
            TV。iOS 派生自 OS X，它们共享 Darwin 基础。OS X 操作系统是用在苹果电脑上，iOS 是苹果的移动版本。
        </p>
        <h4 id="svn">SVN</h4>
        <p>Apache Subversion，通常缩写为 SVN，是一款开源的版本控制系统软件。Subversion 由 CollabNet 公司在 2000 年创建。但是现在它已经发展为 Apache Software
            Foundation 的一个项目，因此拥有丰富的开发人员和用户社区。
        </p>
        <h4 id="jmeter">jMeter</h4>
        <p>jMeter 是一款开源的测试软件。它是 100% 纯 Java 应用程序，用于负载和性能测试。
        </p>
        <h4 id="ejb">EJB</h4>
        <p>Enterprise Java Beans（EJB）是一个创建高度可扩展性和强大企业级应用程序的开发架构，部署在兼容应用程序服务器（比如 JBOSS、Web Logic 等）的 J2EE 上。
        </p>
        <h4 id="spring">Spring</h4>
        <p>Spring 框架是一个开源的 Java 平台，为快速开发功能强大的 Java 应用程序提供了完备的基础设施支持。
        </p>
        <p>Spring 框架最初是由 Rod Johnson 编写的，在 2003 年 6 月首次发布于 Apache 2.0 许可证下。
        </p>
    </div>  

</body>

</html>
```

其他有时间再看，先放一放，不太用得到。
