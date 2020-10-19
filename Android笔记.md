# Android笔记

## 预备知识

### XML

## Android摘要

### 系统架构

![untitled](Android%E7%AC%94%E8%AE%B0-images/untitled.png)

**主要架构解析；**

- Linux内核层

  Android系统是基于Linux内核的，这一层为Android设备的各种硬件提供了底层的驱动，如显示驱动、音频驱动、照相机驱动、蓝牙驱动、Wi-Fi驱动、电源管理等。

- 系统运行库层

  这一层通过一些C/C++库来为Android系统提供了主要的特性支持。如SQLite库提供了数据库的支持，OpenGL|ES库提供了3D绘图的支持，Webkit库提供了浏览器内核的支持等。
  同样在这一层还有Android运行时库，它主要提供了一些核心库，能够允许开发者使用Java语言来编写Android应用。另外，Android运行时库中还包含了Dalvik虚拟机（5.0系统之后改为ART运行环境），它使得每一个Android应用都能运行在独立的进程当中，并且拥有一个自己的Dalvik虚拟机实例。相较于Java虚拟机，Dalvik是专门为移动设备定制的，它针对手机内存、CPU性能有限等情况做了优化处理。

- 应用框架层

  这一层主要提供了构建应用程序时可能用到的各种API，Android自带的一些核心应用就是使用这些API完成的，开发者也可以通过使用这些API来构建自己的应用程序。

- 应用层

  所有安装在手机上的应用程序都是属于这一层的，比如系统自带的联系人、短信等程序，或者是你从Google Play上下载的小游戏，当然还包括你自己开发的程序

### 四大组件

1. 活动（Activity）
2. 服务（Service）
3. 广播接收器（Broadcast Receiver）
4. 内容提供器（Content Provider）



## 配置开发环境

**必要环境；**

- JDK1.8+

### 安装Android Studio

**下载；**

https://developer.android.google.cn/studio



## 创建一个HelloWorld项目

### 建立一个项目

> 演示一个项目基本建立步骤。

1. 启动AS，在欢迎界面。选择启动新的AS项目。

   ![1566199434812](Android%E7%AC%94%E8%AE%B0-images/1566199434812-1600785160710.png)

2. 选择一个活动模板新手选择空的模板即可

   ![1566200108844](Android%E7%AC%94%E8%AE%B0-images/1566200108844.png)

3. 对项目进行配置。

   ![1566222137814](Android%E7%AC%94%E8%AE%B0-images/1566222137814.png)

4. 项目成功创建

   ![1566222352784](Android%E7%AC%94%E8%AE%B0-images/1566222352784.png)

### 模拟器创建

- 点击右上角工具栏的图标启动AVD Manager

  ![1566222804233](Android%E7%AC%94%E8%AE%B0-images/1566222804233.png)

- 点击这里创建模拟器

  ![1566222911382](Android%E7%AC%94%E8%AE%B0-images/1566222911382.png)

- 选择要创建设备的类型

  ![1566223075713](Android%E7%AC%94%E8%AE%B0-images/1566223075713.png)

- 选择模拟器的版本，不带Download的是本地已经存在的。

  ![1566224004423](Android%E7%AC%94%E8%AE%B0-images/1566224004423.png)

- 确认模拟器信息无误后点击finish

  ![1566224111472](Android%E7%AC%94%E8%AE%B0-images/1566224111472.png)

- 等待片刻模拟器就创建成功了，点击下图标注出就可以启动模拟器了。

![1566224259620](Android%E7%AC%94%E8%AE%B0-images/1566224259620.png)

**多学一点；**

AS默认创建的模拟器会存放到以下路径`C:\Users\%USERNAME%\.android\avd`要更改路径可以把镜像文件移动到其它路径然后修改**配置文件**中的`Path`的值为镜像的路径即可.

![1566225143587](Android%E7%AC%94%E8%AE%B0-images/1566225143587.png)

![1566225967852](Android%E7%AC%94%E8%AE%B0-images/1566225967852.png)



### 运行项目

- 观察Android Studio顶部工具栏中的图标,其中左边的**锤子**按钮是用来编译项目的，中间的**下拉列表**是用来选择运行哪一个项目的，通常app就是当前的主项目，右边的**三角形按钮**是用来运行项目的。

![1566224860040](Android%E7%AC%94%E8%AE%B0-images/1566224860040.png)

- 选择要运行的设备点击OK

  ![1566226243659](Android%E7%AC%94%E8%AE%B0-images/1566226243659.png)

- 成功运行

  ![1566226373983](Android%E7%AC%94%E8%AE%B0-images/1566226373983.png)

  

**注意；**

通过Android Studio直接运行项目生成的都是测试版安装文件

## Android项目结构分析

### 目录分析

默认目录结构不利于理解，我们可以更改为**Project** 模式

![1566280488318](Android%E7%AC%94%E8%AE%B0-images/1566280488318.png)

**目录总览；**

![1566281873008](Android%E7%AC%94%E8%AE%B0-images/1566281873008.png)

**app目录；**

![1566283663352](Android%E7%AC%94%E8%AE%B0-images/1566283663352.png)

**app/res资源目录；**

![1566286328404](Android%E7%AC%94%E8%AE%B0-images/1566286328404.png)

1. 所有以**drawable**开头的文件夹都是用来放图片的
2. 所有以**mipmap**开头的文件夹都是用来放应用图标的
3. 所有以**values**开头的文件夹都是用来放字符串、样式、颜色等配置的
4. **layout**文件夹是用来放布局文件的。

### 特定文件分析

> 以下以HelloWorld程序为例子。
>
> 包名为；`top.miku.helloworld`

#### app目录

**AndroidManifest.xml【清单文件】**

所在路径 `app/src/main/AndroidManifest.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="top.miku.helloworld"> //package属性指定当前程序包名
    <!-- app配置 -->
    <application
        android:allowBackup="true" //是否允许用户备份此应用和数据
        android:icon="@mipmap/ic_launcher" //程序icon
        android:label="@string/app_name"  //app名称
        android:roundIcon="@mipmap/ic_launcher_round" //圆形app图标
        android:supportsRtl="true" //是否愿意支持从右到左显示app
        android:theme="@style/AppTheme"> //主题
        <!-- 注册活动标记 -->
        <!--对HelloWorld活动进行注册为注册的活动是无法运行的 -->
        <activity android:name=".MainActivity">
            <!-- 过滤器标记 -->
            <intent-filter>
                <!-- 表示MainActivity这个活动是app启动后的主活动 -->
                <action android:name="android.intent.action.MAIN" />
				<!-- 配置类型 -->
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

**MainActivity.java【活动java代码】**

路径 `app\src\main\java\top.miku.helloworld\MainActivity`

```java
package top.miku.helloworld;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
//继承Activity的子类AppCompatActivity
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);//设置当前活动的布局文件xml
    }
}
```

**注意；**一切活动的创建必须继承**Activity**或其子类

**activity_main.xml【活动布局xml】**

路径 `app\src\main\res\layout/activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <!-- 文字视图控件 -->
    <TextView 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"//显示的文字在此处定义
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

#### 详解build.gradle文件

不同于Eclipse，Android Studio是采用Gradle来构建项目的。Gradle是一个非常先进的项目构建工具，它使用了一种基于Groovy的领域特定语言（DSL）来声明项目设置，摒弃了传统基于XML（如Ant和Maven）的各种烦琐配置。

##### app目录外层build.gradle

通常这个文件我们是不进行修改的。

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.
//翻译：顶级构建文件，您可以在其中添加所有子项目/模块通用的配置选项。
buildscript {
    repositories { //远程仓库配置
        google()
        jcenter()//它是一个代码托管仓库，很多Android开源项目都会选择将代码托管到jcenter上，声明了这行配置之后，我们就可以在项目中轻松引用任何jcenter上的开源项目了。

    }
    //依赖关系
    dependencies {
        //声明了一个Gradle插件。为什么要声明这个插件呢？因为Gradle并不是专门为构建Android项目而开发的，Java、C++等很多种项目都可以使用，Gradle来构建。因此如果我们要想使用它来构建Android项目，则需要声明
        classpath 'com.android.tools.build:gradle:3.4.2'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        // 翻译：注意：请勿在此处放置应用程序依赖项它们属于单个模块build.gradle文件。

    }
}

allprojects {
    repositories {
        google()
        jcenter()

    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

##### app目录下的build.gradle

```groovy
apply plugin: 'com.android.application'//应用了一个插件，一般有两种值可选：com.android.application 表示这是一个应用程序模块，com.android.library 表示这是一个库模块。应用程序模块和库模块的最大区别在于，一个是可以直接运行的，一个只能作为代码库依附于别的应用程序模块来运行。

//在这个闭包中我们可以配置项目构建的各种属性
android {
    compileSdkVersion 29 //用于指定项目的编译版本(API 版本代号)
    buildToolsVersion "29.0.2"//用于指定项目构建工具的版本
    //defaultConfig闭包中可以对项目的更多细节进行配置
    defaultConfig {
        applicationId "top.miku.helloworld"//用于指定项目的包名
        minSdkVersion 19 //用于指定项目最低兼容的Android系统版本
        targetSdkVersion 29 //指定的运行的目标SDK 大于这个版本的新特性内容将无法使用
        versionCode 1 //用于指定项目的实际版本号
        versionName "1.0" //用于指定项目的版本名
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    //buildTypes闭包中用于指定生成安装文件的相关配置
    /*
    通常只会有两个子闭包，一个是debug，一个是release。debug闭包用于指定生成测试版安装文件的配置，release闭包用于指定生成正式版安装文件的配置。另外，debug闭包是可以忽略不写的。
    */
    buildTypes {
    //release闭包
        release {
            minifyEnabled false //用于指定是否对项目的代码进行混淆 true或false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'//用于指定混淆时使用的规则文件
            /*
                这里指定了两个文件，第一个proguard-android.txt 是在Android SDK目录下的，里面是所有项目通用的混淆规则，第二个proguard-rules.pro 是在当前项目的根目录下的，里面可以编写当前项目特有的混淆规则。

            */
        }
    }
}
//dependencies闭包
/*它可以指定当前项目所有的依赖关系。通常Android Studio项目一共有3种依赖方式：
    1.本地依赖、库依赖和远程依赖。本地依赖可以对本地的Jar包或目录添加依赖关系
    2.库依赖可以对项目中的库模块添加依赖关系
    3.远程依赖则可以对jcenter库上的开源项目添加依赖关系.
*/
dependencies {
    /*
        fileTree声明本地依赖关键词
        compile远程依赖声明关键词
        compile project库依赖声明关键词        
    */
    implementation fileTree(dir: 'libs', include: ['*.jar'])//声明本地依赖
    implementation 'androidx.appcompat:appcompat:1.0.2'//
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test:runner:1.2.0'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}
```

## AS日志工具使用

### 使用Android的日志工具Log

Android中的日志工具类是**Log（android.util.Log）**这个类中提供了如下5个方来供我们打印日志。

1. `Log.v()` 用于打印那些最为琐碎的、意义最小的日志信息。对应级别verbose，是Android日志里面级别最低的一种。
2. `Log.d()`用于打印一些调试信息，这些信息对你调试程序和分析问题应该是有帮助的。对应级别debug，比verbose高一级。
3. `Log.i()` 用于打印一些比较重要的数据，这些数据应该是你非常想看到的、可以帮你分析用户行为数据。对应级别info，比debug高一级。
4. `Log.w()`用于打印一些警告信息，提示程序在这个地方可能会有潜在的风险，最好去修复一下这些出现警告的地方。对应级别warn，比info高一级。
5. `Log.e()` 用于打印程序中的错误信息，比如程序进入到了catch语句当中。当有错误信息打印出来的时候，一般都代表你的程序出现严重问题了，必须尽快修复。对应级别error，比warn高一级。

```java
public class MainActivity extends AppCompatActivity {
    //生成log中的rga常量
    private static final String TAG = "MainActivity";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);//引入布局XML
        //打印日志参数（tga【标记，一般写类名】,具体打印内容）
        Log.d("MainActivity","onCreateExecute");
    }
}
```

### 日志级别顺序

verbose【详细】 < debug【调试】 < info【提示】 < warn【警告】 < error【错误】

### Logcat 面板

<img src="Android%E7%AC%94%E8%AE%B0-images/1566371964144.png" alt="1566371964144"  />

#### 日志过滤器

<img src="Android%E7%AC%94%E8%AE%B0-images/1566373863267.png" alt="1566373863267"  />

- Show only selected application 【只显示当前选中程序的日志】

- Firebase【谷歌提供的一个分析工具】

- No Filters【不过滤】

- Edit Filter Configuration【自定义过滤器】

  ![1566374705009](Android%E7%AC%94%E8%AE%B0-images/1566374705009.png)

#### 级别控制

![1566374984209](Android%E7%AC%94%E8%AE%B0-images/1566374984209.png)

- 我们将级别选中为debug，这时只有我们使用debug及大于debug级别方法打印的日志才会显示出来，其他级别以此类推。

#### 关键词过滤

![1566375225884](Android%E7%AC%94%E8%AE%B0-images/1566375225884.png)

- 我们可以在输入框里输入关键字的内容，这样只有符合关键字条件的日志才会显示出来，从而能够快速定位到任何你想查看的日志。另外还有一点需要注意，关键字过滤是支持正则表达式的。

#### Log而不使用System.out

System.out的缺点；

如日志打印不可控制、打印时间无法确定、不能添加过滤器、日志没有级别区分…

**多学一点；**

- 输入logt自动生成TAG常量，赋值为类名

  ```java
      private static final String TAG = "MainActivity";
  ```

- 输入log+日志类型缩写，如logi

  ```java
          Log.d(TAG, "onCreate: 主活动执行完成");
  ```



## 四大组件之Activity（活动）

详细见；[四大组件之Activity](./四大组件之Activity.md)



## 其它组件使用

### Toast【气泡消息】

Toast是Android系统提供的一种非常好的提醒方式，在程序中可以使用它将一些短小的信息通知给用户，这些信息会在一段时间后自动消失，并且不会占用任何屏幕空间

![1566454007517](Android%E7%AC%94%E8%AE%B0-images/1566454007517.png)

**示例代码；**

```java
package top.miku.activitytest;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class FirstActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //引入布局
        setContentView(R.layout.first_layout);
        //获取元素 findViewById通过id获取页面上的元素
        //返回的是一个View 对象，我们需要向下转型将它转成Button 对象
        Button button1 = (Button) findViewById(R.id.button_1);
        //给元素注册点击事件
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //使用Toast通知
                /* 使用Toast.makeTest静态方法创建一个Toast对象,调用其show()方法显示
                *  参数
                *   - context 上下文，由于活动本身就是一个Context 对象，因此这里直接传入FirstActivity.this
                *   - text 要显示的内容
                *   - Toast 显示的时长 默认两个可选值 Toast.LENGTH_SHORT = 长度短 | Toast.LENGTH_LONG = 长度长
                *
                * */
                Toast.makeText(FirstActivity.this, "点击了button按钮", Toast.LENGTH_SHORT).show();
            }
        });

    }

}
```

#### 解决MIUI自带应用名问题

```java
Toast toast = Toast.makeText(MyEditText.this, null, Toast.LENGTH_SHORT);
        toast.setText("文本");
        toast.show();
```



## Menu菜单



![1566475727243](Android%E7%AC%94%E8%AE%B0-images/1566475727243.png)

- `app\src\main\res`以下路径新建menu目录

- 从menu目录新建Menu resource file

  ![1566475280575](Android%E7%AC%94%E8%AE%B0-images/1566475280575.png)

- 编写menu的XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <menu xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- item菜单项 -->
      <item
          android:id="@+id/add_item"//选项的id
          android:title="添加"//项名
      />
      <item
          android:id="@+id/remove_item"
          android:title="移除"
      />
  </menu>
  ```

- 重写onCreateOptionsMenu方法添加菜单。

  ```java
  package top.miku.activitytest;
  
  import androidx.appcompat.app.AppCompatActivity;
  
  import android.os.Bundle;
  import android.view.Menu;
  import android.view.View;
  import android.widget.Button;
  import android.widget.Toast;
  
  public class FirstActivity extends AppCompatActivity {
      /*————————————绑定活动————————————————*/
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          //引入布局
          setContentView(R.layout.first_layout);
  
      }
      /*——————————创建Menu菜单——————————*/
      @Override
      public boolean onCreateOptionsMenu(Menu menu) {
          /*
          * 1.通过getMenuInflater() 方法能够得到MenuInflater 对象
          * 2.再调用它的inflate() 方法就可以给当前活动创建菜单了。
          * 3.inflate() 方法接收两个参数，
          *     - 第一个参数用于指定我们通过哪一个资源文件来创建菜单。
          *     - 第二个参数用于指定我们的菜单项将添加到哪一个Menu对象当中，
          *   这里直接使用onCreateOptionsMenu() 方法中传入的menu 参数。
          *     - 然后给这个方法返回true ，表示允许创建的菜单显示出来，如果返回了false ，创建的菜单将无法显示。
          * */
          getMenuInflater().inflate(R.menu.main,menu);
          return true;//菜单是否可见
      }
  
  }
  ```

- 给菜单选项注册事件

  ```java
      /*——————————给菜单注册事件在绑定活动闭包外面书写————————————*/
  
      @Override
      //@NonNull注解用在指明一个参数，字段或者方法的返回值不可以为null
      public boolean onOptionsItemSelected(@NonNull MenuItem item) {
          //item.getItemId()获取触发事件的id名
          switch (item.getItemId()){
              case R.id.add_item:
                  Toast.makeText(this,"你点击的是添加菜单",Toast.LENGTH_SHORT).show();
                  break;
              case R.id.remove_item:
                  Toast.makeText(this, "你点击的是删除菜单", Toast.LENGTH_LONG).show();
                  break;
              default:
          }
          return true;
      }
  ```



## Intent

**介绍；**

Intent是Android程序中各组件之间进行交互的一种重要方式，它不仅可以指明当前组件想要执行的动作，还可以在不同组件之间传递数据。Intent一般可被用于启动活动、启动服务以及发送广播等



### 显示Intent

所为显式Intent，在创建Intent对象时明确指定了要启动组件的名称。也就是明确知道要启动的组件名称。

**演示；**

> 从活动1启动活动2

- 在创建一个新的活动（活动2）【具体步骤可以参考，四大组件之Activity中使用AS的空activity模板创建部分】

  ![1566485434027](Android%E7%AC%94%E8%AE%B0-images/1566485434027.png)

- 这次我们勾选创建布局文件

  ![1566485703390](Android%E7%AC%94%E8%AE%B0-images/1566485703390.png)

- 自动生成的second_layout.xml过于复杂【不适合新手】我们把里面的代码替换为以下

  ```xml
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
          android:orientation="vertical"
          android:layout_width="match_parent"
          android:layout_height="match_parent">
  
      <Button
              android:id="@+id/button_2"
              android:layout_width="match_parent"
              android:layout_height="wrap_content"
              android:text="Button 2"
              />
  </LinearLayout>
  ```

- 不要忘记，**任何一个活动都是需要在AndroidManifest.xml中注册的**，不过幸运的是，Android Studio已经帮我们自动完成了

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="top.miku.activitytest">
  
      <application
              android:allowBackup="true"
              android:icon="@mipmap/ic_launcher"
              android:label="@string/app_name"
              android:roundIcon="@mipmap/ic_launcher_round"
              android:supportsRtl="true"
              android:theme="@style/AppTheme">
          <!-- 这是注册的第二个活动 -->
          <activity android:name=".SecondActivity"></activity>
          <activity
                  android:name=".FirstActivity"
                  android:label="@string/app_name">
              <intent-filter>
                  <action android:name="android.intent.action.MAIN" />
  
                  <category android:name="android.intent.category.LAUNCHER" />
              </intent-filter>
          </activity>
      </application>
  
  </manifest>
  ```

**构造函数；**

- `Intent(Context packageContext, Class<?> cls)` 。这个构造函数接收两个参数。

  -  参数

    1. 第一个参数Context 要求提供一个启动活动的上下文。

    2. 第二个参数Class 则是指定想要启动的目标活动，通过这个构造函数就可以构建出Intent 的“意图”。

Activity类中提供了一个`startActivity()` 方法，这个方法是专门用于启动活动的，它接收一个Intent 参数。

```java
/*—————————————启动一个活动绑定活动中书写———————————————————————*/
// 从第一个活动中书写。
        Button button3 = (Button) findViewById(R.id.button_3);
        button3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //创建Intent对象
                Intent intent = new Intent(FirstActivity.this,SecondActivity.class);
                //启动这个活动
                startActivity(intent);
            }
        });
```

### 隐式Intent

相比于显式Intent，隐式Intent则含蓄了许多，它**并不明确指出**我们想要启动哪一个活动，而是指定了一系列更为抽象的**action** 和**category** 等信息，然后交由系统去分析这个Intent，并帮我们找出合适的活动去启动。什么叫作合适的活动呢？简单来说就是可以响应我们这个隐式Intent的活动

#### Intent过滤器

过滤器是当使用隐藏Intent设置的一些action和data等这些属性就叫做过滤器。

![image-20191123211151237](Android%E7%AC%94%E8%AE%B0-images/image-20191123211151237.png)

##### 设置过滤器

**简介；**

通常在AndroidManifest.xml 文件下每个组件下添加`<intent-filter>`标记，在这个标记内指定具体的action和data等属性。

如AndroidStudio生成的xml清单文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="top.miku.testintent">
    <uses-permission android:name="android.permission.CALL_PHONE"/>
    <uses-permission android:name="android.permission.SEND_SMS"/>

    <application
            android:allowBackup="true"
            android:icon="@mipmap/ic_launcher"
            android:label="@string/app_name"
            android:roundIcon="@mipmap/ic_launcher_round"
            android:supportsRtl="true"
            android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <!-- 给MainActivity设置过滤器 -->
            <intent-filter>
                //当前组件可以响应的action 动作。
                <!-- 通过android:name来指定具体的值 -->
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
                category //更精确指明当前组件具体响应的信息。
            </intent-filter>
        </activity>
    </application>
```



## UI布局







## 常用控件

详细见；[Android之控件](./Android之控件.md)





## AS中的Activity









## Android中的HTTP

详细见：[Android中的HTTP](./Android中的HTTP.md)









## AS使用技巧

> Android Sutdio简称AS

### 快捷键

- 选中类名或方法按CTRL+N 搜索当前类所在的包
- 选中类按CTRL+H 查看继承关系和实现类等。
- 在方法或构造函数上面输入`/**`回车可以 实现如同C#中的方法说明注解功能。
- CTRL+shrift+U选中的英文字符大小写转换。
- CTRL+P移动到方法上可以查看需要那些参数。
- F2快速定位到错误代码行。
- Ctrl+Q查看当前方法的说明文档。







