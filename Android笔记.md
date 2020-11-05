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



## 四大组件之广播接收者







## UI布局







## 常用控件

详细见；[Android之控件](./Android之控件.md)





## AS中的Activity









## Android中的HTTP

详细见：[Android中的HTTP](./Android中的HTTP.md)



## App权限

详细见: [App权限](./App权限.md)





## UI更新

### 子线程更新UI

[子线程更新UI)](./子线程更新UI.md)



## 字体图标使用

**准备；**

0. 准备字体图标文件`.ttf`

1. 创建一个IconView类继承AppCompatTextView类。

2. 实现三个构造方法。

3. 创建初始化方法`private void init`  并设置字体图标。

4. 从三个构造方法中分别调用init(Context)方法

   ```java
   package com.xuelingmiao.testapp.fonticon;
   
   import android.content.Context;
   import android.graphics.Typeface;
   import android.util.AttributeSet;
   
   import androidx.annotation.NonNull;
   import androidx.annotation.Nullable;
   import androidx.appcompat.widget.AppCompatTextView;
   
   public class IconView  extends AppCompatTextView {
   
       public IconView(@NonNull Context context) {
           super(context);
           init(context);
       }
   
       public IconView(@NonNull Context context, @Nullable AttributeSet attrs) {
           super(context, attrs);
           init(context);
       }
   
       public IconView(@NonNull Context context, @Nullable AttributeSet attrs, int defStyleAttr) {
           super(context, attrs, defStyleAttr);
           init(context);
       }
   
       //创建初始化方法
       private void init (Context context){
           //设置字体图标路径
           this.setTypeface(Typeface.createFromAsset(context.getAssets(),"icon/iconfont.ttf"));
       }
   }
   
   ```

   

5. 在``src\main`目录下新建`assets\fonts`和fonts目录把字体文件拷贝到此处。

   - 新建`assets`目录，建议切换到项目结构试图操作。

     ![image-20201024161632884](Android%E7%AC%94%E8%AE%B0-images/image-20201024161632884.png)

   - 在建立一个fonts目录。

     ![image-20201024161752925](Android%E7%AC%94%E8%AE%B0-images/image-20201024161752925.png)

     ![image-20201024161812812](Android%E7%AC%94%E8%AE%B0-images/image-20201024161812812.png)

**使用；**

- 在XML中使用

  ```xml
   <com.xuelingmiao.testapp.fonticon.IconView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="&#xe64b;"
          android:textColor="#333333"
          android:textSize="50sp"
          />
  ```

  

- Java代码中使用

  在java代码中要使用Unicode编码字符（及字体图标）

  格式；
  	`\ue[字符对应的Unicode编码]`
  如；
  ``&#xe899`对应Unicode编码是 `\ue899`

  ```java
  package com.xuelingmiao.testapp.fonticon;
  
  import androidx.appcompat.app.AppCompatActivity;
  
  import android.graphics.Color;
  import android.os.Bundle;
  import android.text.Layout;
  import android.widget.LinearLayout;
  
  import com.xuelingmiao.testapp.R;
  
  public class FontIcon extends AppCompatActivity {
  
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_font_icon);
          //创建icon控件
          IconView icon = new IconView(FontIcon.this);
          icon.setText("\ue615"); //指定图标
          icon.setTextSize(50);
          icon.setTextColor(Color.parseColor("#FF0000"));
          LinearLayout rootLayout = findViewById(R.id.root_layout);   //获取根元素
          rootLayout.addView(icon); //添加到布局上。
  
      }
  }
  ```




## XML和JSON

### 解析XML

**xml范例；**

>  以下演示中使用此xml作为样本。

```xml
<apps>
    <app>
        <id>1</id>
        <name>Google Maps</name>
        <version>1.0</version>
    </app>
    <app>
        <id>2</id>
        <name>Chrome</name>
        <version>2.1</version>
    </app>

    <app>
        <id>3</id>
        <name>Google Play</name>
        <version>2.3</version>
    </app>
</apps>
```



#### pull解析

##### 解析器

解析xml的过程就是把xml序列化为对象。

XmlPullParser一个xml解析器接口此接口实现类有；

- `KXmlParser`（通过 XmlPullParserFactory.newPullParser()）

  ```java
  XmlPullParser xmlParser = XmlPullParserFactory.newInstance().newPullParser();
  ```

- `ExpatPullParser`（通过 Xml.newPullParser()）

##### XmlPullParser解析事件

| 事件           | 说明               | 备注 |
| -------------- | ------------------ | ---- |
| START_TAG      | 解析到元素开始     |      |
| END_TAG        | 解析到元素结束     |      |
| END_DOCUMENT   | 解析到整个文档结束 |      |
| START_DOCUMENT | 解析到文档开始     |      |
|                |                    |      |
|                |                    |      |



##### XmlPullParser类

**方法；**

- `setInput()`  设置解析器将要处理的输入流。
  - 参数
    - InputStream  要解析的流
    - String 输入流编码 如 utf-8

- `getEventType()`  获取当前事件类型(START_TAG, END_TAG, TEXT, etc.) int编号

  - 返回值
    - int 事件对应的int数。

- `getName()` 获取当前元素名称 String类型。

- `nextText()` 获取开始元素的下一个内容。及元素中间的内容。

- `next()` 获取下一个解析事件，int类型返回事件对应的整数。

  



#### 演示

**步骤一；** 

根据xml数据建立对象类，用来序列化xml对象使用以此类作为xml对象的载体。如上面的xml文件中我们可以把app元素作为对象也就是一个类，把其中的id等元素作为此类的对象。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private int id;
    private String name,version;

    public App() {

    }

    public App(int id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "App{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", version='" + version + '\'' +
                '}';
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}

```

**步骤二；**

一步一步解析xml

1. 创建存放app对象的list集合。
2. 创建app对象变量。
3. 创建解析器
4. 配置解析源
5. 获取解析事件类型
6. 通过循环开始解析文档
7. 根据解析到元素开始事件，来处理xml中的元素，组装对应对象。
8. 根据解析到元素结束事件，把组装后的元素收集到集合中。
9. 遍历解析后的元素解析结束。

```java
        btnPostXml.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // 1. 创建存放app对象的list集合。
                ArrayList<App> apps = null;
                // 2. 创建app对象变量。
                App app = null;

                try {
                    // 3. 创建解析器
                    //通过xml解析器工厂获取一个解析器实例
                    XmlPullParser xmlParser = XmlPullParserFactory.newInstance().newPullParser();
                    // 4. 配置解析源
                    /*
                     * 设置xml文件源
                     * setInput(InputStream inputStream, String inputEncoding)
                     * 参数；
                     *   InputStream文件输入流
                     *   String 输入流编码 如 utf-8
                     * */
                    xmlParser.setInput(PostXmlActivity.this.getAssets().open("xml/test.xml"), "utf-8");
                    Log.d(TAG, "onClick: " + getAssets().open("xml/test.xml"));
                    //获取当前解析事件类型START_TAG, END_TAG, TEXT, etc
                    //5. 获取解析事件类型
                    int eventType = xmlParser.getEventType();
                    // 6. 通过循环开始解析文档
                    //当前解析事件不是文件结束文件事件就继续读取
                    while (eventType != XmlPullParser.END_DOCUMENT) {
                        //更新解析事件类型，同样也是结束循环条件
                        //next()//获取下一个解析事件
                        eventType = xmlParser.next();
                        switch (eventType) {
                            // 7. 根据解析到元素开始事件，来处理xml中的元素，组装对应对象。
                            case XmlPullParser.START_TAG:
                                if (xmlParser.getName().equals("apps")) {
                                    //如果当前解析到的元素是apps那么就创建一个存储app对象的集合。
                                    apps = new ArrayList<App>();

                                } else if (xmlParser.getName().equals("app")) {
                                    //如果是app元素就创建一个app对象。
                                    app = new App();
                                } else if (xmlParser.getName().equals("id")) {
                                    //把id元素中的数据赋值给app对象的id属性。
                                    app.setId(xmlParser.nextText());

                                } else if (xmlParser.getName().equals("name")) {
                                    app.setName(xmlParser.nextText());

                                } else if (xmlParser.getName().equals("version")) {
                                    app.setVersion(xmlParser.nextText());
                                }
                                break;
                            // 8.  根据解析到元素结束事件，把组装后的元素收集到集合中。
                            case XmlPullParser.END_TAG:
                                if (xmlParser.getName().equals("app")) {
                                    // 把app元素添加到集合中。
                                    apps.add(app);
                                }
                                break;

                        }
                    }
                    StringBuilder data = new StringBuilder();

                    // 9. 遍历解析后的元素
                    for (App tempApp : apps
                    ) {
//                        data.append(tempApp.toString());
                        data.append(tempApp.toString());
                        Log.d(TAG, "onClick: " + tempApp.toString());

                    }

                    //更新数据到UI
                    editResult.post(new Runnable() {
                        @Override
                        public void run() {
                            editResult.setText(data);
                        }
                    });


                } catch (XmlPullParserException | IOException e) {
                    e.printStackTrace();
                }
            }
        });
```



### pull生成XML

默认生成的xml是不包含换行符的。如果需要格式化输出使用`text("\n")`方法添加换行

#### 序列化器

- `XmlSerializer` xml序列化器。

  ```java
   // 获取解析器工程
   XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
   // 获取序列化器
   XmlSerializer serializer = factory.newSerializer();
  ```

#### XmlSerializer类

**方法；**

- `setOutput()`  设置输出流
  - 参数
    - OutputStream 指定输出的流。
    - String 指定流编码如 `utf-8`
- `startDocument()`  声明文档头信息及文档开始。
  - 参数
    - String  xml文档编码如`utf-8`
    - Boolean 是否是独立的。不需要可以设置为null
- `text(String)`  写入文本特殊字符串会自动转义。
- `startTag()`  写入元素开始标记
  - 参数；
    - String namespace 名称空间无名称空间可以写null
    - String name 元素名称
- `endTag(namespace,name)` 写入元素结束标记
- `attribute(namespace,name,value)` 写入元素属性;
  - 参数
    - String namespace 名称空间无名称空间可以写null
    - String name 属性名称
    - Stirng value 属性值
- `endDocument()`  结束整个文档写入操作。

#### 演示

1. 获取解析器工程
2. 获取序列化器
3. 配置输出位置
4.  设置xml文档头信息，也就是文档头开始。
5. 设置xml文档根元素开始
6. 生成其它元素
7. 设置根元素结束。
8. 设置xml文档结束

```java
        btnGenerateXml.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                try {
                    //1. 获取解析器工程
                    XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
                    //2. 获取序列化器
                    XmlSerializer serializer = factory.newSerializer();
                    //存放生成xml
                    ByteArrayOutputStream xml = new ByteArrayOutputStream();
                    //3. 配置输出位置
                    serializer.setOutput(xml, "utf-8");
                    //4. 设置xml文档头信息也就是文档头开始。
                    serializer.startDocument("utf-8", null);
                    serializer.text("\n"); //设置标签中内容
                    //5. 设置xml文档根元素开始
                    serializer.startTag(null, "apps");
                    serializer.text("\n");
                    //6. 生成其它元素
                    for (int i = 0; i < 2; i++) {
                        serializer.startTag(null, "app");
                        serializer.text("\n");	//添加换行

                        serializer.startTag(null, "id");
                        serializer.text("1");
                        serializer.endTag(null, "id");
                        serializer.text("\r\n");

                        serializer.startTag(null, "name");
                        serializer.text("Google Maps");
                        serializer.endTag(null, "name");
                        serializer.text("\r\n");

                        serializer.startTag(null, "version");
                        serializer.text("1.0");
                        serializer.endTag(null, "version");
                        serializer.text("\r\n");

                        serializer.endTag(null, "app");
                        serializer.text("\r\n");

                    }
                    //7. 设置根元素结束。
                    serializer.endTag(null, "apps");
                    //8. 设置xml文档结束
                    serializer.endDocument();

                    String data = xml.toString("utf-8");
                    Log.d(TAG, "onClick: 生成xml"+data);
                    //更新到UI
                    editResult.post(new Runnable() {
                        @Override
                        public void run() {

                            editResult.setText(data);
                        }
                    });


                } catch (XmlPullParserException | IOException e) {
                    e.printStackTrace();
                }

            }
        });
```

**生成内容展示；**

```xml
<?xml version='1.0' encoding='utf-8' ?><apps><app><id>1</id><name>Google Maps</name><version>1.0</version></app><app><id>1</id><name>Google Maps</name><version>1.0</version></app></apps>
```



### JSON

**json范例**

> 以下演示中使用此json作为样本。

```json
[
  {
    "id": "5",
    "version": "5.5",
    "name": "Clash of Clans"
  },
  {
    "id": "6",
    "version": "7.0",
    "name": "Boom Beach"
  },
  {
    "id": "7",
    "version": "3.5",
    "name": "Clash Royale"
  }
]
```



#### GSON

GitHub；https://github.com/google/gson

GSON是Google提供的一个操作json 的开源库。默认不在api中需要手动集成。

```groovy
dependencies {
  implementation 'com.google.code.gson:gson:2.8.6'
}
```



##### 解析JSON

json字符串反序列化到Java对象的过程。

**步骤一；**

创建一个json字符串中对象的实体类。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private String id,name,version;

    public App() {

    }

    public App(String id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "App{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", version='" + version + '\'' +
                '}';
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}

```

**步骤二；**

解析json字符串，并映射到实体类。

1. 装备JSON字符串
2. 实例化gson对象
3. 解析json字符映射到实体对象
4. 解析完成

```java
btnPullJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                try {
                    // 1. 装备JSON字符串。
                    InputStream  jsonFile = PostJsonActivity.this.getAssets().open("json/test.json");
                    ByteArrayOutputStream os = new ByteArrayOutputStream();
                    int len = 0; //标记读取有效字节数。
                    byte[] byteArr = new byte[1024];
                    //循环读取流
                    while ((len=jsonFile.read(byteArr)) != -1 ){
                        os.write(byteArr,0,len); //写入到输出流
                    }
                    String jsonStr = os.toString("utf-8");  //将流转换为字符串。
                    Log.d(TAG, "onClick: JsonStr"+jsonStr);
                    // 2. 实例化gson对象
                    Gson gson = new Gson();
                    // 3. 解析json字符映射到实体对象。
                    List<App> appList = gson.fromJson(jsonStr, new TypeToken<List<App>>()
                    {}.getType());
					
                    // 4. 解析完成
                    Log.d(TAG, "onClick: "+appList.toString());

                    //更新到UI
                    editJson.post(new Runnable() {
                        @Override
                        public void run() {
                             editJson.setText(appList.toString());
                             //输出单个数据
                            Log.d(TAG, "run: "+appList.get(0).getName());
                        }
                    });


                } catch (IOException e) {
                    e.printStackTrace();
                }


            }
        });


        //生成json
        btnGenerateJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

            }
        });
```



##### 生成JSON

类序列化为json字符串的过程。默认生成JSON是为格式化的

**步骤一；**

准备要序列化为json字符串的实体类。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private String id,name,version;

    public App() {

    }

    public App(String id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "App{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", version='" + version + '\'' +
                '}';
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}

```



**步骤二；**

类序列化为json字符串。

1. 准备要生成json的类的数据
2. 实例化为gson
3. 类序列化为json字符串

```java
        btnGenerateJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //1. 准备要生成json的类的数据。
                List<App> appList = new ArrayList<>();
                for (int i = 0; i < 2; i++) {
                    App app = new App();
                    app.setId("1");
                    app.setName("My App");
                    app.setVersion("1.0.0");
                    appList.add(app);
                }

                //2. 实例化为gson
                Gson gson = new Gson();
                //3. 类序列化为json字符串。
                String jsonStr = gson.toJson(appList, new TypeToken<List<App>>() {
                }.getType());
              

                Log.d(TAG, "onClick: 生成json" + jsonStr);
                //更新到UI
                editJson.post(new Runnable() {
                    @Override
                    public void run() {
                        editJson.setText(jsonStr);
                    }
                });

            }
        });
```



## Bugly日志收集

腾讯Bugly，为移动开发者提供专业的异常上报和运营统计，帮助开发者快速发现并解决异常，同时掌握产品运营动态，及时跟进用户反馈。

官网；https://bugly.qq.com/v2/

### 异常上报

#### 集成步骤

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

   

2. 在 AndroidManifest.xml 文件的 application 增加属性

   ```xml
   android:networkSecurityConfig="@xml/network_security_config"
   ```

   ![image-20201031201115622](Android%E7%AC%94%E8%AE%B0-images/image-20201031201115622.png)

   

**同时集成SDK和NDK**

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

   ![image-20201031202802010](Android%E7%AC%94%E8%AE%B0-images/image-20201031202802010.png)

#### 基本使用

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

![image-20201031203731471](Android%E7%AC%94%E8%AE%B0-images/image-20201031203731471.png)



**配置APP信息**

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

![image-20201031213824304](Android%E7%AC%94%E8%AE%B0-images/image-20201031213824304.png)



![image-20201031213805484](Android%E7%AC%94%E8%AE%B0-images/image-20201031213805484.png)



![image-20201031214901380](Android%E7%AC%94%E8%AE%B0-images/image-20201031214901380.png)



#### 增加上报进程控制【正确使用姿势】

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



### 应用升级

由于 Google Play 政策限制，请不要使用升级功能，否则可能被检测到违规而导致警告、下架甚至封禁账号等后果。

#### 集成

同样也需要对网络安全进行配置详细见上面的，异常上报中的**网络安全配置**。

##### 自动集成【推荐】

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

   

3. 配置FileProvider

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

   

   

4. 混淆配置

   为了避免混淆SDK，在Proguard混淆文件中增加以下配置

   ```
   -dontwarn com.tencent.bugly.**
   -keep public class com.tencent.bugly.**{*;}
   -keep class android.support.**{*;}
   ```



#### 测试验证

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

**发布新版本**

进入应用升级页面，点击发布新版本，上传要升级的APP的版本（**上传APP的versioncode必须不低于外发版本的versiocode，否则用户检测不到更新**）

![img](Android%E7%AC%94%E8%AE%B0-images/JIQ5U45I%7B_E%5DI3_AX%7D5%7BJ3.png)





## 多线程

[多线程](./多线程.md)



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







