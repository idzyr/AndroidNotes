# GridLayout【网格布局】

控件按行列方式摆放。就像是一个表格一样。

**属性**

| 属性                        | 作用                                                     | 值                                 |
| --------------------------- | -------------------------------------------------------- | ---------------------------------- |
| android:orientation         | 设置为指定行和列显式的控件的默认方向                     | horizontal【水平】vertical【垂直】 |
| android:rowCount            | 设置最大行数                                             | int                                |
| android:columnCount         | 设置最大列数                                             | int                                |
| android:layout_column       | 指定子组件位于网格第几列                                 | int                                |
| android:layout_columnSpan   | 指定子组件跨第几列配合android:layout_gravity属性使用     | int                                |
| android:layout_columnWeight | 设置子组件水平权重【分配父控件剩余空间】                 | int                                |
| android:layout_row          | 指定子组件位于网格第几行                                 | int                                |
| android:layout_rowSpan      | 指定子组件跨第几行【配合android:layout_gravity属性使用】 | int                                |
| android:layout_RowWeight    | 设置子组件垂直权重【分配父控件剩余空】                   | int                                |
| android:layout_gravity      | 设置子组件什么方式占据网格的空间【fill常用】             | fill填充等                         |