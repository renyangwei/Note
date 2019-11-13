# NestedScrollView

`NestedScrollView` 是support-v4包提供的控件,它的作用类似于 `android.widget.ScrollView` ,不同点在于 `NestedScrollView` 支持嵌套滑动，且默认开启。

虽然 `NestedScrollView` 支持嵌套滑动，但是在实际应用中，嵌套滑动可能会带来其他的一些奇奇怪怪的副作用，Google 也推荐我们能不使用嵌套滑动就尽量不要使用。

> 注意： `NestedScrollView` 子布局里只能有一个布局，比如 LinnearLayout和GridView。

举例:

```xml
 <androidx.core.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="@dimen/activity_horizontal_margin">

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

        </GridLayout>

    </androidx.core.widget.NestedScrollView>
```

**问题记录**

如果根布局是 `ConstraintLayout` ，那么 `NestedScrollView` 不会滑动，我把根布局改成LinnearLayout就没问题了。