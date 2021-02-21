# percentlayout百分比布局

> **警告；**
>
> ~~PercentFrameLayout~~逐渐被淘汰

由于LinearLayout本身已经支持按比例指定控件的大小了，百分比布局只为FrameLayout和RelativeLayout进行了功能扩展，提供了PercentFrameLayout和PercentRelativeLayout这两个全新的布局。

#### 让早期Android也支持百分比布局

- 2018年之前适用

1. 打开app/build.gradle文件，在`dependencies`闭包中添加如下内容

   ```xml
   dependencies {
       compile 'com.android.support:appcompat-v7:24.2.1'
       compile 'com.android.support:percent:24.2.1'
   }
   ```

2. 让gradle同步一下

- 2018年之后。

  > 如果项目默认是Androidx可以不用执行步骤1

  1. [迁移项目步骤](#项目迁移到androidx)

1. 把`compile 'com.android.support:percent:24.2.1'`修改为以下

```
  implementation 'androidx.percentlayout:percentlayout:1.0.0'
```

**示例**

- PercentFrameLayout

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.percentlayout.widget.PercentFrameLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"//定义一个app命名控件
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    <Button
            app:layout_widthPercent="50%"
            app:layout_heightPercent="50%"
            app:layout_marginTopPercent="25%"
            app:layout_marginLeftPercent="25%"
            android:text="@string/test"/>
</androidx.percentlayout.widget.PercentFrameLayout>
```

属性

| 属性                 | 作用                               | 值     |
| -------------------- | ---------------------------------- | ------ |
| layout_widthPercent  | 布局宽度                           | 百分比 |
| layout_heightPercent | 布局高度                           | 百分比 |
| layout_marginPercent | 布局外边距【包含其它的margin属性】 | 百分比 |
| layout_aspectRatio   | 宽高比                             |        |

- PercentRelativeLayout

  [了解更多点击这里](https://developer.android.google.cn/reference/kotlin/androidx/percentlayout/widget/PercentRelativeLayout)

