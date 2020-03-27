# PopupWindow

官网解释：表示一个弹出窗口，可用于显示任意视图。它是一个浮动容器，显示在当前活动的顶部。

## 使用--初始化

1. 创建布局文件
2. 创建popupwindow
3. 显示

举例：

布局文件popup_window.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/colorAccent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/Hello"
        android:layout_marginStart="@dimen/activity_horizontal_margin"
        android:layout_marginTop="@dimen/activity_vertical_margin"/>

    <Button
        android:id="@+id/btn_popup"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/sure" />
    
</LinearLayout>
```

创建popupwindow

```kotlin
// 不用填根节点
val view = View.inflate(this, R.layout.popup_window, null)
// 初始化，还有第四个参数 focusable，是否可以获得焦点，默认false
val popupWindow = PopupWindow(view, dip2px(this, 300.0f), ViewGroup.LayoutParams.WRAP_CONTENT)
// 一定要设置背景，因为在某些 Andorid 系统版本中会出现点击外部和返回键弹窗却无法消失的 Bug
popupWindow.setBackgroundDrawable(ColorDrawable())
// 设置是否点击消失
popupWindow.isOutsideTouchable = true
```

显示

有两种方式， `showAsDropDown` 和 `showAtLocation`，前者在 anchorView 的下方，后者在界面上任意位置。

```kotlin
// 显示在 anchorView 的下方
popupWindow.showAsDropDown(anchor, 0, 0, Gravity.END)
// 显示在屏幕下方
popupWindow.showAtLocation(anchor, Gravity.BOTTOM, 0, 0)
// 其他位置，比如Gravity.Top表示在屏幕上方
```

## 使用--继承

1. 创建布局文件
2. 创建自定义类继承PopupWindow,自定义构造函数
3. 解析布局文件，获得内部控件
4. 设置宽高
5. 设置背景
6. setContentView设置内容
7. setAnimationStyle设置动画(可选)
8. 显示

举例：

```java
public class MyWindow extends PopupWindow {

    private Context mContext;
    private ViewGroup mRoot;

    public MyWindow(Context context, ViewGroup root) {
       super(context);
       mContext = context;
       mRoot = root;
       setHeight(ViewGroup.LayoutParams.WRAP_CONTENT);
       setWidth(ViewGroup.LayoutParams.WRAP_CONTENT);
       setOutsideTouchable(true);
       setFocusable(true);
       setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));
       View contentView = LayoutInflater.from(context).inflate(R.layout.popup_test, null, false);
       setContentView(contentView);
       setAnimationStyle(ResourceUtil.getStyle("SiginAnim"));
    }
     public void show() {
         // 显示在屏幕最上方
        showAtLocation(mRoot, Gravity.TOP, 0, 0);
    }

    private void viewDismiss() {
        dismiss();
    }
}
```

style.xml

```xml
<style name="SiginAnim" parent="@android:style/Animation">
    <item name="android:windowEnterAnimation">@anim/anim_sign_in</item>
    <item name="android:windowExitAnimation">@anim/anim_sign_out</item>
</style>
```

anim_sign_in.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android" android:shareInterpolator="true">
    <translate
        android:duration="@integer/dyb_medium_anim_time"
        android:fromYDelta="-100%p"
        android:toYDelta="0%p" />
</set>
```

anim_sign_out.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android" android:shareInterpolator="true">
    <translate
        android:duration="@integer/dyb_medium_anim_time"
        android:fromYDelta="0%p"
        android:toYDelta="-100%p" />
</set>
```

## 总结

popupWindow适合用做的控件：

- APP内引导
- 自定义下拉菜单（有官方提供的popupMenu）
- 自定义Toast提示（比如sdk的登录）
- 悬浮窗
- 等等

用途还是比较广泛。

参考： [简书](https://www.jianshu.com/p/6c32889e6377)