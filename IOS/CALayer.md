# CALayer

当UIView需要显示时，先调用 `drawRect` 绘图，绘制到自己的图层上。CALayer负责展示，UIView负责监听和响应事件。

CALayer的属性比UIView更强大。

可以和Photoshop图层类比。

示例：

```objc
UIView *view = [[UIView alloc] initWithFrame:CGRectMake(150, 300, 200, 200)];
view.layer.borderWidth = 10;
view.layer.borderColor = (__bridge CGColorRef _Nullable)([UIColorredColor]);
view.layer.cornerRadius = 20;
// 裁剪多余的部分
view.layer.masksToBounds = YES;
view.layer.shadowOffset = CGSizeMake(10, 10);
view.layer.shadowColor = [UIColor grayColor].CGColor;
view.layer.shadowOpacity = 1;
view.layer.contents = (__bridge id _Nullable)([UIImageimageNamed:@"mg"].CGImage);
[self.view addSubview:view];
```

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    
    // 自定义layer
    CALayer* lay = [[CALayer alloc] init];
    lay.backgroundColor = [UIColor redColor].CGColor;
    // 大小
    lay.bounds = CGRectMake(0, 0, 100, 100);
    // 位置
    lay.position = CGPointMake(200, 200);
    [self.view.layer addSublayer:lay];
    self.layer = lay;
}

- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    UITouch *t = touches.anyObject;
    // 获取当前手指位置
    CGPoint p = [t locationInView:t.view];
    // 让图层移动到手指点击位置
    // 这里默认带有隐式动画
    // 但是控件的根layer没有动画，比如UIImageView，UIButton等
    
    // 如果需要禁用则使用事务
    [CATransaction begin];
    [CATransaction setDisableActions:YES];
    self.layer.position = p;
    [CATransaction commit];
    
}
```

## 时钟练习

### 1.时针的位置

需要设置一个锚点。

锚点是将图片的某个位置定位到中心点（position属性）。

锚点范围 0-1，默认是0.5，也就是图片中心。

比如上文的代码 `lay.position = CGPointMake(200, 200);` ，表示将图片中心点放到这个位置，锚点如果设置成 `(0, 0)` 表示将图片左上角放到这个点。

    lay.anchorPoint = CGPointMake(0.5, 0.7);

这样就改变了图片旋转时的位置。

### 2.按时间旋转

思路：

每秒移动 2PI/60 ，初始位置：当前秒*2PI/60

初始化先调用一次确定位置。

```objc
-(void) timeChange {
    CGFloat angle = 2 * M_PI / 60;
    NSDate * date = [NSDate date];
    NSDateFormatter * fromatter = [[NSDateFormatter alloc] init];
    fromatter.dateFormat = @"ss";
    CGFloat time = [[fromatter stringFromDate:date] floatValue];
    // 表示旋转到某个位置
    self.view.layer.affineTransform = CGAffineTransformMakeRotation(time * angle);
}
```

## CADisplayLink

是一种以屏幕刷新频率触发的时钟机制，每秒钟执行大约60次左右。

```objc
// timeChange 函数每秒会执行大约60次
CADisplayLink * link = [CADisplayLink displayLinkWithTarget:self selector:@selector(timeChange)];
// 添加到主循环中
[link addToRunLoop:[NSRunLoop mainRunLoop] forMode:NSDefaultRunLoopMode];
```

```objc
NSDate * date = [NSDate date];
NSCalendar * cal = [NSCalendar currentCalendar];
CGFloat time = [cal component:NSCalendarUnitSecond fromDate:date];
```