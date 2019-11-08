# ViewPager

视图翻页工具，提供了多页面切换的效果。

有两种用法：广告轮播和卡片切换。

## 广告轮播

**布局**

```xml
<!-- 轮播图 -->
<androidx.viewpager.widget.ViewPager
    android:id="@+id/view_pager"
    android:layout_width="match_parent"
    android:layout_height="120dp"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:padding="@dimen/normal_padding"
    app:layout_constraintHorizontal_bias="1.0" 
    android:layout_marginTop="8dp">

</androidx.viewpager.widget.ViewPager>
```

**广告布局**

这里用textView代替

```xml
<TextView
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/text_view"
        android:background="@color/colorBottomNav">

</TextView>
```

**适配器**

```kotlin
// 类名和构造函数
class BookShelfAdapter(context: Context, data: List<String>) : PagerAdapter() {

    private val mContext:Context = context

    var mData:List<String> = data

    // 判断是否page view与 instantiateItem(ViewGroup, int)返回的object的key 是否相同，以提供给其他的函数使用
    override fun isViewFromObject(view: View, `object`: Any): Boolean {
        return view == `object`
    }

    // 对象的数量
    override fun getCount(): Int {
        return mData.size
    }

    // 创建指定位置的页面视图
    override fun instantiateItem(container: ViewGroup, position: Int): Any {
        val textView : TextView = View.inflate(mContext, R.layout.text_view, null) as TextView
        textView.text =  mData[position]
        container.addView(textView)
        return textView
    }

    // 移除一个给定位置的页面
    override fun destroyItem(container: ViewGroup, position: Int, `object`: Any) {
        container.removeView(`object` as View?)
    }
}
```

**Activity**

```kotlin
 override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val view: View =  inflater.inflate(R.layout.bookshelf_fragment, container, false)
        val viewPager = view.findViewById<ViewPager>(R.id.view_pager)
        val adapter = context?.let { BookShelfAdapter(it, initData()) }
        viewPager.adapter = adapter
        return view
    }

private fun initData(): List<String> {
        val list: ArrayList<String> = ArrayList()
        list.add("A")
        list.add("B")
        list.add("C")
        return list
    }
```

## 与Fragment结合使用

与Fragment结合使用其实也一样，只是用Fragment代替原先的View，填充Viewpager；然后就是Adapter不一样，配合Fragment使用的有两个Adapter： `FragmentPagerAdapter` 和 `FragmentStatePagerAdapter` 。

