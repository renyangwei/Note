# GridLayout

`GridLayout` 布局(网格布局)是 Android 4.0 以后引入的新布局，用于实现类似计算器界面的网格。

## 参数

- columnCount：列数
- rowCount：行数
- orientation：布局方向，水平或者竖直，一般选水平 horizontal
- layout_columnSpan：子视图参数，表示当前视图占用列数，默认是1
- layout_rowSpan：子视图参数，表示当前视图占用行数，默认是1
- layout_gravity：子视图参数，`fill` 表示填充其他空格

举例：

```xml
 <GridLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:columnCount="3"
                android:orientation="horizontal"
                android:id="@+id/gridLayout">
            <Button
                    style="@style/grid_layout_item"
                    android:text="1"/>

            <Button
                    style="@style/grid_layout_item"
                    android:text="2"
                    android:layout_columnSpan="1"/>

            <Button
                    android:text="3"
                    style="@style/grid_layout_item"/>

            <Button
                    android:text="4"
                    style="@style/grid_layout_item"/>

            <Button
                    android:text="5"
                    style="@style/grid_layout_item"/>

            <Button
                    android:text="6"
                    style="@style/grid_layout_item"/>

</GridLayout>
```

`GridLayout` 不能滑动，因为它是一个布局， `GridView` 可以滑动，想要 `GridView` 滑动可以嵌套 `NestedScrollView`。

> 还有一个 `GridView` ，用于显示多列的列表，毕竟 `listView` 只能显示一列，现在用 `RecyclerView` 都可以实现。