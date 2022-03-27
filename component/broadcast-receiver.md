# BroadcastReceiver【广播接收者】

## BroadcastReceiver是什么鬼？

答：Broadcast直译广播，我们举个形象的例子来帮我理解下BroadcastReceiver，记得以前读书 的时候，每个班级都会有一个挂在墙上的大喇叭，用来广播一些通知，比如，开学要去搬书，广播： "每个班级找几个同学教务处拿书"，发出这个广播后，所有同学都会在同一时刻收到这条广播通知， 收到，但不是每个同学都会去搬书，一般去搬书的都是班里的"大力士"，这群"大力士"接到这条 广播后就会动身去把书搬回可是！
——好吧，上面这个就是一个广播传递的一个很形象的例子：
`大喇叭--> 发送广播 --> 所有学生都能收到广播 --> 大力士处理广播`
回到我们的概念，其实BroadcastReceiver就是应用程序间的全局大喇叭，即通信的一个手段， 系统自己在很多时候都会发送广播，比如电量低或者充足，刚启动完，插入耳机，输入法改变等， 发生这些时间，系统都会发送广播，这个叫系统广播，每个APP都会收到，如果你想让你的应用在接收到 这个广播的时候做一些操作，比如：系统开机后，偷偷后台跑服务~哈哈，这个时候你只需要为你的应用 注册一个用于监视开机的BroadcastReceiver，当接收到开机广播就做写偷偷摸摸的勾当~ 当然我们也可以自己发广播，比如：接到服务端推送信息，用户在别处登录，然后应该强制用户下线回到 登陆界面，并提示在别处登录~

## 广播类型

### 标准广播

完全**异步执行**的广播，发出广播后，**所有**广播接收器几乎会在同一时刻收到这条广播通知

### 有序广播

**同步执行**的一种广播，发出广播后，**同一时间只有一个**广播接受者能收到，当这个广播接收者的逻辑执行完后，才会传递到下一个接收者；当然，前面的接受者还可以**阶段**广播的继续传递，那么后续接受者就无法收到广播信息了



## 接收系统广播

### 注册广播接收器

要想接收系统广播，我们的APP注册广播接收器哦！

#### 动态注册

就是在Java代码中指定`IntentFilter`，然后添加不同的Action即可，想监听什么广播就写什么Action，另外动态注册的广播，一定要调用`unregisterReceiveri`让广播取消注册

#### 静态注册

动态注册需程序**启动**后才能接收广播，静态广播就弥补了这个短板，在`AndroidManifest`中制定`<IntentReceiver>`就可以让程序在未启动的情况下接收到广播了

### 监听网络状态变化(动态注册)

![receiver-wifi](broadcast-receiver-images/receiver-wifi.gif)

1. 创建一个类继承`android.content.BroadcastReceiver`并重写`public void onReceive(Context context, Intent intent)`

   ```java
   public class MyBRReceiver extends BroadcastReceiver {
       @Override
       public void onReceive(Context context, Intent intent) {
   
       }
   }
   ```

   

2. 在重写的`onReceive`方法内处理接收到广播后的逻辑。

   ```java
     	@Override
       public void onReceive(Context context, Intent intent) {
           // 当收到WiFi广播后会执行
           Toast.makeText(context, "WiFi状态发生了改变", Toast.LENGTH_SHORT).show();
       }
   ```

   

3. 在Activity中动态注册

   1. 创建接收器类实力
   2. 创建Intent过滤器，只保留我们需要的广播
   3. 使用`registerReceiver()` 方法注册广播

   ````java
     private  MyBRReceiver myBRReceiver;
       @Override
       public void onClick(View view) {
           int id = view.getId();
           if (id == R.id.receiver_system_dynamic) {
               myBRReceiver = new MyBRReceiver();
               IntentFilter intentFilter = new IntentFilter();
               // 过滤WiFi动作信息
               intentFilter.addAction("android.net.conn.CONNECTIVITY_CHANGE");
               registerReceiver(myBRReceiver, intentFilter);
           }
       }
   ````

   

4. 取消注册，一般是在Activity的`onDestroy()` 生命周期方法内调用`unregisterReceiver（）`方法取消注册。

   ```java
       @Override
       protected void onDestroy() {
           super.onDestroy();
           unregisterReceiver(myBRReceiver);
       }
   ```

   

### 接收开机广播(静态注册)

![receiver-static](broadcast-receiver-images/receiver-static.gif)

1. 和上面动态注册一样先要搞一个继承自`BroadcastReceiver` 接收器类。

   ````java
   import android.content.BroadcastReceiver;
   import android.content.Context;
   import android.content.Intent;
   import android.widget.Toast;
   
   public class BootCompleteReceiver extends BroadcastReceiver {
   
       @Override
       public void onReceive(Context context, Intent intent) {
           Toast.makeText(context, "开机完毕~", Toast.LENGTH_LONG).show();
       }
   }
   ````

   

2. 在`AndroidManifest.xml`中对我们的接收器`BroadcastReceiver`进行注册，注意是`application`节点内并配置`intent-filter`还需要``RECEIVE_BOOT_COMPLETED`权限

   ```xml
   <!-- 权限 -->
   <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
    <receiver
               android:name=".BootCompleteReceiver"
               android:enabled="true"
               android:exported="true">
               <intent-filter>
                   <action android:name="android.intent.action.BOOT_COMPLETED"/>
               </intent-filter>
   </receiver>
   ```

   属性；

   - `exported` 是否允许这个广播接收器接收本程序以外的广播
   - `enabled` 否启用这个广播接收器 







