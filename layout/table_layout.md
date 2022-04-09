# TableLayout【表格布局】

## 行列设置

### 计数

1. TableLayout中添加组件,默认占满一行！！！
2. 如需一行上有多个组件，需要添加一个`TableRow`的容器,把组件都丢到里面！
3. tablerow中的组件个数就决定了该行有多少列,而列的宽度由该列中最宽的单元格决定
4. 有多少行就要自己数啦,一个tablerow一行,一个单独的组件也一行！多少列则是看tableRow中 的组件个数,组件最多的就是TableLayout的列数

### 宽高

1. tablerow的layout_width属性,默认是fill_parent的,我们自己设置成其他的值也不会生效！！！ 但是layout_height默认是wrapten——content的,我们却可以自己设置大小！
2. 整个表格布局的宽度取决于父容器的宽度(占满父容器本身)

## 属性

| 属性                    | 描述                       | 值   |
| :---------------------- | -------------------------- | ---- |
| android:collapseColumns | 设置需要被隐藏的列的序号   | int  |
| android:shrinkColumns   | 设置允许被收缩的列的列序号 | int  |
| android:stretchColumns  | 设置运行被拉伸的列的列序号 |      |
|                         |                            |      |

