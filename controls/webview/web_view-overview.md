# 概览

Android内置webkit内核的高性能浏览器,而WebView则是在这个基础上进行封装后的一个 控件,WebView直译网页视图,我们可以简单的看作一个可以嵌套到界面上的一个浏览器控件！

## WebView发展史

 在Android4.4（API level 19）系统以前，Android使用了原生自带的Android Webkit内核，这个内核对HTML5的支持不是很好，现在使用4.4以下机子的也不多了，就不对这个内核做过多介绍了，

从Android4.4系统开始，Chromium内核取代了Webkit内核，正式地接管了WebView的渲染工作。Chromium是一个开源的浏览器内核项目，基于Chromium开源项目修改实现的浏览器非常多，包括最著名的Chrome浏览器，以及一众国内浏览器（360浏览器、QQ浏览器等）。其中Chromium在Android上面的实现是Android System WebView。
 从Android5.0系统开始，WebView移植成了一个独立的apk，可以不依赖系统而独立存在和更新，我们可以在`系统->设置->Android System WebView`看到WebView的当前版本。
 从Android7.0系统开始，如果系统安装了Chrome (version>51)，那么Chrome将会直接为应用的WebView提供渲染，WebView版本会随着Chrome的更新而更新，用户也可以选择WebView的服务提供方（`在开发者选项->WebView Implementation`里），WebView可以脱离应用，在一个独立的沙盒进程中渲染页面（需要在开发者选项里打开）^2。
 从Android8.0系统开始，默认开启WebView多进程模式，即WebView运行在独立的沙盒进程中。

> 更多参考；https://cloud.tencent.com/developer/article/1388497

## 用到的辅助类

| 类名            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| WebChromeClient | 辅助WebView处理Javascript的对话框、网站图标、网站title、加载进度等！ |
| WebViewClient   | 辅助WebView处理各种通知与请求事件！                          |
| WebSettings     | WebView相关配置的设置，                                      |
| CookieManager   | cookie数据管理                                               |

### WebChromeClient

**事件；**

- `onJsAlert(WebView view,String url,String message,JsResult result)`	处理Js中的Alert对话框
- `onJsConfirm(WebView view,String url,String message,JsResult result)`	处理Js中的Confirm对话框
- `onJsPrompt(WebView view,String url,String message,String defaultValue,JsPromptResult result)`	处理Js中的Prompt对话框
- `onProgressChanged(WebView view,int newProgress)`	当加载进度条发生改变时调用
- `onReceivedIcon(WebView view, Bitmap icon)`	获得网页的icon
- `onReceivedTitle(WebView view, String title)`	获得网页的标题



### WebViewClient

**方法；**

- `doUpdateVisitedHistory(WebView view,String url,boolean isReload)`	更新历史记录
- `shouldOverrideKeyEvent(WebView view,KeyEvent event)`	控制webView是否处理按键时间,如果返回true,则WebView不处理,返回false则处理
- `shouldOverrideUrlLoading(WebView view,String url)`	控制对新加载的Url的处理,返回true,说明主程序处理WebView不做处理,返回false意味着WebView会对其进行处理

**事件；**

- `onPageStared(WebView view,String url)`	通知主程序网页开始加载
- `onPageFinished(WebView view,String url,Bitmap favicon)`	通知主程序,网页加载完毕
- `onLoadResource(WebView view,String url)`	通知主程序WebView即将加载指定url的资源
- `onScaleChanged(WebView view,float oldScale,float newScale)`	ViewView的缩放发生改变时调用
- `onReceivedError(WebView view,int errorCode,String description,String failingUrl)`	遇到不可恢复的错误信息时调用



### WebSettings

**方法；**

- `setJavaScriptEnabled()`设置是否允许JS脚本执行
- `setUseWideViewPort(true)` 设置 WebView 是应该启用对“viewport”HTML 元标记的支持还是应该使用宽视口。
- `setLoadWithOverviewMode(true)` 自适应屏幕
-  `setBuiltInZoomControls(true)`  设置 WebView 是否应使用其内置的缩放机制。
- `setDisplayZoomControls(false)` 设置 WebView 在使用内置缩放机制时，是否应显示屏幕缩放控件
- `setSupportZoom(true)` 设置 WebView 是否应支持使用其屏幕缩放控件和手势进行缩放。
- `setInitialScale(int s)` 自定义缩放比例 25%，最小缩放等级
- `setTextZoom(int)` 只缩放文本 Android自带五个可选字体大小的值：SMALLEST(50%),SMALLER(75%),NORMAL(100%),LARGER(150%), LARGEST(200%)。

### CookieManager

- `setAcceptCookie (boolean accept)` 设置应用程序的 WebView 实例是否应该发送和接受 cookie。

- `setCookie(String url, String value)` 为给定的 URL 设置单个 cookie（键值对）。
- `flush()` 确保当前可通过 getCookie API 访问的所有 cookie 都写入持久存储。是在API21以后CookieSyncManager类中sync()方法的替代。

## WebViewAPI

**属性；**



**方法；**

- `setHorizontalScrollBarEnabled()` 设置是否启用水平滚动条
- `setVerticalScrollBarEnabled()` 设置是否启用垂直滚动条
- `setScrollBarStyle();` 滚动条显示方式
  - View.SCROLLBARS_OUTSIDE_OVERLAY  滚动条在WebView内侧显示
  - View.SCROLLBARS_INSIDE_OVERLAY 滚动条在WebView外侧显示
- 

- `getSettings()`	返回一个WebSettings对象,用来控制WebView的属性设置
- `loadUrl(String url)`	加载指定的Url
- `loadData(String data,String mimeType,String encoding)`	加载指定的Data到WebView中.使用"data:"作为标记头,该方法不能加载网络数据.其中mimeType为数据类型如:textml,image/jpeg. encoding为字符的编码方式
- `loadDataWithBaseURL(String baseUrl, String data, String mimeType, String encoding, String historyUrl)` 	比上面的loadData更加强大
- `setWebViewClient(WebViewClient client)`	为WebView指定一个WebViewClient对象.WebViewClient可以辅助WebView处理各种通知,请求等事件。
- `setWebChromeClient(WebChromeClient client)`	为WebView指定一个WebChromeClient对象,WebChromeClient专门用来辅助WebView处理js的对话框,网站title,网站图标,加载进度条等

- `reload()` 重新加载页面
- `setScrollY(int value)` 设置滚动条Y轴值
- `boolean canGoBack()` 当前页面是否可以回退，可以回退则为true
- `goBack()` 让网页后退

**三个load方法的区别：**

- `loadUrl()`直接显示网页内容(单独显示网络图片)，一般不会出现乱码。
- `loadData(data, "text/html", "UTF-8")`用来加载URI格式的数据，不能通过网络来加载内容， 不能加载图片，而且经常会遇到乱码的问题，我们知道String类型的数据主要是Unicode编码的， 而WebView一般为了节省资源使用的是UTF-8编码，尽管我们按上面写了，但是还需要为webView设置： `webview.getSettings().setDefaultTextEncodingName("UTF -8");` 
- `loadDataWithBaseURL(baseUrl, string, "text/html", "utf-8", null)：`loadData类的一个 增强类，可以加载图片，baseUrl为你存储的图片路径，而且只需在这里设置utf-8就可以解决乱码 问题了！























