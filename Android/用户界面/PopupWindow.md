# PopupWindow

官网解释：表示一个弹出窗口，可用于显示任意视图。它是一个浮动容器，显示在当前活动的顶部。

## 使用

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
