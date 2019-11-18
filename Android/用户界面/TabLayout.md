# TabLayout

头部导航，官方有提供Tablayout，但是不能自定义。

这里推荐 [FlycoTabLayout](https://github.com/H07000223/FlycoTabLayout)，有很多效果。

至于自己实现起来也不是很难，有时间再研究。

举例：

```xml
 <com.flyco.tablayout.SlidingTabLayout
            android:id="@+id/sliding_tab_layout"
            android:layout_width="match_parent"
            android:layout_height="32dp"
            android:background="@color/colorPrimary"
            app:tl_textSelectColor="@color/colorAccent"
            app:tl_textUnselectColor="@color/colorBlack"
            app:tl_indicator_width="10dp"
            app:tl_indicator_color="@color/colorAccent"
            app:tl_tab_space_equal="true"
            android:layout_marginTop="8dp"
            />
```

```kotlin

private val TITLE: Array<String> = arrayOf("精选", "免费", "超级会员", "漫画", "独家")

 override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        ...
        val slidingTabLayout: SlidingTabLayout = view.findViewById(R.id.sliding_tab_layout)
        slidingTabLayout.setViewPager(viewPager, TITLE)
        return view
    }
```