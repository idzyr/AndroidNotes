# File方式存储

| 分类                 | 其它应用是否可以访问                                         | 读写权限 | 卸载应用时是否移除文件 |
| -------------------- | :----------------------------------------------------------- | -------- | ---------------------- |
| 内部存储空间目录     | 否，在 Android 10（API 级别 29）及更高版本中，系统会对这些位置进行加密 | 否       | 是                     |
| 外部存储空间私有目录 | 有适当权限的情况下访问这些目录                               | 是       | 是                     |
| 外部存储空间公开目录 | 是                                                           | 是       | 否                     |



## 应用专属文件

### 内部目录

- `getFilesDir() ` file目录

  - ```
    Android6.0前 /data/data/package/files
    ```

  - ```
    /data/user/0/package/files
    ```

    

- `getCacheDir()`  缓存

  - ```
    Android6.0前/data/data/0/package/cache
    ```

  - ```
    /data/user/0/top.miku.datasave/cache
    ```

**查看文件列表**

```java
Array<String> files = context.fileList();
```

**移除缓存文件**

如需从内部存储空间内的缓存目录中移除文件，请使用以下方法之一：

- ```java
  cacheFile.delete();
  ```

- ```java
  context.deleteFile(cacheFileName);
  ```

### 外部目录

外部空间是指外置的SD卡存储，如今是将内部存储分区作为外部存储空间的，被视为主外部存储卷

**验证存储空间的可用性**

- `Environment.getExternalStorageState()` 
  - MEDIA_MOUNTED 可以读取和写入应用专属文件
  - MEDIA_MOUNTED_READ_ONLY 不可以只能读取这些文件

**选择物理存储位置**

有时，分配内部存储分区作为外部存储空间的设备**也会提供 SD 卡插槽**。这意味着设备具有多个可能包含外部存储空间的物理卷，因此您需要选择用于应用专属存储空间的物理卷。

如需访问其他位置，请调用 `ContextCompat.getExternalFilesDirs()`。如代码段中所示，返回数组中的第一个元素被视为主外部存储卷。除非该卷已满或不可用，否则请使用该卷。

```java
File[] externalStorageVolumes =
        ContextCompat.getExternalFilesDirs(getApplicationContext(), null);
File primaryExternalStorage = externalStorageVolumes[0];
```



- `getExternalFilesDir()`

  - ```
    /storage/emulated/0/Android/data/package/files
    ```

    

- `getExternalCacheDir(()`

- `Environment.getExternalStorageDirectory()`  外部存储主目录

### 媒体内容

如果您的应用支持使用仅在您的应用内对用户有价值的媒体文件，最好将这些文件存储在外部存储空间中的应用专属目录中.

```java
getExternalFilesDir(
            Environment.DIRECTORY_PICTURES), // 
```

[预定义子目录名称](https://developer.android.google.cn/reference/android/os/Environment#fields)， 您可以改为将 `null` 传递到 `getExternalFilesDir()`。这将返回外部存储空间中的应用专属根目录。

**注意；**

> 以下数据文件默认会被存储到**内置路径** 的file文件夹下。也就是`getFilesDir()`方法返回的路径中。

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

