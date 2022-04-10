# 动态注入JavaScript

## loadUrl方式

### javascript:直接代码

```java
webview.loadUrl("javascript: alert('hello');");
```

**缺点：**

会有最大字符限制，不同内核会有不同限制大小，目前发现TBS内核超过大概1024字节就注入不成功了，原生webview比较大，是2097152字节 (即：2M)，pc端情况如下：

| 游览器              | 最大长度（字符数） |                                   备注 |
| ------------------- | :----------------: | -------------------------------------: |
| Internet Explorer   |        2083        | 如果超过这个数字，提交按钮没有任何反应 |
| Firefox             |       65,536       |                                        |
| chrome              |        8182        |                                        |
| Safari              |       80,000       |                                        |
| Opera               |      190,000       |                                        |
| curl（linux下指令） |        8167        |                                        |

### javascript:加script标签块

通过js的script标签引入一个外部的脚本文件

````java
// 通过js代码创建script标签
String js = "var newscript = document.createElement(\"script\");"; 
// 设置script标签的src属性
js += "newscript.src=\"http://www.123.456/789.js\";";
// 追加到body标签内最后一个节点。
js += "document.body.appendChild(newscript);";
````

**问题一；**

如果你是使用本地js注入别人的网站，而非你自己放在sdcard的html页面的话是会有报错的：

`Not allowed to load local resource: file:///sdcard/inject.js`

解决方法参考：
[https://groups.google.com/forum/#!topic/android-developers/4g6H0vr5_0E](https://link.jianshu.com/?t=https://groups.google.com/forum/#!topic/android-developers/4g6H0vr5_0E)

**问题二；**

当你注入完JS之后你想要立即调用其中的方法，javascript:方式注入，没问题可以调用到。但是第二种方法中，你要确保注入的`<script>`便签对应的js文件加载完才可调用成功。

解决：在第二种方法中为加入`script`标签添加`onload`事件，确保该script已加载完成。代码可更改如下：

````java
String js = "var newscript = document.createElement(\"script\");";
   js += "newscript.src=\"http://www.123.456/789.js\";";
   js += "newscript.onload=function(){xxx();};";  //xxx()代表js中某方法
   js += "document.body.appendChild(newscript);";
````



## loadDataWithBaseURL

```java
String data = "<script>alert('hello');<script>";
webview.loadDataWithBaseURL( null, data, "text/html", "utf-8", null );
```



**缺点：**

这种方式看似完美，但还是有问题，每次调用loadDataWithBaseURL时都会触发`WebChromeClient#onProgressChanged()`方法，就是进度条是会变化的



## 总结

最稳妥的方法是将大的js **按功能模块拆分** 成小js，通过 `webview.loadUrl` 一个一个注入.





