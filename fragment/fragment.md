# Fragment

可以在activity中嵌套部分页面为Fragment页面同样也支持同一个Fragment重用。类似于HTML中的iframe标签

## 生命周期

一个Fragment必须被嵌入到activity中。它的生命和其所在的activity紧密关联，当activity被销毁那么同样fragment也会被销毁。

![image-20191122125552809](fragment-images/image-20191122125552809.png)



## 在Activity中使用

### 静态添加

**创建**

1. 创建一个javaClass并继承自**Fragment**类
2. 创建一个布局文件xml【书写自己要展示的布局内容】
3. 在继承的了Fragment的class中重写`onCreateView`方法，绑定布局文件。

- `inflater.inflate()`
  - 参数1 布局文件id
  - 参数2 ViewGroup对象直接使用方法中的形参container即可
  - 参数3 指定为false

```java
package top.miku.testfragment;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;

public class Fragment1 extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        //加载布局文件
        //inflate方法参数
        //参数1 布局文件id 参数2 ViewGroup对象直接使用方法中的形参container即可 参数3 指定为false
        View view = inflater.inflate(R.layout.fragment_fragment1, container,false);


        return view; //返回这个view。
    }
}
```

**Activity中添加Fragment**

<img src="fragment-images/image-20191122171025122.png" alt="image-20191122171025122" style="zoom: 25%;" />

- 活动xml布局中引用

1. 在获得布局中添加fragment标记。

2. 通过android:name属性指定Fragment类所在的路径包含包名全路径。

3. **注意** 标记中必须为其设置一个id否则会报错无法启动

   ```xml
   <fragment
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:name="top.miku.testfragment.Fragment1" //指定类
           android:id="@+id/fragment1" //必须指定id
           />
   ```

### 代码动态添加

- `getSupportFragmentManager()`获取FragmentManager管理对象
- `fragmentManager.beginTransaction()`获取片段交易对象
- `transaction.add()` 添加要提交的fragment对象
  - 参数1 要添加到那个容器上容器id
  - 参数2 fragment对象
  - 参数3可选 一个tag标记
- `transaction.commit();` 提交交易

```java
package top.miku.testfragment;

import androidx.appcompat.app.AppCompatActivity;

import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //实例化一个要敲入活动中的Fragment对象
        Fragment2 fragment2 = new Fragment2();

        //获取FragmentManager管理对象
        FragmentManager fragmentManager = getSupportFragmentManager();
        //开启片段交易
        FragmentTransaction transaction = fragmentManager.beginTransaction();
        //添加要提交的fragment对象
        //参数1 要添加到那个容器上容器id 参数2 fragment对象 参数3可选 一个tag标记。
        transaction.add(R.id.layout,fragment2);
        //提交交易
        transaction.commit();

    }
}
```



## 仿写微信的选项卡效果

![fragment](fragment-images/fragment.gif)

**xml布局**

- main.ml

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:app="http://schemas.android.com/apk/res-auto"
          xmlns:tools="http://schemas.android.com/tools"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          tools:context=".MainActivity"
          android:orientation="vertical">
      <fragment
              android:id="@+id/fragment"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:name="top.miku.wechatfragment.Fragment1"/>
      <LinearLayout
              android:layout_width="match_parent"
              android:layout_height="50dp"
              android:layout_alignParentBottom="true"
              android:orientation="horizontal">
  
          <Button
                  android:id="@+id/btn1"
                  android:layout_width="0dp"
                  android:layout_height="wrap_content"
                  android:text="界面1"
                  android:layout_weight="1"/>
  
          <Button
                  android:id="@+id/btn2"
                  android:layout_width="0dp"
                  android:layout_height="wrap_content"
                  android:text="界面2"
                  android:layout_weight="1"/>
  
          <Button
                  android:id="@+id/btn3"
                  android:layout_width="0dp"
                  android:layout_height="wrap_content"
                  android:text="界面3"
                  android:layout_weight="1"/>
      </LinearLayout>
  
  </RelativeLayout>
  ```

- Fragment.xml其它三个代码相似。

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
          android:layout_width="match_parent" android:layout_height="match_parent"
          android:background="#F805F4">
  
      <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_centerInParent="true"
              android:text="界面一"
              android:textSize="50sp"/>
  
  </RelativeLayout>
  ```

**java**

- fragment其它几个代码一致只是布局文件指定不一样。

  ```java
  package top.miku.wechatfragment;
  
  import android.os.Bundle;
  import android.view.LayoutInflater;
  import android.view.View;
  import android.view.ViewGroup;
  
  import androidx.annotation.NonNull;
  import androidx.annotation.Nullable;
  import androidx.fragment.app.Fragment;
  
  public class Fragment1 extends Fragment {
      @Nullable
      @Override
      public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
          View view = inflater.inflate(R.layout.fragment1,container,false);
          return view;
      }
  }
  ```

- main

  - `transaction.replace()` 替换fragment
    - 参数1 要嵌入到页面上那个容器的id
    - 参数2 fragment实例对象。

  ```java
  package top.miku.wechatfragment;
  
  import androidx.appcompat.app.AppCompatActivity;
  import androidx.fragment.app.Fragment;
  import androidx.fragment.app.FragmentManager;
  import androidx.fragment.app.FragmentTransaction;
  
  import android.os.Bundle;
  import android.view.View;
  import android.widget.Button;
  
  public class MainActivity extends AppCompatActivity {
      Button btn1, btn2, btn3;
  
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
  
          btn1 = findViewById(R.id.btn1);
          btn2 = findViewById(R.id.btn2);
          btn3 = findViewById(R.id.btn3);
  
          /*设置监听事件 事件处理函数设置为定义的v*/
          btn1.setOnClickListener(v);
          btn2.setOnClickListener(v);
          btn3.setOnClickListener(v);
  
      }
  
      //创建单击事件监处理方法。
      View.OnClickListener v = new View.OnClickListener() {
          @Override
          public void onClick(View v) {
              //获取Fragment
              FragmentManager fragmentManager = getSupportFragmentManager();
              //开启一个事务
              FragmentTransaction transaction = fragmentManager.beginTransaction();
              Fragment fragment = null; //存放实例化的Fragment
              switch (v.getId()) {
                  case R.id.btn1:
                      fragment = new Fragment1();
                      break;
                  case R.id.btn2:
                      fragment = new Fragment2();
                      break;
                  case R.id.btn3:
                      fragment = new Fragment3();
                      break;
                  default:
                      break;
              }
  
              //替换Fragment
              transaction.replace(R.id.fragment,fragment);
              transaction.commit(); //提交
          }
      };
  }
  ```