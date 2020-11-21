# TextView【文本框】

主要用于在界面上显示一段文本信息

**属性；**

| 属性                                                 | 作用                                   | 值                                     |
| ---------------------------------------------------- | -------------------------------------- | -------------------------------------- |
| android:text                                         | 指定TextView中显示的文本内容           | 要显式的文本内容或@string/引用字符name |
| adnroid:textStyle                                    | 设置字体风格                           | normal(无效果) bold(加粗) italic(斜体) |
| android:maxLines                                     | 指定最大行数，超过最大行数会出现滚动条 | 取值int类型                            |
| android:ellipsize                                    | 文字显式不下展示点点点                 | 常用end，结合maxLines单行使用          |
| android:drawable[Right]("其它方向Top、Left、Bottom") | 在文字的右边显式一个icoon              | @drawable/图片name                     |
| android:drawablePadding                              | 设置图片内边距，改变图片距文字的距离   | 数字如（-15dp，15dp，15.5dp)           |
| android:focusable                                    | 当前控件设置为焦点                     | true / false                           |
| android:focusableInTouchMode                         | 在触摸模式下获得焦点                   | true / false                           |
| android:singleLine                                   | 是否单行显式                           | true / false                           |
| android:marqueeRepeatLimit                           | 设置文字滚动次数                       | marquee_forever永久，或int类型次数。   |
| android:textIsSelectable                             | 让文字可以被选择                       | true / false                           |

## 文字显式中划线【删除字】

~~文字显式中划线~~

```java
textView.getPaint().setFlags(Paint. STRIKE_THRU_TEXT_FLAG);
textView.getPaint().setAntiAlias(true)
package top.miku.uiwidgettest;

import androidx.appcompat.app.AppCompatActivity;

import android.graphics.Paint;
import android.os.Bundle;
import android.widget.TextView;

public class MyTextView extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my_text_view);
        TextView textView = (TextView) findViewById(R.id.del_word);
        textView.getPaint().setFlags(Paint. STRIKE_THRU_TEXT_FLAG);//设置中划线
        textView.getPaint().setAntiAlias(true);//消除锯齿

    }
}
```



## 文字显式下划线

<u>下划线文字</u>

```java
//下划线
        TextView textView1 = (TextView) findViewById(R.id.underline);
        textView1.getPaint().setFlags(Paint.UNDERLINE_TEXT_FLAG);//设置下划线
        textView1.getPaint().setAntiAlias(true);//消除锯齿
```



## 文字滚动【跑马灯】

- 必要属性和前提

  **显示的文字必须要超出给定的宽度或宽度**

  - `android:singleLine`
  - `android:ellipsize`
  - `android:marqueeRepeatLimit`
  - `android:focusable`
  - `android:focusableInTouchMode`

```xml
 <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp"
            android:text="@string/scrolling_text"
            android:singleLine="true"//单行显式
            android:ellipsize="marquee"//以跑马灯的方式显示(动画横向移动) 
            android:marqueeRepeatLimit="marquee_forever"//循环次数（永久）
            android:focusable="true"//控件获得焦点
            android:focusableInTouchMode="true"//触摸模式下获得焦点
            />
```



**解决部分手机不支持;**

1. 新建一个`MarqueTextView`类继承`AppCompatTextView`类重写里面的方法

   ```java
   package top.miku.uiwidgettest;
   
   import android.content.Context;
   import android.util.AttributeSet;
   
   import androidx.appcompat.widget.AppCompatTextView;
   
   public class MarqueTextView extends AppCompatTextView {
       public MarqueTextView(Context context, AttributeSet attrs, int defStyle) {
           super(context, attrs, defStyle);
       }
   
       public MarqueTextView(Context context, AttributeSet attrs) {
           super(context, attrs);
       }
   
       public MarqueTextView(Context context) {
           super(context);
       }
   
       //覆盖重写获得焦点方法
       @Override
       public boolean isFocused() {
           return true;
       }
   }
   ```

2. 到布局xml中使用自定义的这个控件

   ```xml
   <top.miku.uiwidgettest.MarqueTextView //包名+自定义控件名
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:textSize="20sp"
               android:text="@string/scrolling_text"
               //以下是必要属性
               android:singleLine="true"
               android:ellipsize="marquee"
               android:marqueeRepeatLimit="marquee_forever"
               android:focusable="true"
               android:focusableInTouchMode="true"/>
   ```









