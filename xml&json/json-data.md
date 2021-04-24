# JSON

**json范例**

> 以下演示中使用此json作为样本。

```json
[
  {
    "id": "5",
    "version": "5.5",
    "name": "Clash of Clans"
  },
  {
    "id": "6",
    "version": "7.0",
    "name": "Boom Beach"
  },
  {
    "id": "7",
    "version": "3.5",
    "name": "Clash Royale"
  }
]
```



## GSON

GitHub；https://github.com/google/gson

GSON是Google提供的一个操作json 的开源库。默认不在api中需要手动集成。

```groovy
dependencies {
  implementation 'com.google.code.gson:gson:2.8.6'
}
```

### 解析JSON

json字符串反序列化到Java对象的过程。

**步骤一；**

创建一个json字符串中对象的实体类。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private String id,name,version;

    public App() {

    }

    public App(String id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "App{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", version='" + version + '\'' +
                '}';
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}
```

**步骤二；**

解析json字符串，并映射到实体类。

1. 装备JSON字符串
2. 实例化gson对象
3. 解析json字符映射到实体对象
4. 解析完成

```java
btnPullJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                try {
                    // 1. 装备JSON字符串。
                    InputStream  jsonFile = PostJsonActivity.this.getAssets().open("json/test.json");
                    ByteArrayOutputStream os = new ByteArrayOutputStream();
                    int len = 0; //标记读取有效字节数。
                    byte[] byteArr = new byte[1024];
                    //循环读取流
                    while ((len=jsonFile.read(byteArr)) != -1 ){
                        os.write(byteArr,0,len); //写入到输出流
                    }
                    String jsonStr = os.toString("utf-8");  //将流转换为字符串。
                    Log.d(TAG, "onClick: JsonStr"+jsonStr);
                    // 2. 实例化gson对象
                    Gson gson = new Gson();
                    // 3. 解析json字符映射到实体对象。
                    List<App> appList = gson.fromJson(jsonStr, new TypeToken<List<App>>()
                    {}.getType());

                    // 4. 解析完成
                    Log.d(TAG, "onClick: "+appList.toString());

                    //更新到UI
                    editJson.post(new Runnable() {
                        @Override
                        public void run() {
                             editJson.setText(appList.toString());
                             //输出单个数据
                            Log.d(TAG, "run: "+appList.get(0).getName());
                        }
                    });


                } catch (IOException e) {
                    e.printStackTrace();
                }


            }
        });


        //生成json
        btnGenerateJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

            }
        });
```

### 生成JSON

类序列化为json字符串的过程。默认生成JSON是为格式化的

**步骤一；**

准备要序列化为json字符串的实体类。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private String id,name,version;

    public App() {

    }

    public App(String id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "App{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", version='" + version + '\'' +
                '}';
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}
```

**步骤二；**

类序列化为json字符串。

1. 准备要生成json的类的数据
2. 实例化为gson
3. 类序列化为json字符串

```java
        btnGenerateJson.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //1. 准备要生成json的类的数据。
                List<App> appList = new ArrayList<>();
                for (int i = 0; i < 2; i++) {
                    App app = new App();
                    app.setId("1");
                    app.setName("My App");
                    app.setVersion("1.0.0");
                    appList.add(app);
                }

                //2. 实例化为gson
                Gson gson = new Gson();
                //3. 类序列化为json字符串。
                String jsonStr = gson.toJson(appList, new TypeToken<List<App>>() {
                }.getType());


                Log.d(TAG, "onClick: 生成json" + jsonStr);
                //更新到UI
                editJson.post(new Runnable() {
                    @Override
                    public void run() {
                        editJson.setText(jsonStr);
                    }
                });

            }
        });
```

