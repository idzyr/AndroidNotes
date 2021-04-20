# OKHttp

> **参考；**
>
> 《服务器后台》https://gitee.com/sunofbeaches/SOBAndroidMiniWeb

GitHub；https://github.com/square/okhttp

okhttp 是一个第三方网络请求框架其扮演者一个浏览器的角色。

> **注意；**
>
> 1. OkHttp的4.0.x版本已经全部由`java`替换到了`Kotlin`，API的一些使用也会有些不同，具体的参考[Upgrading to OkHttp 4](https://links.jianshu.com/go?to=https%3A%2F%2Fsquare.github.io%2Fokhttp%2Fupgrading_to_okhttp_4%2F)
> 2. okhttp依赖于okio
> 3. 无论是同步请求还是异步请求处理结果都要从子线程操作，要操作UI需要主进程去完成。

