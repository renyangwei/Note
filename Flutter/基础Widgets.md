# 基础 Widgets

## Container

一个拥有绘制、定位、调整大小的 widget。

可以为其他部件添加背景。

举例：

```dart
void showAllContainer() {
  runApp(
    new MaterialApp(
      title: "Container",
      home: new Scaffold(
        body: new Center(
          child: Container(   // 创建
            child: Text('boring'),  // 子控件
            color: Colors.blue,     // 颜色
            padding: EdgeInsets.all(10.0),  // 内边距
            alignment: Alignment.center,  // 使子控件在容器中对齐,设置后整个容器铺满父控件
            width: 200,   // 也可以指定宽高
            height: 200,
            transform: Matrix4.rotationZ(0.05),// 绕Z轴旋转
            // decoration: BoxDecoration(  // 在容器中添加一个形状，该属性不能和颜色同时使用
            //   color: Colors.red,
            //   shape: BoxShape.circle,
            // ),
          ),
        ),
      ),
    )
  );
}
```

## Row

在水平方向上排列子widget的列表。

