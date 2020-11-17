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



