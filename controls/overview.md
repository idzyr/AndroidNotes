# 总览



## 通用属性

| 属性                  | 作用                                                         | 值                                                           |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| android:id            | 给当前控件定义了一个唯一标识符                               | @+/xxid                                                      |
| android:layout_width  | 指定了控件的宽度                                             | 推荐[match_parent]("表示让当前控件的大小和父布局的大小一样") [fill_parent]("表示让当前控件的大小和父布局的大小一样") [wrap_content]("表示让当前控件的大小能够刚好包含住里面的内容") |
| android:layout_height | 指定了控件的高度                                             | 推荐[match_parent]("表示让当前控件的大小和父布局的大小一样") [fill_parent]("表示让当前控件的大小和父布局的大小一样") [wrap_content]("表示让当前控件的大小能够刚好包含住里面的内容") |
| android:textAllCaps   | 文本内容全部大写【默认true】                                 | true / false                                                 |
| android:gravity       | 指定文字对齐方式                                             | top、right、bottom、left、center等 可以用 &#124; 指定多个值。    |
| android:textSize      | 指定文字的大小                                               | sp位单位                                                     |
| android:textColor     | 指定文字颜色                                                 | 支持十六位颜色代码                                           |
| android:background    | 指定背景色                                                   | 支持十六位颜色代码                                           |
| android:visibility    | 控件的可见性                                                 | visible【可见默认】 invisible【不可见会占位置】 gone【不可见也不占位置】 |
| android:onClick       | 给控件设置点击事件                                           | 一个方法名，                                                 |
| android:padding       | 默认四方向设置内边距，也可以单独设置不同方向如android:paddingTop | 数值加单位                                                   |
| android:layout_margin | 默认四方向设置外边距，也可以单独设置不同方向android:layout_marginLeft | 数值加单位                                                   |