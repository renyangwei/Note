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

