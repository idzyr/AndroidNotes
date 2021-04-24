# XML

**xml范例；**

> 以下演示中使用此xml作为样本。

```xml
<apps>
    <app>
        <id>1</id>
        <name>Google Maps</name>
        <version>1.0</version>
    </app>
    <app>
        <id>2</id>
        <name>Chrome</name>
        <version>2.1</version>
    </app>

    <app>
        <id>3</id>
        <name>Google Play</name>
        <version>2.3</version>
    </app>
</apps>
```

## pull方式

### 解析器

解析xml的过程就是把xml序列化为对象。

XmlPullParser一个xml解析器接口此接口实现类有；

- `KXmlParser`（通过 XmlPullParserFactory.newPullParser()）

  ```java
  XmlPullParser xmlParser = XmlPullParserFactory.newInstance().newPullParser();
  ```

- `ExpatPullParser`（通过 Xml.newPullParser()）

#### XmlPullParser解析事件

| 事件           | 说明               | 备注 |
| -------------- | ------------------ | ---- |
| START_TAG      | 解析到元素开始     |      |
| END_TAG        | 解析到元素结束     |      |
| END_DOCUMENT   | 解析到整个文档结束 |      |
| START_DOCUMENT | 解析到文档开始     |      |

#### XmlPullParser类

**方法；**

- `setInput()` 设置解析器将要处理的输入流。
  - 参数
    - InputStream 要解析的流
    - String 输入流编码 如 utf-8
- `getEventType()` 获取当前事件类型(START_TAG, END_TAG, TEXT, etc.) int编号
  - 返回值
    - int 事件对应的int数。
- `getName()` 获取当前元素名称 String类型。
- `nextText()` 获取开始元素的下一个内容。及元素中间的内容。
- `next()` 获取下一个解析事件，int类型返回事件对应的整数。



### pull解析xml

**步骤一；**

根据xml数据建立对象类，用来序列化xml对象使用以此类作为xml对象的载体。如上面的xml文件中我们可以把app元素作为对象也就是一个类，把其中的id等元素作为此类的对象。

```java
package com.xuelingmiao.testapp.postxml;

public class App {
    private int id;
    private String name,version;

    public App() {

    }

    public App(int id, String name, String version) {
        this.id = id;
        this.name = name;
        this.version = version;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
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

一步一步解析xml

1. 创建存放app对象的list集合。
2. 创建app对象变量。
3. 创建解析器
4. 配置解析源
5. 获取解析事件类型
6. 通过循环开始解析文档
7. 根据解析到元素开始事件，来处理xml中的元素，组装对应对象。
8. 根据解析到元素结束事件，把组装后的元素收集到集合中。
9. 遍历解析后的元素解析结束。

```java
        btnPostXml.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // 1. 创建存放app对象的list集合。
                ArrayList<App> apps = null;
                // 2. 创建app对象变量。
                App app = null;

                try {
                    // 3. 创建解析器
                    //通过xml解析器工厂获取一个解析器实例
                    XmlPullParser xmlParser = XmlPullParserFactory.newInstance().newPullParser();
                    // 4. 配置解析源
                    /*
                     * 设置xml文件源
                     * setInput(InputStream inputStream, String inputEncoding)
                     * 参数；
                     *   InputStream文件输入流
                     *   String 输入流编码 如 utf-8
                     * */
                    xmlParser.setInput(PostXmlActivity.this.getAssets().open("xml/test.xml"), "utf-8");
                    Log.d(TAG, "onClick: " + getAssets().open("xml/test.xml"));
                    //获取当前解析事件类型START_TAG, END_TAG, TEXT, etc
                    //5. 获取解析事件类型
                    int eventType = xmlParser.getEventType();
                    // 6. 通过循环开始解析文档
                    //当前解析事件不是文件结束文件事件就继续读取
                    while (eventType != XmlPullParser.END_DOCUMENT) {
                        //更新解析事件类型，同样也是结束循环条件
                        //next()//获取下一个解析事件
                        eventType = xmlParser.next();
                        switch (eventType) {
                            // 7. 根据解析到元素开始事件，来处理xml中的元素，组装对应对象。
                            case XmlPullParser.START_TAG:
                                if (xmlParser.getName().equals("apps")) {
                                    //如果当前解析到的元素是apps那么就创建一个存储app对象的集合。
                                    apps = new ArrayList<App>();

                                } else if (xmlParser.getName().equals("app")) {
                                    //如果是app元素就创建一个app对象。
                                    app = new App();
                                } else if (xmlParser.getName().equals("id")) {
                                    //把id元素中的数据赋值给app对象的id属性。
                                    app.setId(xmlParser.nextText());

                                } else if (xmlParser.getName().equals("name")) {
                                    app.setName(xmlParser.nextText());

                                } else if (xmlParser.getName().equals("version")) {
                                    app.setVersion(xmlParser.nextText());
                                }
                                break;
                            // 8.  根据解析到元素结束事件，把组装后的元素收集到集合中。
                            case XmlPullParser.END_TAG:
                                if (xmlParser.getName().equals("app")) {
                                    // 把app元素添加到集合中。
                                    apps.add(app);
                                }
                                break;

                        }
                    }
                    StringBuilder data = new StringBuilder();

                    // 9. 遍历解析后的元素
                    for (App tempApp : apps
                    ) {
//                        data.append(tempApp.toString());
                        data.append(tempApp.toString());
                        Log.d(TAG, "onClick: " + tempApp.toString());

                    }

                    //更新数据到UI
                    editResult.post(new Runnable() {
                        @Override
                        public void run() {
                            editResult.setText(data);
                        }
                    });


                } catch (XmlPullParserException | IOException e) {
                    e.printStackTrace();
                }
            }
        });
```



### 序列化器

- `XmlSerializer` xml序列化器。

  ```java
   // 获取解析器工程
   XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
   // 获取序列化器
   XmlSerializer serializer = factory.newSerializer();
  ```

#### XmlSerializer类

**方法；**

- `setOutput()` 设置输出流
  - 参数
    - OutputStream 指定输出的流。
    - String 指定流编码如 `utf-8`
- `startDocument()`声明文档头信息及文档开始。
  - 参数
    - String xml文档编码如`utf-8`
    - Boolean 是否是独立的。不需要可以设置为null
- `text(String)` 写入文本特殊字符串会自动转义。
- `startTag()` 写入元素开始标记
  - 参数；
    - String namespace 名称空间无名称空间可以写null
    - String name 元素名称
- `endTag(namespace,name)` 写入元素结束标记
- `attribute(namespace,name,value)` 写入元素属性;
  - 参数
    - String namespace 名称空间无名称空间可以写null
    - String name 属性名称
    - Stirng value 属性值
- `endDocument()` 结束整个文档写入操作。

### pull生成XML

默认生成的xml是不包含换行符的。如果需要格式化输出使用`text("\n")`方法添加换行

1. 获取解析器工厂
2. 获取序列化器
3. 配置输出位置
4. 设置xml文档头信息，也就是文档头开始。
5. 设置xml文档根元素开始
6. 生成其它元素
7. 设置根元素结束。
8. 设置xml文档结束

```java
        btnGenerateXml.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                try {
                    //1. 获取解析器工程
                    XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
                    //2. 获取序列化器
                    XmlSerializer serializer = factory.newSerializer();
                    //存放生成xml
                    ByteArrayOutputStream xml = new ByteArrayOutputStream();
                    //3. 配置输出位置
                    serializer.setOutput(xml, "utf-8");
                    //4. 设置xml文档头信息也就是文档头开始。
                    serializer.startDocument("utf-8", null);
                    serializer.text("\n"); //设置标签中内容
                    //5. 设置xml文档根元素开始
                    serializer.startTag(null, "apps");
                    serializer.text("\n");
                    //6. 生成其它元素
                    for (int i = 0; i < 2; i++) {
                        serializer.startTag(null, "app");
                        serializer.text("\n");    //添加换行

                        serializer.startTag(null, "id");
                        serializer.text("1");
                        serializer.endTag(null, "id");
                        serializer.text("\r\n");

                        serializer.startTag(null, "name");
                        serializer.text("Google Maps");
                        serializer.endTag(null, "name");
                        serializer.text("\r\n");

                        serializer.startTag(null, "version");
                        serializer.text("1.0");
                        serializer.endTag(null, "version");
                        serializer.text("\r\n");

                        serializer.endTag(null, "app");
                        serializer.text("\r\n");

                    }
                    //7. 设置根元素结束。
                    serializer.endTag(null, "apps");
                    //8. 设置xml文档结束
                    serializer.endDocument();

                    String data = xml.toString("utf-8");
                    Log.d(TAG, "onClick: 生成xml"+data);
                    //更新到UI
                    editResult.post(new Runnable() {
                        @Override
                        public void run() {

                            editResult.setText(data);
                        }
                    });


                } catch (XmlPullParserException | IOException e) {
                    e.printStackTrace();
                }

            }
        });
```

**结果；**

```xml
<?xml version='1.0' encoding='utf-8' ?><apps><app><id>1</id><name>Google Maps</name><version>1.0</version></app><app><id>1</id><name>Google Maps</name><version>1.0</version></app></apps>
```







