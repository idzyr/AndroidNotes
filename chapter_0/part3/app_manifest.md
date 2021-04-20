# 应用清单文件

每个应用项目必须在[项目源设置](https://developer.android.google.cn/studio/build#sourcesets)的根目录中加入 `AndroidManifest.xml` 文件（且必须使用此名称）。 清单文件会向 Android 构建工具、Android 操作系统和 Google Play 描述应用的基本信息。

## 概览

AndroidManifest.xml【清单文件】

路径 `app/src/main/AndroidManifest.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="top.miku.helloworld">
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <!--对Activity组件进行注册，为注册的的app是无法运行的 -->
        <activity android:name=".MainActivity">
            <intent-filter>
                <!-- 表示MainActivity这个活动是app启动后的主活动 -->
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```



## 部分元素属性说明

### 通用属性

> **提示；**
>
> 使用与application元素activity 元素



| 属性名称      | 作用                                | 可选值           |
| ------------- | ----------------------------------- | ---------------- |
| android:label | 可指定app名称或activity名称         | @string/app_name |
| android:theme | 可指定整个app主题或单个activity主题 | @style/AppTheme  |
|               |                                     |                  |

### manifest

| 属性名称 | 作用             | 可选值                 |
| -------- | ---------------- | ---------------------- |
| package  | 指定当前程序包名 | 通常这个值有AS自动生成 |
|          |                  |                        |
|          |                  |                        |



### application

> **提示；**
>
> 1. 值中起始的`.`所代表的是当前app的package路径如`top.miku.helloworld`在我们需要指定某类的完整路径是就可以省略这么长的包名直接使用`.`来代替。

| 属性名称            | 作用                         | 可选值     |
| ------------------- | ---------------------------- | ---------- |
| android:allowBackup | 是否允许系统备份此应用和数据 | Boolean    |
| android:icon        | app icon                     | @mipmap/xx |
| android:roundIcon   | 圆形App icon                 | @mipmap/xx |
| android:supportsRtl | 是否支持从右到左显示app      | Boolean    |
|                     |                              |            |
|                     |                              |            |
|                     |                              |            |
|                     |                              |            |



### activity

| 属性名称     | 作用                               | 可选值        |
| ------------ | ---------------------------------- | ------------- |
| android:name | activity所关联的java类（完整路径） | .MainActivity |
|              |                                    |               |
|              |                                    |               |

