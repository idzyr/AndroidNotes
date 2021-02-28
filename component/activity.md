# Activity【活动】
## 介绍
活动（Activity）是最容易吸引用户的地方，它是一种可以包含用户界面的组件，主要用于和用户进行交互。一个应用程序中可以包含零个或多个活动，但不包含任何活动的应用程序很少见，谁也不想让自己的应用永远无法被用户看到吧？

## 使用AS手动创建一个活动

### 创建不包含活动的项目；

- 创建一个项目

  启动AS，在欢迎界面。选择启动新的AS项目。

  ![1566199434812](activity-images/1566199434812-1600785160710.png)

  

- 不带活动

  ![1566376899383](activity-images/1566376899383.png)

- 配置项目

  ![1566376994556](activity-images/1566376994556.png)

  

- 在`app/src/main/java/top.miku.activitytest`创建一个活动

  依次选择

  ![1566377890271](activity-images/1566377890271.png)

- 这里暂时不创建布局文件

![1566378042599](activity-images/1566378042599.png)

项目中的任何活动都应该重写Activity的`onCreate()`方法，而目前我们的FirstActivity中已经重写了这个方法，这是由Android Studio自动帮我们完成的，代码如下所示：

```java
package top.miku.activitytest;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle; //向下兼容

public class FirstActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
}
```

### 创建和加载布局xml

- 在`app/src/main/res`目录创建layout目录

  ![1566378655820](activity-images/1566378655820.png)

  

- 接着在layout目录下创建first_layout.xml

  ![1566378864402](activity-images/1566378864402.png)

  

![1566378922750](activity-images/1566378922750.png)

- 编辑布局文件，添加一个button

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="vertical" android:layout_width="match_parent"
      android:layout_height="match_parent">
      <!-- 定义一个button控件 -->
      <Button
          android:layout_width="match_parent" //宽度 match_parent继承子父级
          android:layout_height="wrap_content"//高度 wrap_content刚好包裹里面的内容
          android:id="@+id/button_1" //给按钮添加一个id属性
          android:text="Button_1"//按钮中显示的内容
          />
  </LinearLayout>
  ```

- 到`FirstActivity.java`文件中设置布局文件

  ```java
  package top.miku.activitytest;
  
  import androidx.appcompat.app.AppCompatActivity;
  
  import android.os.Bundle;
  
  public class FirstActivity extends AppCompatActivity {
  
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.first_layout);//引入布局
      }
  }
  ```

### 注册活动

在`AndroidManifest`文件中注册活动。

- 打开`app/src/main/AndroidManifest.xml`中注册活动【一般IDE会自动注册】

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
      package="top.miku.activitytest"> //package=指定包
  
      <application
          android:allowBackup="true"
          android:icon="@mipmap/ic_launcher"
          android:label="@string/app_name"
          android:roundIcon="@mipmap/ic_launcher_round"
          android:supportsRtl="true"
          android:theme="@style/AppTheme">
          <!-- 注册一个活动 -->
          //android:name指定要注册的活动因为外层已经声明了包所以这里可以忽略直接写.FirstActivity
          //android:label 指定活动标题
          <activity android:name=".FirstActivity" android:label="@string/app_name">
              <!-- 把当前活动设置为主活动【程序启动的第一个活动】 -->
                <intent-filter>
                  <!-- 暂时固定写法两行声明 -->
                  <action android:name="android.intent.action.MAIN"></action>
                  <category android:name="android.intent.category.LAUNCHER" />
              </intent-filter>
          </activity>
      </application>
  
  </manifest>
  ```



## 以类的方式创建活动

1. 在包下创建一个class并继承AppCompatActivity

   ![1568437173840](activity-images/1568437173840.png)![1568437302736](activity-images/1568437302736-1600847401228.png)
   
2. 在layout文件下新建布局文件。

   ![1568437408702](activity-images/1568437408702.png)

3. 到class中去重写`protected void onCreate(Bundle bundle)`方法

   ```java
   package top.miku.uiwidgettest;
   
   import android.os.Bundle;
   
   import androidx.appcompat.app.AppCompatActivity;
   
   public class Test extends AppCompatActivity {
      @Override
      protected void onCreate(Bundle bundle) {
          super.onCreate(bundle);
          //绑定布局文件
          setContentView(R.layout.activity_test);
      }
   }
   ```

4. 到AndroidManifest.xml文件中注册这个活动

   ```xml
    <activity
                   android:name=".Test" //活动名
                   android:label="测试"/>
   ```



## 启动Activity

![image-20191119204959631](activity-images/image-20191119204959631.png)

Activity有两种启动方式，一是作为app的主activity启动。二是被其他activity启动。

### 主启动activity

> AndroidManifest.xml

在AndroidManifest.xml注册活动时添加`intent-filter`标记

```xml
 <activity android:name=".MainActivity">
            <!-- 设置为主活动 -->
            <intent-filter>
                <!-- 指定响应的动作名 android.intent.action.MAIN意思是作为app的主启动活动-->
                <action android:name="android.intent.action.MAIN" />
                <!-- 在什么环境下动作才会被响应 -->
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```

### 启动其它活动

> startActivity()

```java
package top.miku.testactivity;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btn1 = (Button) findViewById(R.id.new_activity);

        btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //实例intent对象，
                //参数1 packageContext 【上下文对象】和MainActivity有继承关系所以可以直接使用子类。
                //参数2 要启动的活动【活动名+.class】
                Intent intent = new Intent(MainActivity.this, NewActivity.class);
                //使用startActivity方法启动这个活动参数为intent
                startActivity(intent);
            }
        });
    }
}
```

### 关闭活动

调用`finish();`方法关闭活动【销毁活动】



## Activity之间跳转





## Activity之间数据传递

### 使用Bundle传值

> **参考；**
>
> Bundle类https://developer.android.google.cn/reference/android/os/Bundle?hl=en

![image-20191120143224571](activity-images/image-20191120143224571.png)

**方法**

- `put[String](key,value)`存储要保存的数据 字符串类型。**其它类型更换[]括号中的其它类型即可**，如`putString("键名","值");`

#### 把数据传递给下一个Activity

> **注意；**
>
> 如果要想当用户按下Back键后也返回数据那么需要重写键盘回调事件。也要返回数据

从活动1传递数据到活动2

**保存数据【活动1】；**

1. `bundle.putString(key,value)`以键值对形式存放要传递的数据。
2. `intent.putExtras(bundle)`把bundle保存到intent中。当然putExtras()也可以直接传输数据

```java
  package top.miku.testbundle;

  import androidx.appcompat.app.AppCompatActivity;

  import android.content.Intent;
  import android.os.Bundle;
  import android.view.View;
  import android.widget.Button;
  import android.widget.TextView;

  public class MainActivity extends AppCompatActivity {

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);

          Button send = (Button) findViewById(R.id.btn_send);


          send.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View v) {
                  TextView txt = (TextView) findViewById(R.id.txt);

                  //创建Intent对象
                  Intent intent = new Intent(MainActivity.this,Main2Activity.class);

                  //实例化bundle对象
                  Bundle bundle = new Bundle();
                  //以键值对形式存放要传递的数据。
                  bundle.putString("txt",txt.getText().toString());

                  //把bundle保存到intent中。
                  intent.putExtras(bundle);
                  //启动另一个活动【活动2】
                  startActivity(intent);

              }
          });

      }
  }
```

**获取数据【活动2】；**

1. `getIntent()`获取上一个活动的Intent
2. `intent.getExtras()`获取传递来的bundle
3. `bundle.getString(key)`通过key获取存储的数据

```java
package top.miku.testbundle;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;

public class Main2Activity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        //获取上一个活动的Intent
        Intent intent = getIntent();

        //获取传递来的bundle
        Bundle bundle = intent.getExtras();

        //通过key获取存储的数据
        String str = bundle.getString("txt");

        //显式纯度的数据
        TextView textView = findViewById(R.id.txt2);
        textView.setTextSize(20);
        textView.setText(str+"从上个活动中获得的内容");

    }
}
```

#### 返回数据给上一个活动

调用另一个Activity并返回数据给调用者【上一个Activity】

![IntentBundle](activity-images/IntentBundle.gif)

**xml布局**

- MainActivity.xml布局

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:app="http://schemas.android.com/apk/res-auto"
          xmlns:tools="http://schemas.android.com/tools"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          tools:context=".MainActivity">
      <!-- 使用帧布局可以实现叠加效果 -->
      <FrameLayout 
              android:layout_width="200dp"
              android:layout_height="200dp">
  
          <ImageView
                  android:id="@+id/avatar"
                  android:layout_width="wrap_content"
                  android:layout_height="wrap_content"
                  android:src="@mipmap/myhero_36"/>
  
          <Button
                  android:id="@+id/set_avatar"
                  android:text="点击修改头像"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                  android:layout_gravity="bottom"
                  android:background="#72666666"
                  android:textSize="20sp"/>
  
      </FrameLayout>
  </LinearLayout>
  ```

- 选择头像activity.xml布局

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:app="http://schemas.android.com/apk/res-auto"
          xmlns:tools="http://schemas.android.com/tools"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          tools:context=".ChooseAvatar">
      <!-- 稍后使用适配器添加内容 -->
      <GridView
              android:id="@+id/grid_view"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:numColumns="auto_fit"/>
  
  </LinearLayout>
  ```

**java代码；**

- Main.java

  - `startActivityForResult();`启动要返回数据的活动，
    - 参数1 要启动的Intent
    - 参数2 一个请求码一般是以0x开始。十六进制

  - `protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data)`  重写此方法接收返回的数据

```java
package top.miku.testbundle2;

import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;

import java.util.Map;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.set_avatar);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                /*———————————————————启动要返回数据的Intent————————————————————-*/
                Intent intent = new Intent(MainActivity.this, ChooseAvatar.class);
                //使用startActivityForResult方法启动活动
                //参数1 要启动的Intent 参数2 一个请求码一般是以0x开始。
                startActivityForResult(intent,0x00);
            }
        });
    }
    /*——————————————接收返回的结果————————————————————————*/
    //重写onActivityResult方法

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        //判断请求码和返回码是否一致，一致后再获取数据
        if (requestCode == 0x00 && resultCode == 0x00){
            //获取返回的bundle对象
            Bundle bundle = data.getExtras();
            //通过bundle方法获取对应key的数据
            int imageId = bundle.getInt("imageId"); //获取图片资源id

            /*————————————————对获取的数据进行处理————————————————*/
            //把获取到的图片资源id设置给当前活动中ImageView控件
            ImageView imageView = findViewById(R.id.avatar);
            imageView.setImageResource(imageId);

        }
    }
}
```

选择头像.java

- 通过创建Bundle对象，把数据存入bundle中再存入Intent中

- setResult();  设置返回数据
  - 参数1 返回码一般设置和请求码一致。
  - 参数2 要返回带有数据的Intent对象

```java
  package top.miku.testbundle2;

  import androidx.appcompat.app.AppCompatActivity;

  import android.content.Context;
  import android.content.Intent;
  import android.os.Bundle;
  import android.view.View;
  import android.view.ViewGroup;
  import android.widget.AdapterView;
  import android.widget.BaseAdapter;
  import android.widget.GridLayout;
  import android.widget.GridView;
  import android.widget.ImageView;

  public class ChooseAvatar extends AppCompatActivity {

      private int[] imgs = new int[]{
              R.mipmap.myhero_36,R.mipmap.myhero_47,R.mipmap.myhero_70,
              R.mipmap.myhero_76,R.mipmap.myhero_81,R.mipmap.ic_launcher
      };
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_choose_avatar);
          /*———————————————————展示头像——————————*/
          GridView gridView = findViewById(R.id.grid_view);
          gridView.setAdapter(new ImageAdapter(this));    //设置适配器


          /*——————————————返回数据给上一个活动——————————————————*/

          //监听选项点击事件
          gridView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
              @Override
              public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                  //获取Intent对象，主要用来传递数据
                  Intent intent = getIntent();
                  //创建Bundle主要用来保存数据。
                  Bundle bundle = new Bundle();
                  //保存当前选中项的图片id
                  //position就是当前选中项的index通过这个索引就可以从图片数组中找到对应的图片资源id了
                  bundle.putInt("imageId",imgs[position]);

                  //保存到Intent
                  intent.putExtras(bundle);

                  //设置返回码,并返回intent对象
                  //参数1 返回码一般设置和请求码一致。 参数2 要返回带有数据的Intent对象
                  setResult(0x00,intent);

                  finish();   //关闭当前活动
              }
          });

      }
  //继承BaseAdapter编写自己的适配器
      public class ImageAdapter extends BaseAdapter{
          //存放实例化时构造函数中的上下文对象。
          private Context mContext;

          //带有上下文对象的构造函数
          public ImageAdapter(Context context){
              mContext = context; //保存上下文对象
          }

          //计数
          @Override
          public int getCount() {
              return imgs.length; //返回图片数组的长度
          }

          @Override
          public Object getItem(int position) {
              return null;
          }

          @Override
          public long getItemId(int position) {
              return 0;
          }

          @Override
          public View getView(int position, View convertView, ViewGroup parent) {
              ImageView imageView; //保存组件

              //进行判断
              if (convertView == null){
                  //等于空就自己创建一个image组件
                  imageView = new ImageView(mContext);    //上下文就是构造中传递的

                  //设置图片大小
                  imageView.setLayoutParams(new GridView.LayoutParams(200,200));

              }else {
                  //不等于空，就保存这个组件，强制类型转换为image组件
                  imageView = (ImageView) convertView;
              }
              //设置图片资源id
              //position 当前项的index
              imageView.setImageResource(imgs[position]);
              return imageView; //返回这个组件
          }
      }
  }
```

