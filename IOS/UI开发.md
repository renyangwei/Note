# UI开发

每一个界面都是一个View Controller，里面包含一个UIView，里面又包含了许多子控件。

## 1. UITextField 输入框

获取用户输入：

```objc
@property (weak, nonatomic) IBOutlet UITextField *text1;
NSString *num1 = self.text1.text;
```

将键盘叫回：

`[self.view endEditing:YES];`

在模拟器中使用 `cmd` + `K` 弹出键盘。

## 2. UIButton 按钮

```objc
// 移动图片
// 拖拽的时候选择uibutton，通过tag分辨不同的按钮
// 还可以通过改变 imgLoading.center,改变中心点位置
- (IBAction)moveImg:(UIButton *)sender {
    CGRect originRect = self.imgLoading.frame;
    switch (sender.tag) {
        case 1: // 上
            originRect.origin.y--;
            break;
        case 2: // 右
            originRect.origin.x++;
            break;
        case 3: // 下
            originRect.origin.y++;
            break;
        case 4: // 左
            originRect.origin.x--;
            break;
        default:
            break;
    }
    self.imgLoading.frame = originRect;
}
```

```objc
// 改变大小
// 还可以通过改变 imgLoading.bounds，改变边长
- (IBAction)scaleImg:(UIButton *)sender {
    CGRect originRect = self.imgLoading.frame;
    switch (sender.tag) {
        case 1: // 大
            originRect.size.height += 10;
            originRect.size.width += 10;
            break;
        case 2: // 小
            originRect.size.height -= 10;
            originRect.size.width -= 10;
            break;
        default:
            break;
    }
    self.imgLoading.frame = originRect;
}
```

**添加点击事件**

```objc
[btn addTarget:self action:@selector(btnClick) forControlEvents:UIControlEventTouchUpInside];

- (void) btnClick {
    NSLog(@"you click me");
}
```

## 3. 简单动画

### 3.1 方式一：头尾式(在iOS13上已经废弃)

```objc
// 开启动画
[UIView beginAnimations:nil context:nil];
// 设置动画时间
[UIView setAnimationDuration:2];
// 要执行的动作
self.imgLoading.frame = originRect;
// 提交
[UIView commitAnimations];
```

### 3.2 方式二：block式

```objc
 [UIView animateWithDuration:1 animations:^{
 				// 要执行的代码
        self.imgLoading.frame = originRect;
 }];
```

还有其他的API，以后自行查看。

## 4. 动态创建控件

```objc
UIButton *btn = [[UIButton alloc]initWithFrame:CGRectMake(16, 400, 50, 40)];
[btn setTitle:@"hello" forState:UIControlStateNormal];
[btn setTitleColor:UIColor.blackColor forState:UIControlStateNormal];
// 添加单击事件
[btn addTarget:self action:@selector(btnClick) forControlEvents:UIControlEventTouchUpInside];
// 添加到视图上
[self.view addSubview:btn];
```

单击执行的函数：

```objc
- (void) btnClick {
    NSLog(@"you click me");
}
```

## 5. 平移、旋转和缩放

```objc
// 平移
self.imgLoading.transform = 
CGAffineTransformTranslate(self.imgLoading.transform, 0, 10);
// 缩放，后面填倍数，现在是1.1倍
self.imgLoading.transform = CGAffineTransformScale(self.imgLoading.transform, 1.1, 1.1);
// 旋转，这里要填弧度，2π = 360°
// 可以用常量表示，M_PI_2 表示 90°
self.imgLoading.transform = CGAffineTransformRotate(self.imgLoading.transform, M_PI_2);
// 让控件回到原始状态
self.imgLoading.transform = CGAffineTransformIdentity;
```

## 6. xib 与 storyboard

两者都用于描述界面。xib轻量级，用于描述一个界面中的某个部分，后者用来描述多个界面以及跳转关系。

### 6.1 创建

1. 创建 **User Interface** 里的 **View**，确定，然后和storyboard一样操作控件；

2. 创建一个类 **MyUiView** 继承 **UIView**，并与xib关联；
3. 拖动xib里的子控件，在 **MyUiView** 里生成属性。

### 6.2 获取xib控件

```objc
// 找到应用程序的根目录
NSBundle *rootBundle = [NSBundle mainBundle];
// 获取对应的xib文件里的view
MyUiVIew *appView = [[rootBundle loadNibNamed:@"MyView" owner:nil options:nil] firstObject];
// 获取子控件并赋值
appView.myLabel.text = @"fadsfa";
```

> 一般情况不暴露子控件，而是提供具体的方法。

## 7.UILabel

```objc
UILabel *label = [[UILabel alloc] init];
// 设置圆角
label.layer.cornerRadius = 10;
// 裁剪多余的部分
label.layer.masksToBounds = YES;
```

## 8.UIScorllView

可以实现 "滚动" 和 "缩放"。基本设置和其他控件差不多，拖拽到ViewController 里面，设置其子控件。

步骤：

1. 拖拽ScrollView，设置全屏；
2. 拖拽ImageView到ScrollView，设置全屏、图片和大小(大小和图片相同)；
3. 设置ScrollView的内容，`self.scrollView.contentSize = self.imageView.frame.size;` 。

> 注意：ScrollView 和 ImageView 都要勾选 User Interaction Enabled。

```objc
#import "ViewController.h"
// 继承协议
@interface ViewController () <UIScrollViewDelegate>

@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@property (weak, nonatomic) IBOutlet UIImageView *imageView;

@end

@implementation ViewController

//返回需要缩放的子视图
- (UIView *) viewForZoomingInScrollView:(UIScrollView *) scrollView {
    return self.imageView;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    // 设置代理
    self.scrollView.delegatae = self;
    // 设置大小
    self.scrollView.contentSize = self.imageView.frame.size;
  	// 设置缩放
    self.scrollView.maximumZoomScale = 4;
    self.scrollView.minimumZoomScale = 0.2;
}

@end
```

## 9. 代理 (实现协议)

和 Android中的监听事件基本一致。前者实现接口，后者实现协议。

```objc
// 实现代理
@interface ScrollViewController () <UIScrollViewDelegate>

// 设置代理
- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    self.scrollView.contentSize = self.imageView.frame.size;
    self.scrollView.delegate = self;
}

// 实现代理方法
- (void) scrollViewDidScroll:(UIScrollView *)scrollView {
    // 正在滑动
}

- (void) scrollViewWillBeginDragging:(UIScrollView *)scrollView {
    // 开始拖拽
}
```

## 10. 轮播图

用到 `UIScorllView` 和 `UIPageControl` 。

```objc
#import "ScrollViewController.h"

@interface ScrollViewController () <UIScrollViewDelegate>
@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@property (weak, nonatomic) IBOutlet UIPageControl *pageControl;

@property (nonatomic, strong) NSTimer *timer;

@end

@implementation ScrollViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.scrollView.delegate = self;
    CGFloat imgW = 343;
    CGFloat imgH = 130;
    CGFloat imgY = 0;
    
    // 将图片添加到ScrollView
    for (int i=0; i<4; i++) {
        UIImageView *imageView = [[UIImageView alloc] init];
        imageView.frame = CGRectMake(i * imgW, imgY, imgW, imgH);
        imageView.scalesLargeContentImage = YES;
        NSString *imageName = [NSString stringWithFormat:@"loading%d", i+1];
        imageView.image = [UIImage imageNamed:imageName];
        [self.scrollView addSubview:imageView];
    }
    // 所有图片的宽度
    self.scrollView.contentSize = CGSizeMake(imgW*4, imgH);
    // 实现分页效果
    self.scrollView.pagingEnabled = YES;
    // 隐藏水平滚动器
    self.scrollView.showsHorizontalScrollIndicator = NO;
    
    // 总页数
    self.pageControl.numberOfPages = 4;
    // 当前页
    self.pageControl.currentPage = 0;
    
    self.timer = [NSTimer scheduledTimerWithTimeInterval:3 target:self selector:@selector(timerBlock) userInfo:nil repeats:YES];
    // 修改timer的优先级,使其与控件相同
    NSRunLoop *runLoop = [NSRunLoop currentRunLoop];
    [runLoop addTimer:self.timer forMode:NSRunLoopCommonModes];
    
}

// 计算当前滚动到了第几页
- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    // x轴偏移量
    CGFloat offsetX = scrollView.contentOffset.x;
    // 加上一半的宽度
    offsetX += scrollView.frame.size.width / 2;
    self.pageControl.currentPage = offsetX / scrollView.frame.size.width;
}

- (void) scrollViewWillBeginDragging:(UIScrollView *)scrollView {
    // 停止计时器,下次必须重新创建新对象
    [self.timer invalidate];
    // 指向nil方便判断
    self.timer = nil;
}

- (void) scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate {
    // 重新开启计时器
    self.timer = [NSTimer scheduledTimerWithTimeInterval:3 target:self selector:@selector(timerBlock) userInfo:nil repeats:YES];
    // 修改timer的优先级,使其与控件相同
    NSRunLoop *runLoop = [NSRunLoop currentRunLoop];
    [runLoop addTimer:self.timer forMode:NSRunLoopCommonModes];
}

- (void) timerBlock {
    NSInteger page = self.pageControl.currentPage;
    if (page == self.pageControl.numberOfPages - 1) {
        page = 0;
    } else {
        page++;
    }
    CGFloat offsetX = page * self.scrollView.frame.size.width;
    [self.scrollView setContentOffset:CGPointMake(offsetX, 0) animated:YES];
}

@end
```

## 11. 启动页

启动页其实就是系统截屏后显示的图片。

## 12. UITableView

和Android差不多。

1. 创建 `UITableView` ；
2. 设置 `DataSource` ，重写方法；
3. 创建 `UITableViewCell` ，可通过xib，设置数据

```objc
#import "ViewController.h"
#import "CZHero.h"


@interface ViewController () <UITableViewDataSource, UITableViewDelegate> // 遵循多个协议
@property (weak, nonatomic) IBOutlet UITableView *uiTableView;
@property (nonatomic, strong) CZHero *hero;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // 设置 dataSource
    self.uiTableView.delegate = self;
    self.uiTableView.dataSource = self;
    // 设置行高,如果要设置每行不同高度，则实现 UITableViewDelegate 协议
    self.uiTableView.rowHeight = 60;
    //设置分割线
    self.uiTableView.separatorStyle = UITableViewCellSeparatorStyleSingleLine;
    self.uiTableView.separatorColor = UIColor.brownColor;
    // 还可以设置header View 和footer View，前者可以放广告，后者可以加载更多
 	  self.uiTableView.tableHeaderView = [HeaderView headerView];
  	// 滑动到特定行
    [self.uiTableView scrollToRowAtIndexPath:[NSIndexPath indexPathWithIndex:5] atScrollPosition:UITableViewScrollPositionBottom animated:YES];
}


// 数据懒加载
- (CZHero *)hero {
    if (_hero == nil) {
        NSMutableDictionary *d1 = [@{@"icon": @"dsdd", @"name": @"亚索", @"slogan": @"我的剑就是你的剑"} mutableCopy];
        _hero = [CZHero heroWithDictionary:d1];
    }
    return _hero;
}


// 组的数量
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 2;
}

// 每一组显示多少行
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 5;
}

// 返回单元格控件
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    // 单元格重用，去缓存池查找，没有就创建，尽管@"hero_cell"在常量区，加上static后字符串变成常量，不会重复创建resId变量
    static NSString *resId = @"hero_cell";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:resId];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:resId];
    }
    cell.textLabel.text = self.hero.name;
    cell.detailTextLabel.text = self.hero.slogan;
    // 单元格设置箭头，还有其他图案，比如checkbox
    cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
    return cell;
}

// 每组的标题，类似页眉
// 如果重写了改方法，但是UITableView的style设置为plain，标题会类似联系人固定在屏幕上
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section {
    return @"header";
}

// 每组尾部说明，类似页脚
- (NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section {
    return @"footer";
}

// 隐藏状态栏
- (BOOL)prefersStatusBarHidden {
    return YES;
}

// 设置右侧的索引栏
- (NSArray<NSString *> *)sectionIndexTitlesForTableView:(UITableView *)tableView {
    return @[@"A", @"B", @"C", @"D"];
}

// 监听被单击的单元格
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
  	// 弹窗
    UIAlertController* alert = [UIAlertController alertControllerWithTitle:@"My Alert"
                                                                   message:@"This is an alert."
                                                            preferredStyle:UIAlertControllerStyleAlert];
    UIAlertAction* defaultAction = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault handler:^(UIAlertAction * action) {
        NSLog(@"you input:%@", alert.textFields[0].text);
        self.hero.slogan = alert.textFields[0].text;
        // 重新加载全部数据
        // [tableView reloadData];
        // 加载要修改的行，只适用于总行数不变的情况
        [tableView reloadRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationAutomatic];
    }];
    [alert addAction:defaultAction];
    [alert addTextFieldWithConfigurationHandler:^(UITextField *textField){
        textField.text = @"请输入要修改的内容";
    }];
    [self presentViewController:alert animated:YES completion:nil];
}


@end
```

```objc
#import "CZHero.h"

@implementation CZHero

// 字典转对象
- (instancetype)initWithDictionary:(NSDictionary *)dict {
    if (self = [super init]) {
        [self setValuesForKeysWithDictionary:dict];
    }
    return self;
}

+ (instancetype)heroWithDictionary:(NSDictionary *)dict {
    return [[self alloc] initWithDictionary:dict];
}


@end
```

设置 `HeaderView`

先设置xib文件，然后创建并关联到UiView，获取对象。

```objc
#import "HeaderView.h"

@interface HeaderView()
@property (weak, nonatomic) IBOutlet UIImageView *imageView;

@end

@implementation HeaderView

+ (instancetype) headerView {
    HeaderView * head = [[[NSBundle mainBundle]loadNibNamed:@"HeaderView" owner:self options:nil] firstObject];
    return head;
}

// 表示已经加载好，可以处理控件
- (void)awakeFromNib {
    [super awakeFromNib];
    [self.imageView setHighlighted:YES];
}

@end
```

## 13. 延迟函数

```objc
// 延迟3秒
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(3 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    // 要执行的代码
});
```

