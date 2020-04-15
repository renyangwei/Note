# RecyclerView

RecyclerView部件是更先进的，灵活的版本ListView

RecyclerView模型执行了大量优化工作，因此您不必：

- 首次填充列表时，它会创建并绑定列表两侧的某些视图持有者。例如，如果视图显示列表位置0到9，则RecyclerView创建并绑定这些视图持有者，也可能创建并绑定视图持有者的位置10.这样，如果用户滚动列表，则下一个元素已准备就绪显示。
- 当用户滚动列表时，根据需要RecyclerView创建新的视图持有者。它还可以保存已在屏幕外滚动的视图持有者，因此可以重复使用。如果用户切换他们正在滚动的方向，则可以向后移动从屏幕滚动的视图保持器。另一方面，如果用户继续向相同方向滚动，则已经离屏最长的视图持有者可以重新绑定到新数据。视图持有者不需要创建或视图膨胀; 相反，应用程序只更新视图的内容以匹配它绑定的新项目。
- 当显示的项目发生更改时，您可以通过调用适当的RecyclerView.Adapter.notify…()方法通知适配器。然后，适配器的内置代码仅重新绑定受影响的项目。

## 添加依赖

    dependencies {
        implementation 'com.android.support:recyclerview-v7:28.0.0'
    }

## 添加到布局文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- A RecyclerView with some commonly used attributes -->
<android.support.v7.widget.RecyclerView
    android:id="@+id/my_recycler_view"
    android:scrollbars="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```

```java
public class MyActivity extends Activity {
    private RecyclerView recyclerView;
    private RecyclerView.Adapter mAdapter;
    private RecyclerView.LayoutManager layoutManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.my_activity);
        recyclerView = (RecyclerView) findViewById(R.id.my_recycler_view);

        // use this setting to improve performance if you know that changes
        // in content do not change the layout size of the RecyclerView
        recyclerView.setHasFixedSize(true);

        // use a linear layout manager
        layoutManager = new LinearLayoutManager(this);
        recyclerView.setLayoutManager(layoutManager);

        // specify an adapter (see also next example)
        mAdapter = new MyAdapter(myDataset);
        recyclerView.setAdapter(mAdapter);
    }
    // ...
}
```

## 添加适配器

```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {
    private String[] mDataset;

    // Provide a reference to the views for each data item
    // Complex data items may need more than one view per item, and
    // you provide access to all the views for a data item in a view holder
    public static class MyViewHolder extends RecyclerView.ViewHolder {
        // each data item is just a string in this case
        public TextView textView;
        public MyViewHolder(TextView v) {
            super(v);
            textView = v;
        }
    }

    // Provide a suitable constructor (depends on the kind of dataset)
    public MyAdapter(String[] myDataset) {
        mDataset = myDataset;
    }

    // Create new views (invoked by the layout manager)
    @Override
    public MyAdapter.MyViewHolder onCreateViewHolder(ViewGroup parent,
                                                   int viewType) {
        // create a new view
        TextView v = (TextView) LayoutInflater.from(parent.getContext())
                .inflate(R.layout.my_text_view, parent, false);
        ...
        MyViewHolder vh = new MyViewHolder(v);
        return vh;
    }

    // Replace the contents of a view (invoked by the layout manager)
    @Override
    public void onBindViewHolder(MyViewHolder holder, int position) {
        // - get element from your dataset at this position
        // - replace the contents of the view with that element
        holder.textView.setText(mDataset[position]);

    }

    // Return the size of your dataset (invoked by the layout manager)
    @Override
    public int getItemCount() {
        return mDataset.length;
    }
}
```

适配器还可以使用 `ListAdapter`，传入List，自动在后台比较数据，使用动画更新，精简代码，还是很不错的。

## 自定义RecyclerView

### 修改布局

Android支持库包括三个标准布局管理器，每个管理器提供许多自定义选项：
- `LinearLayoutManager`将项目排列在一维列表中。使用RecyclerView with `LinearLayoutManager`提供旧版ListView布局等功能。
- `GridLayoutManager`将物品排列成二维网格，就像棋盘上的方块一样。使用RecyclerView with `GridLayoutManager`提供旧版GridView布局等功能。
- `StaggeredGridLayoutManager` 将物品排列成二维网格，每列略微偏离前一个，就像美国国旗中的星星一样。

如果这些布局管理器都不适合您的需求，您可以通过扩展 `RecyclerView.LayoutManager` 抽象类来创建自己的布局管理器。

## 添加项目动画

每当项目发生变化时，都会RecyclerView 使用动画师来改变其外观。这个动画师是一个扩展抽象`RecyclerView.ItemAnimator`类的对象。默认情况下， RecyclerView使用`DefaultItemAnimator`提供动画。如果要提供自定义动画，可以通过扩展来定义自己的动画对象`RecyclerView.ItemAnimator`。

## 启用列表项选择

该 `recyclerview-selection` 库使用户能够RecyclerView使用触摸或鼠标输入选择列表中的项目 。您可以保持对所选项目的可视化表示的控制。您还可以保留对控制选择行为的策略的控制，例如可以选择的项目以及可以选择的项目数。
