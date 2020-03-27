# Dialog弹窗

弹窗使用的最多的是两种：`DialogFragment` 和 `PopupWindow` 。我们分别来讲它们如何使用。

至于 `AlertDialog` 和 `Dialog` ，官方已经不推荐直接使用。官方的说法是： `DialogFragment` 做了各种事情来保持片段的生命周期驱动它，而不是 `Dialog` 。

## DialogFragmen

1. 创建布局文件；
2. 继承 `DialogFragment` ，重写 `onCreateView` 方法。

举例：

```java
public class MyDialogFragment extends DialogFragment {


    private static final double PORTRAIT_SCREEN_SIZE = 0.95;//竖屏时屏幕宽度的0.95倍


   
    @Override
    public void onStart() {
        super.onStart();
        Dialog dialog = getDialog();
        if (dialog != null) {
             // 设置宽高
            DisplayMetrics dm = new DisplayMetrics();
            getActivity().getWindowManager().getDefaultDisplay().getMetrics(dm);
            dialog.getWindow().setLayout((int) (dm.widthPixels * PORTRAIT_SCREEN_SIZE), ViewGroup.LayoutParams.WRAP_CONTENT);
            // 设置位置
            dialog.getWindow().setGravity(Gravity.START);
            // 设置动画
            dialog.getWindow().setWindowAnimations(R.sytle.dlalog_animator);
        }
    }


    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        // 有没有都一样
        // getDialog().requestWindowFeature(Window.FEATURE_NO_TITLE);
        return inflater.inflate(R.layout.my_dialog_fragment, container);
    }
    
}
```

动画

```xml
<!-- 横屏动画 -->
<style name="LandscapeDialogAnimation">
    <item name="android:windowEnterAnimation">@anim/landscape_float_in</item>
    <item name="android:windowExitAnimation">@anim/landscape_float_out</item>
</style>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:duration="@integer/dyb_medium_anim_time"
        android:fromXDelta="-50%p"
        android:toXDelta="0" />

</set>
```

显示弹窗

    new MyDialogFragment().show(getSupportFragmentManager(), "my_fragment");

> 注意资源文件要从最上面写，而不是居中。

