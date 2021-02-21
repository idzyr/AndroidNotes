# EditText【可编辑文本框】

**功能；**

EditText是程序用于和用户进行交互的另一个重要控件，它允许用户在控件里输入和编辑内容，并可以在程序中对这些内容进行处理**。它继承自TextView所以也可以使用TextView中的属性**

**属性；**

| 属性              | 作用                                             | 值             |
| ----------------- | ------------------------------------------------ | -------------- |
| android:hint      | 指定一段提示性的文本                             | 提示的文本内容 |
| android:maxLines  | 指定EditText的最大行数，超过最大行数会出现滚动条 | 取值int类型    |
| android:inputType | 指定输入框类型                                   |                |

## 获取用户输入的内容

- 注册事件，并添加处理逻辑

```java
package top.miku.uiwidgettest;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MyEditText extends AppCompatActivity implements View.OnClickListener {
    private static final String TAG = "MyEditText";
    //生命一个EditText类型的成员变量
    private EditText editText;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my_edit_text);
        //获取button和editText
        Button button = (Button) findViewById(R.id.button_1);
        editText = (EditText) findViewById(R.id.edit_text);
        //以接口方式实现onClick事件监听
        button.setOnClickListener(this);
    }

    @Override
    public void onClick(View view) {
        //把获取到的内容转换为字符串
        String inputText = editText.getText().toString();
        //通用Toast展示输入的内容。
//        Toast.makeText(MyEditText.this,inputText,Toast.LENGTH_SHORT).show();
        //解决小米手机再带应用名问题
        Toast toast = Toast.makeText(MyEditText.this, null, Toast.LENGTH_SHORT);
        toast.setText(inputText);
        toast.show();
    }
}
```