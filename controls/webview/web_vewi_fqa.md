# 问题处理

## 无法通过后退退出页面

出现这种问题是网站重定向导致的

```java
  wView.setWebViewClient(new WebViewClient() {
            //在webview里打开新链接
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                return false;
            }
        });
```



- `public boolean shouldOverrideUrlLoading(WebView view, String url)` 当即将在当前 WebView 中加载 URL 时，让宿主应用程序有机会进行控制拦截。
  - 参数；
    - view：发起回调的 WebView。
    - url 要加载的 URL。‘
  - 返回；
    - boolean True（拦截WebView加载Url），False（允许WebView加载Url）

> [!WARNING]
>
> 此方法在 API 级别 24 中已弃用。 改用 [shouldOverrideUrlLoading(WebView, WebResourceRequest)。](https://developer.android.google.cn/reference/android/webkit/WebViewClient#shouldOverrideUrlLoading(android.webkit.WebView,%20android.webkit.WebResourceRequest))



## JavaScriptAlert没有弹出

需要为webVIew设置setWebChromeClient对象

```java
  mWebView.setWebChromeClient(new WebChromeClient());
```







