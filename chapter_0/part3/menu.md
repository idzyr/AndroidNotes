# menu/【菜单】

用于定义应用菜单（如选项菜单、上下文菜单或子菜单）的 XML 文件。请参阅[菜单资源](https://developer.android.google.cn/guide/topics/resources/menu-resource)。

1. 在res目录下新建menu目录。
2. 从创建的menu目录上右键New——Menu resource file 设置文件名即可。
3. 使用`<item>` 定义菜单项

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- android:title设置菜单项名 -->
    <item android:id="@+id/menu_item1" android:title="选项一"></item>
    <item android:id="@+id/menu_item2" android:title="选项二"></item>
    <item android:id="@+id/menu_item3" android:title="选项三"></item>
</menu>
```



**使用；**

可以查看 其它组件——>>菜单组件