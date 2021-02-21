### Chronometer【计时器】

**属性**

| 属性           | 作用           | 值                                                           |
| -------------- | -------------- | ------------------------------------------------------------ |
| android:format | 设置计时器格式 | %s已时分秒格式显式时间【可以加入其它内容保证有时间格式即可】 |

**方法**

- `getBase()`：返回时间。
- `setBase(long base)`：设置计时器的起始时间。
- `start()`：开始计时。
- `stop()：`停止计时。**假停止计时**只是不在刷新计时控件，实际一直在运行中。
- `setFormat(String format)：`设置显示时间的格式。

**事件**

- 开始 停止 重置 简单计时器

  ```java
  package top.miku.mytimer;
  
  import androidx.appcompat.app.AppCompatActivity;
  
  import android.os.Bundle;
  import android.os.SystemClock;
  import android.util.Log;
  import android.view.View;
  import android.widget.Button;
  import android.widget.Chronometer;
  
  public class MainActivity extends AppCompatActivity {
      private  Chronometer chronometer; //保存计时器控件
      private Button start,stop,reset; //保存按钮
      private long sumTime = 0; //记录总时间 也就是计时器走的时间。
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          //获取控件资源
          chronometer = (Chronometer) findViewById(R.id.my_timer);
          start = (Button) findViewById(R.id.start);
          stop = (Button) findViewById(R.id.stop);
          reset = (Button) findViewById(R.id.reset);
  
          chronometer.setFormat("%s");//设置计时器格式。
  
          //开始
          start.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View view) {
                  /*
                  * SystemClock.elapsedRealtime()//从设备开机到现在的时间，
                  * 单位毫秒，含系统深度睡眠时间
  
                   *
                  * */
                  //当前系统时间减去总时间【触发停止按钮记入的时间】得到上次暂停的时间
                  chronometer.setBase(SystemClock.elapsedRealtime() - sumTime);
                  chronometer.start();//开始计时
  
              }
          });
  
          //停止
          stop.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View view) {
                  chronometer.stop();//停止计时，实际是停止刷新计时控件的数据，实际计时器一直工作中。
                  //就是这样写
                  sumTime = SystemClock.elapsedRealtime() - chronometer.getBase();
              }
          });
  
          //重置
          reset.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View view) {
                  sumTime = 0; //重置总时间
                  chronometer.setBase(SystemClock.elapsedRealtime());//计时器归零
              }
          });
  ```

- 监听计时器改变

  ```java
  chronometer.setOnChronometerTickListener(new Chronometer.OnChronometerTickListener() {
              @Override
              public void onChronometerTick(Chronometer chronometer) {
  
                  if ((SystemClock.elapsedRealtime() - chronometer.getBase()) >= 20000){
                      Toast.makeText(MainActivity.this,"计时到大20秒了",Toast.LENGTH_SHORT).show();
                  }
              }
          });
  ```