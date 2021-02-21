# RadioButton【单选按钮】

![1567406274266](radio_button-images/1567406274266.png)

长用于性别的选择，要集合`<RadioGroup></RadioGroup>`打组使用

**属性**

| 属性                | 作用                         | 值                                 |
| ------------------- | ---------------------------- | ---------------------------------- |
| adnroid:checked     | 前提必须设置id默认是否被选中 | Boolean                            |
| android:orientation | 设置显式方向                 | vertical【垂直】horizontal【水平】 |

**事件监听**

```java
package top.miku.uiwidgettest;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.Toast;

public class MyRadioButton extends AppCompatActivity {

    private RadioGroup radioGroup;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my_radio_button);
        radioGroup = (RadioGroup) findViewById(R.id.radio_group);
        //注册被修改事件
        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup radioGroup, int i) {//int i当前被选中的radioButton的id
                Toast toast = Toast.makeText(MyRadioButton.this,null,Toast.LENGTH_SHORT);
                //通过radioGroup获得radioButton控件
                RadioButton radioButton = (RadioButton) radioGroup.findViewById(i);
                toast.setText(radioButton.getText());
                toast.show();
            }
        });
    }
}
```