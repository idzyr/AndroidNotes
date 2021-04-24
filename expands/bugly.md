# Bugly

腾讯Bugly，为移动开发者提供专业的异常上报和运营统计，帮助开发者快速发现并解决异常，同时掌握产品运营动态，及时跟进用户反馈。

官网；https://bugly.qq.com/v2/

## 异常上报

### 集成步骤

**网络安全配置**

> 自Android9.0开始不允许直接访问非HTTTPS协议内容。

1. 在 res 目录下添加 xml 目录，同时在该目录下新增文件 network_security_config.xml

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <network-security-config>
       <domain-config cleartextTrafficPermitted="true">
           <domain includeSubdomains="true">android.bugly.qq.com</domain>
       </domain-config>
   </network-security-config>
   ```

1. 在 AndroidManifest.xml 文件的 application 增加属性

   ```xml
   android:networkSecurityConfig="@xml/network_security_config"
   ```

   ![image-20201031201115622](bugly-images/image-20201031201115622.png)

**同时集成SDK和NDK;**

在Module的build.gradle文件中添加依赖和属性配置：

```groovy
android {
    defaultConfig {
        ndk {
            // 设置支持的SO库架构
            abiFilters 'armeabi' , 'x86' //, 'armeabi-v7a', 'x86_64', 'arm64-v8a'
        }
    }
}

dependencies {
    implementation 'com.tencent.bugly:crashreport:latest.release' //其中latest.release指代最新Bugly SDK版本号，也可以指定明确的版本号，例如2.1.9
    implementation 'com.tencent.bugly:nativecrashreport:latest.release' //其中latest.release指代最新Bugly NDK版本号，也可以指定明确的版本号，例如3.0
}
```

**参数配置;**

1. 在AndroidManifest.xml中添加权限：

   ```xml
       <uses-permission android:name="android.permission.READ_PHONE_STATE" />
       <uses-permission android:name="android.permission.INTERNET" />
       <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
       <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   ```

2. 请避免混淆Bugly，在proguard-rules.pro混淆文件中增加以下配置：建议把项目切换成project模式。

   ```
   -dontwarn com.tencent.bugly.**
   -keep public class com.tencent.bugly.**{*;}
   ```

   ![image-20201031202802010](bugly-images/image-20201031202802010.png)

### 基本使用

**简单初始化**

> 为在AndroidManifest.xml的“Application”中增加“meta-data”配置项，初始化。

- 将以下代码复制到项目Application类`onCreate()`中，Bugly会为自动检测环境并完成配置：

  **为了保证运营数据的准确性，建议不要在异步线程初始化Bugly。**

  > 第三个参数为SDK调试模式开关，调试模式的行为特性如下：
  >
  > - 输出详细的Bugly SDK的Log；
  > - 每一条Crash都会被立即上报；
  > - 自定义日志将会在Logcat中输出。
  >
  > 建议在测试阶段建议设置成true，发布时设置为false。

```java
/* Bugly SDK初始化
        * 参数1：上下文对象
        * 参数2：APPID，平台注册时得到,注意替换成你的appId 如876a9ea437
        * 参数3：是否开启调试模式，调试模式下会输出'CrashReport'tag的日志
*/
CrashReport.initCrashReport(getApplicationContext(), "注册时申请的APPID", false); 
```

![image-20201031203731471](bugly-images/image-20201031203731471.png)

**配置APP信息;**

Bugly2.0及以上版本还支持通过`AndroidManifest.xml`来配置APP信息。如果同时又通过代码中配置了APP信息，**则最终以代码配置的信息为准.**

在“AndroidManifest.xml”的“Application”中增加“meta-data”配置项：

```xml
<application
    <!-- 配置APP ID -->
    <meta-data
            android:name="BUGLY_APPID"
            android:value="<APP_ID>" />
    <!-- 配置APP版本号 -->
    <meta-data
            android:name="BUGLY_APP_VERSION"
            android:value="<APP_Version>" />
    <!-- 配置APP渠道号 -->
    <meta-data
            android:name="BUGLY_APP_CHANNEL"
            android:value="<APP_Channel>" />
    <!-- 配置Bugly调试模式（true或者false）-->
    <meta-data
            android:name="BUGLY_ENABLE_DEBUG"
            android:value="<isDebug>" />
</application>
```

- 什么是，app渠道号；

  渠道包指的是在各大应用市场，发布的apk包的清单文件中，某个meta-data标签下，配置的value不一样，这个标签的作用就是用来区分是哪个市场的，比如你发布到360.这个值就是你就可以配置成360，豌豆荚就可以配置成wandoujia，那么这么配置的作用是干嘛的？很简单，就是用来做统计的，比如我们项目中用的是友盟统计，它可以统计用户从哪个平台下载了你们的app，从而更好的掌握用户的操作习惯。所以，如果app没有统计功能的需求，你只需要打一个同样的包，直接发布到各个平台即可，根本不用关心什么渠道。

- 不同于“android:versionName”，“BUGLY_APP_VERSION”配置的是Bugly平台的APP版本号。

- 通过“AndroidManifest.xml”配置后的初始化方法如下：

  ```java
  CrashReport.initCrashReport(getApplicationContext());
  ```



**测试;**

现在您可以制造一个Crash（建议通过“按键”来触发），来体验Bugly的能力了。在初始化Bugly的之后，调用Bugly测Java Crash方法。

- java层

  ```java
  CrashReport.testJavaCrash();
  ```

- ndk层

  ```java
  CrashReport.testNativeCrash();
  ```

![image-20201031213824304](bugly-images/image-20201031213824304.png)

![image-20201031213805484](bugly-images/image-20201031213805484.png)

![image-20201031214901380](bugly-images/image-20201031214901380.png)

### 增加上报进程控制【正确使用姿势】

如果App使用了多进程且各个进程都会初始化Bugly（例如在Application类onCreate()中初始化Bugly），那么每个进程下的Bugly都会进行数据上报，造成不必要的资源浪费。

因此，为了节省流量、内存等资源，建议初始化的时候对上报进程进行控制，只在主进程下上报数据：判断是否是主进程（通过进程名是否为包名来判断），并在初始化Bugly时增加一个上报进程的策略配置。

```java
Context context = getApplicationContext();
// 获取当前包名
String packageName = context.getPackageName();
// 通过调用getProcessName方法获取当前进程名
String processName = getProcessName(android.os.Process.myPid());
// 设置是否为上报进程
CrashReport.UserStrategy strategy = new CrashReport.UserStrategy(context);
strategy.setUploadProcess(processName == null || processName.equals(packageName));
// 初始化Bugly并指定上报策略
CrashReport.initCrashReport(context, "注册时申请的APPID", isDebug, strategy);
// 如果通过“AndroidManifest.xml”来配置APP信息，初始化方法如下
// CrashReport.initCrashReport(context, strategy);
```

- 其中获取进程名的方法“getProcessName”有多种实现方法，推荐方法如下：

```java
/**
 * 获取进程号对应的进程名
 * 
 * @param pid 进程号
 * @return 进程名
 */
private static String getProcessName(int pid) {
    BufferedReader reader = null;
    try {
        reader = new BufferedReader(new FileReader("/proc/" + pid + "/cmdline"));
        String processName = reader.readLine();
        //不等于空
        // trim() 返回字符串的副本，忽略前导空白和尾部空白。
        if (!TextUtils.isEmpty(processName)) {
            processName = processName.trim();
        }
        return processName;
    } catch (Throwable throwable) {
        throwable.printStackTrace();
    } finally {
        try {
            if (reader != null) {
                reader.close();
            }
        } catch (IOException exception) {
            exception.printStackTrace();
        }
    }
    return null;
}
```

## 应用升级

由于 Google Play 政策限制，请不要使用升级功能，否则可能被检测到违规而导致警告、下架甚至封禁账号等后果。

### 集成

同样也需要对网络安全进行配置详细见上面的，异常上报中的**网络安全配置**。

#### 自动集成【推荐】

**gradle配置;**

配置示例（路径app/build.gradle）

**注意：** 升级SDK已经集成crash(崩溃日志)上报功能，已经集成Bugly的用户需要注释掉原来Bugly的jcenter库； 已经配置过符号表的Bugly用户保留原有符号表配置； Bugly SDK（2.1.5及以上版本）已经将Java Crash和Native Crash捕获功能分开，如果想使用NDK库，需要配置： `implementation 'com.tencent.bugly:nativecrashreport:latest.release'`

```groovy
  android {
        defaultConfig {
          ndk {
            //设置支持的SO库架构
            abiFilters 'armeabi' , 'x86' //, 'armeabi-v7a', 'x86_64', 'arm64-v8a'
          }
        }
      }
      dependencies {
          //注释掉原有bugly的仓库
          //implementation 'com.tencent.bugly:crashreport:latest.release'//其中latest.release指代最新版本号，也可以指定明确的版本号，例如2.3.2
          implementation 'com.tencent.bugly:crashreport_upgrade:latest.release'//其中latest.release指代最新版本号，也可以指定明确的版本号，例如1.2.0
          implementation 'com.tencent.bugly:nativecrashreport:latest.release' //其中latest.release指代最新版本号，也可以指定明确的版本号，例如2.2.0
      }
```

#### 参数设置

**在AndroidMainfest.xml中进行以下配置：**

1. 权限配置

   ```xml
   <uses-permission android:name="android.permission.READ_PHONE_STATE" />
       <uses-permission android:name="android.permission.INTERNET" />
       <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
       <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
       <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
       <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
   ```

2. Activity配置

   ```xml
   <application>
   
       <activity
                   android:name="com.tencent.bugly.beta.ui.BetaActivity"
                   android:configChanges="keyboardHidden|orientation|screenSize|locale"
                   android:theme="@android:style/Theme.Translucent" />
   </application>    
   ```

1. 配置FileProvider

   **注意：**如果您想兼容Android N(Android 7.0)或者以上的设备，必须要在AndroidManifest.xml文件中配置FileProvider来访问共享路径的文件。

   ```xml
   <application>
       <provider
                   android:name="androidx.core.content.FileProvider"
                   android:authorities="${applicationId}.fileProvider"
                   android:exported="false"
                   android:grantUriPermissions="true">
               <meta-data
                       android:name="android.support.FILE_PROVIDER_PATHS"
                       android:resource="@xml/provider_paths"/>
          </provider>
   </application>
   ```

1. 混淆配置

   为了避免混淆SDK，在Proguard混淆文件中增加以下配置

   ```
   -dontwarn com.tencent.bugly.**
   -keep public class com.tencent.bugly.**{*;}
   -keep class android.support.**{*;}
   ```

### 测试验证

**SDK初始化**

注意：如果您之前使用过Bugly SDK，请将以下这句注释掉。

```java
 CrashReport.initCrashReport(getApplicationContext(), "注册时申请的APPID", false); 
```

统一初始化方法：

```java
 /**
         * 统一初始化方法
         * context 上下文
         * appid 注册时appid
         * Boolean 是否启用调式模式
         */
Bugly.init(getApplicationContext(), "注册时申请的APPID", false);
```

**提示：**已经接入Bugly用户改用上面的初始化方法,不影响原有的crash上报功能.

init方法会自动检测更新，不需要再手动调用`Beta.checkUpgrade(),` 如需增加自动检查时机可以使用Beta.checkUpgrade(false,false);

- `Beta.checkUpgrade(false,false);`
  - 参数
    - isManual 用户手动点击检查，非用户点击操作请传false
    - isSilence 是否显示弹窗等交互，[true:没有弹窗和toast] [false:有弹窗或toast]

**发布新版本;**

进入应用升级页面，点击发布新版本，上传要升级的APP的版本（**上传APP的versioncode必须不低于外发版本的versiocode，否则用户检测不到更新**）

![img](bugly-images/JIQ5U45I%7B_E%5DI3_AX%7D5%7BJ3.png)