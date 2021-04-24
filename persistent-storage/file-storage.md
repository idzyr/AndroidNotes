# file方式存储

>  以文件形式保存

在Android中

存储分为内部存储和外部存储.

- 内部存储 随应用卸载被删除
- 外部存储
  - 公有目录
  - 私有目录 随应用卸载而删除

## File内部存储

**内置路径**

**方法**

- `this.getFilesDir() /`/返file类型。 文件存储路径:

  - ```
    Android6.0前 /data/data/package/files
    ```

  - ```
    /data/user/0/package/files
    ```

    

- `this.getCacheDir()` //返回file类型 缓存路径:

  - ```
    Android6.0前/data/data/0/package/cache
    ```

  - ```
    /data/user/0/top.miku.datasave/cache
    ```

**外置SD卡路径**

方法

- `Environment.getExternalStorageDirectory()` 。

**注意；**

内部存储≠内存

> 以下数据文件默认会被存储到**内置路径** 的file文件夹下。也就是`this.getFilesDir()`方法返回的路径中。

```java
/*+++++++++++++++存储文件+++++++++++++++++++*/
   FileOutputStream fos = null;	//创建文件输出流对象
   try {
	   //通过openFileOutput获得输出流对象
	   //参数1 文件名，参数2 文件权限【这里设置为只有本app可以操作】
       fos = openFileOutput("data",MODE_PRIVATE);
	   //把字符串转换为字节数组写入到文件中【任何文件其实写入的都是字节】
       fos.write(editView.getText().toString().getBytes());
       fos.flush();		//把内容从缓冲区写入到存储设备中。
   } catch (IOException e) {
       e.printStackTrace();
   }finally {
       if (fos != null){
           try {
           fos.close();	//释放资源
       } catch (IOException e) {
           e.printStackTrace();
       }
       }
   }
   	
	/*——————————读取文件——————————————————————————————*/
	byte[] buffbytes;	//存储读取的字节内容
   FileInputStream fis = null;	//保存文件输入流对象
   try {
	   //通过openFileInput方法获取文件输入流对象
	   //参数 要读取的文件名
       fis = openFileInput("data");
	   //初始化字节数组，available()此方法获取文件中所有字节个数，不建议用来读取大文件使用
       buffbytes = new byte[fis.available()];	
		//读取文件 参数 读取的内容存储到那个字节数组中
       fis.read(buffbytes);
   }catch (IOException e) {
       e.printStackTrace();
   } finally {
       if (fis != null){
           try {
           fis.close();	//释放资源
           editView.setText(
               new String(buffbytes)//把字节数组转换为字符串
           );	//展示读取的内容

       } catch (IOException e) {
           e.printStackTrace();
       }
       }
   }

```





## SharedPreferences

> 以xml形式存储数据

安卓提供以XML文件格式永久保存数据的方法常用保存**偏好设置**。也就是保存对app的设置

路径 `data/data/<应用id名【默认AS生成是包名】>/.xml`

最好把 **SharedPreferences和SharedPreferences.Editor**声明为全局变量。

- `getSharedPreferences`()  获取SharedPreferences对象实例
  - 参数
    - 参数1 文件名 
    - 参数2 权限设置为只有本app可以操作，其它常量已经被废弃
- `sharedPreferences.edit()`  获取SharedPreferences.Editor 编辑对象。

**SharedPreferences.Editor方法；**

- `put[String]("keyName",value)` 保存string类型数据。其它类型替换[]中的类型即可
- `get[String]("keyName")` 获取对应key的值。其它类型替换[]中的类型即可
- `apply()` 异步保存推荐
- `commit()` 同步保存

```java
package top.miku.testsharedpreferences;

import androidx.appcompat.app.AppCompatActivity;

import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;

public class MainActivity extends AppCompatActivity {
    private SharedPreferences sharedPreferences;	//存放对象
    private SharedPreferences.Editor editor;
	
    @Override
    protected void onCreate(final Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

		//获得SharedPreferences对象，参数1文件名 参数2 权限设置为只有本app可以操作，其它常量已经被废弃
        sharedPreferences = getSharedPreferences("data",MODE_PRIVATE);
		//通过sharedPreferences获得edit就可以对文件操作了
        editor = sharedPreferences.edit();	
		//存储内容key和value 这里存储String类型
		//通过put+变量类型名大写，可以存储其它内容的值
		editor.putString("keyName",value);
		editor.apply();     //异步保存推荐
		//editor.commit();    //同步保存
	   
		//通过sharedPreferences对象的get+要获取值的变量类型大写即可得到对应值。
		//参数 要获取值的key，如果没有读取到值，默认值是。
		sharedPreferences.getString("content",null);

    }
}

```

