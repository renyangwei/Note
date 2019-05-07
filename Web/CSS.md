# CSS

## 语法

    who{ what: how;}

## 依赖

```html
<head>
  <link rel="stylesheet" type="text/css" href="reset.css">
  <link rel="stylesheet" type="text/css" href="styles.css">
</head>
```

## 根据类型配置

```css
/* Tag */
blockquote{
    background: lightgreen;
    color: darkgreen;
  }

/* Class */
.docClass{
    background: red;
    color: aquamarine;
}

/* IDs */
#docId{
    background: blue;
    color: brown;
}
```

## 距离单位

- px：像素
- %：百分比(依赖于父元素)

举例：

```css
body{ width: 400px;}
p{ width: 50%;}
```

## 字体

都是以 `font-` 开头

一共有九中字体：

- Arial
- Arial Black
- Comic Sans MS
- Courier New
- Georgia
- Impact
- Times New Roman
- Trebuchet MS
- Verdana

```css
body{ font-family: Arial;}
p{ font-size: 16px;}
h2{ font-style: italic;} 
h2{ font-weight: bold;}
/* 1.5倍行距 */
body{ font-size: 16px; line-height: 1.5;}
```

## 文字

都是以 `text-` 开头

```css
body{ text-align: left;}
/* 删除线，还有下划线之类的 */
.deleted{ text-decoration: line-through;}
blockquote{ text-indent: 30px;}
/* 阴影：x轴、y轴、模糊度、颜色 */
h1{ text-shadow: 0 2px 5px rgba(0,0,0,0.5);}

```


## 背景

```css
body{ background: #f2eee9;}
body{ background-image: url(images/diagonal-pattern.png);}
/* 宽高 */
body{ background: yellow; height: 50px; width: 100px;}
```

## 边界

```css
blockquote{ border-color: yellow; border-style: solid; border-width: 1px;}
/* 单个方向 */
blockquote{ border-bottom-color: yellow; border-bottom-style: solid; border-bottom-width: 1px;}
```

## 填充

```css
blockquote{ padding: 20px;}
blockquote{ padding-bottom: 20px;}
```

## 边距

```css
p{ margin: 40px;}
.title{ margin-bottom: 30px;}
.subtitle{ margin-top: 15px;}
```