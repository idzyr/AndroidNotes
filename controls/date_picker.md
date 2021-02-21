# DatePicker【日期选择器】

**事件监听**

```java
package top.miku.viewtime;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.DatePicker;
import android.widget.Toast;

import java.util.Calendar;

public class MainActivity extends AppCompatActivity {

    private int year,month,day; //定义存放年月日变量
    private DatePicker datePicker;//存放日期View
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        datePicker = (DatePicker) findViewById(R.id.my_date_picker);
        /*获取当前系统的日期*/
        Calendar calendar = Calendar.getInstance();//获取一个java的日历对象。
        year = calendar.get(Calendar.YEAR);
        month = calendar.get(Calendar.MONTH);
        day = calendar.get(Calendar.DAY_OF_MONTH);

        /*通过当前日期初始化DatePicker对象*/
        /*参数
        * 1. Calendar类型的年
        * 2. Calendar类型的月
        * 3。Calendar类型的日
        * 4. 日期改变监听器
        * */

        datePicker.init(year, month, day, new DatePicker.OnDateChangedListener() {
            @Override
            public void onDateChanged(DatePicker datePicker, int i, int i1, int i2) {
                //把改变的日期赋值给定义存放日期的成员变量。
                MainActivity.this.year = i;
                MainActivity.this.month = i1;
                MainActivity.this.day = i2;

                show(year,month,day);//显式日期
            }
        });
    }
    ///显式选择的日期
    private void show(int year,int month,int day){
        String str = year+"年"+(month+1)+"月"+day+"日";
        Toast toast = Toast.makeText(MainActivity.this,null,Toast.LENGTH_SHORT);
        toast.setText(str);
        toast.show();


    };
}
```

