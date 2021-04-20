# Intent【意图】

## 介绍
Intent是Android程序中各组件之间进行交互的一种重要方式，它不仅可以指明当前组件想要执行的动作，还可以在不同组件之间传递数据。Intent一般可被用于启动活动、启动服务以及发送广播等。



## 显示Intent

所为显式Intent，在创建Intent对象时明确指定了要启动组件的名称。也就是明确知道要启动的组件名称。

**示例；**

从活动1启动活动2

- 在创建一个新的活动（活动2）【具体步骤可以参考，四大组件之Activity中使用AS的空activity模板创建部分】

  ![1566485434027](intent-images/1566485434027.png)

- 这次我们勾选创建布局文件

  ![1566485703390](intent-images/1566485703390.png)

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



- Activity类中提供了一个`startActivity()` 方法，这个方法是专门用于启动活动的，它接收一个Intent 参数。

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



## Intent类

**构造函数；**

- `Intent(Context packageContext, Class<?> cls)` 。这个构造函数接收两个参数。
  - 参数
    1. 第一个参数Context 要求提供一个启动活动的上下文。
    2. 第二个参数Class 则是指定想要启动的目标活动，通过这个构造函数就可以构建出Intent 的“意图”。



## 隐式Intent

相比于显式Intent，隐式Intent则含蓄了许多，它**并不明确指出**我们想要启动哪一个活动，而是指定了一系列更为抽象的**action** 和**category** 等信息，然后交由系统去分析这个Intent，并帮我们找出合适的活动去启动。什么叫作合适的活动呢？简单来说就是可以响应我们这个隐式Intent的活动

![image-20191123211151237](intent-images/image-20191123211151237.png)

### Intent过滤器

过滤器是当使用隐藏Intent设置的一些action和data等这些属性就叫做过滤器。

#### 设置过滤器

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