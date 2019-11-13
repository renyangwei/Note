# ViewPager

视图翻页工具，提供了多页面切换的效果。

使用场景：广告轮播、卡片切换和第一次进入的引导界面。

## 1 广告轮播

### 1.1 布局

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

### 1.2 适配器

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

### 1.3 Activity

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

## 2 与Fragment结合使用

与Fragment结合使用其实也一样，只是用Fragment代替原先的View，填充Viewpager；然后就是Adapter不一样，配合Fragment使用的有两个Adapter： `FragmentPagerAdapter` 和 `FragmentStatePagerAdapter` 。

区别：前者在换到其他页时不会销毁之前的页面内容，适合页面较少的情况使用，后者则是换到其他页会将之前的页面给销毁，返回到之前的页面就是重新加载，适合页面过多的情况使用。

举例：

```kotlin
class MyFragmentAdapter(fm: FragmentManager, index: Int, list: List<Fragment>) : FragmentPagerAdapter(fm, index) {

    val mList: List<Fragment> = list

    override fun getItem(position: Int): Fragment {
        return mList[position]
    }

    override fun getCount(): Int {
        return mList.size
    }
}
```

另一个也类似。

## 3 圆形指示器

思路：自定义LinnerLayout，用CheckRadio动态构造小圆点，监听 viewPager 切换事件，然后切换即可。

也可以使用第三方库，比如 [CircleIndicator](https://github.com/ongakuer/CircleIndicator)。

## 4 自动切换滑动

1. 处理自动滑动和手动滑动
2. 自动滑动使用 handle

参考 [ViewPager循环、自动滚动效果](https://www.jianshu.com/p/58f356eaa6e9)

定时任务参考 [Android定时任务的应用及实现](https://www.jianshu.com/p/9304c8faf79f)

## 5 第三方库

- [youth5201314/banner](https://github.com/youth5201314/banner)
- [alibaba/UltraViewPager](https://github.com/alibaba/UltraViewPager)

试了阿里巴巴的UltraViewPager，就是滚动速度不能自定义，第一个可自定义比较多。