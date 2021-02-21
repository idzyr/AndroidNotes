# RelativeLayout相对布局

RelativeLayout又称作相对布局，也是一种非常常用的布局。和LinearLayout的排列规则不同，RelativeLayout显得更加随意一些，它可以通过相对定位的方式让控件出现在布局的任何位置。

**属性**

| 属性                             | 作用                                                         | 值         |
| -------------------------------- | ------------------------------------------------------------ | ---------- |
| android:layout_alignParent方位词 | 让控件对齐到父控件指定方向，如android:layout_alignParentTop  | true/false |
| android:centerInParent           | 在父控件中心对齐                                             | true/false |
| android:layout_above             | 以指定id控件的上方                                           | @+id/id名  |
| android: layout_below            | 以指定id控件的下方                                           | @+id/id名  |
| android:layout_toLeftOf          | 以指定id控件的左侧                                           | @+id/id名  |
| android:layout_toRightOf         | 以指定id控件的右侧                                           | @+id/id名  |
| android:layout_align方位词       | 表示让一个控件的左边缘和另一个控件的左边缘对齐如android:layout_alignLeft | @+id/id名  |
| android:layout_gravity           | 设置子控件从布局管理器中的摆放位置                           | 方位词     |
|                                  |                                                              |            |

## 相对于父控件对齐

主要使用以下属性`android:layout_alignParent`和`android:centerInParent`

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_alignParentLeft="true"/>//对齐到父控件左边
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_alignParentRight="true"/>//对齐到父控件右边
</RelativeLayout>
```

## 相对于控件定位

`android:layout_above`、`android: layout_below`等

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_alignParentLeft="true"/>
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_alignParentRight="true"/>
    <Button
            android:id="@+id/center"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_centerInParent="true"/>
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_above="@+id/center"/>//在center控件上方
    <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/test"
            android:layout_below="@+id/center"//在center控件下方
            android:layout_alignLeft="@+id/center"/>//在center左边缘对齐

</RelativeLayout>
```