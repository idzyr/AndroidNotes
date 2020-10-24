# 子线程更新UI)



## 常用六种方案

- 模拟耗时任务代码

  ```java
   /**
       * 模拟一个下载任务
       * @return
       */
      private String download(){
          try {
              //线程休眠1秒
              Thread.sleep(1000);
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
          return "当前下载进度";
      };
  ```

  



### ①Activity.runOnUiThread()

`runOnUiThread`是Activity中的方法，只有**当前对象是Activity**，就可以直接使用，如果当前的对象不是Activity，需要找到Activity对象，才能执行此方法

- `Activity.runOnUiThread(Runnable)` 更新UI方法

  参数；

  ​	Runnable 接口。

```java
 btnActvUIThread.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String data = download();   //获取子线程数据
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            edtiContent.setText(data);  //更新数据
                        }
                    });

            }
        });
```



### ②View.post()

post方法是View对象的方法，参数也是接收一个runnable接口

这里我选用的view对象是需要进行更新textview的本身，当然也可以选用其他的View对象，**只要是在当前Activity的对象都可以**

- `View.post(Runnable)` 

  - 参数

    Runnable 接口

```java
        btnViewPost.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String data = download();
                // 选择当前Activity的View对象都可以
                edtiContent.post(new Runnable() {
                    @Override
                    public void run() {
                        edtiContent.setText(data);  //更新数据
                    }
                });
            }
        });
```



### ③View.PostDelayed()

此方法和上面的post方法类似，只是多一个参数，用来实现延迟更新UI的效果

- `View.PostDelayed(Runnable,)` 延迟更新UI
  - 参数
    - Runnable 接口
    - delayMillis 延迟毫秒。

```java
 btnViewPostDelayed.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String data = download();
                edtiContent.postDelayed(new Runnable() {
                    @Override
                    public void run() {
                        edtiContent.setText(data);  //更新数据到ui
                    }
                }, 2000);
            }
        });
```



### ④Handler.post()

new一个Handler对象（全局变量）

```java
private Handler mHandler = new Handler()
```

- `Handler.post(Runnable) 
  - 参数
    - Runnable 接口。

```java
btnHandlerPost.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String data = download();
                mHandler.post(new Runnable() {
                    @Override
                    public void run() {
                        edtiContent.setText(data);
                    }
                });
            }
        });
```



### ⑤AsyncTask【推荐】

**介绍；**



### ⑥



