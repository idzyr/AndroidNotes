# 语法

> **参考；**
>
> 《Gradle 入门--只此一篇》https://www.jianshu.com/p/001abe1d8e95

Gradle是一种声明式的构建工具。Gradle向我们提供了一整套DSL，所以在很多时候我们写的代码似乎已经脱离了groovy，但是在底层依然是执行的groovy所以很多语法还是Groovy的语法规则。



## 阶段闭包

### buildscript 

用于指定构建阶段要执行的任务





## 部分闭包

### 构建阶段

#### repositories 【存储库】

用于声明远程托管仓库，声明了这行配置之后，我们就可以在项目中轻松引用任何远程仓库上的开源项目了。

- `jcenter()`它是一个代码托管仓库，很多Android开源项目都会选择将代码托管到jcenter上，

**示例；**

```groovy
 repositories { 
     /*--------------简写------------------------*/
        google() //谷歌官方仓库
        jcenter()
     /*--------------url方式------------------------*/
		maven { url 'http://maven.aliyun.com/nexus/content/repositories/google' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
     // maven {url '远程仓库地址'}

    }

```



#### dependencies 【依赖关系】

**示例；**

```groovy
dependencies {
        //声明了一个Gradle插件。为什么要声明这个插件呢？因为Gradle并不是专门为构建Android项目而开发的，Java、C++等很多种项目都可以使用，Gradle来构建。因此如果我们要想使用它来构建Android项目，则需要声明
        classpath 'com.android.tools.build:gradle:3.4.2'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        // 翻译：注意：请勿在此处放置应用程序依赖项它们属于单个模块build.gradle文件。

    }
```



### android 

| 名称              | 类型   | 作用                                 |
| ----------------- | ------ | ------------------------------------ |
| compileSdkVersion | int    | 用于指定项目的编译版本(API 版本代号) |
| buildToolsVersion | string | 用于指定项目构建工具的版本           |
|                   |        |                                      |

### defaultConfig闭包

用于默认配置

| 名称             | 类型   | 作用                                                   |
| ---------------- | ------ | ------------------------------------------------------ |
| applicationId    | String | 用于指定app的包名                                      |
| minSdkVersion    | int    | 用于指定app最低兼容的Android系统版本                   |
| targetSdkVersion | int    | 指定的运行的目标SDK 大于这个版本的新特性内容将无法使用 |
| versionCode      | int    | 用于指定app的实际版本号                                |
| versionName      | String | 用于指定app的版本名                                    |
|                  |        |                                                        |
|                  |        |                                                        |

### buildTypes 闭包

用于指定app构建相关配置

通常只会有两个子闭包，一个是debug，一个是release。

- debug闭包用于指定生成测试版安装文件的配置，
- release闭包用于指定生成正式版安装文件的配置。另外，debug闭包是可以忽略不写的。

#### release 闭包

| 名称          | 类型    | 作用                             |
| ------------- | ------- | -------------------------------- |
| minifyEnabled | Boolean | 用于指定是否对项目的代码进行混淆 |
| proguardFiles |         | 用于指定混淆时使用的规则文件     |
|               |         |                                  |

### dependencies 闭包

用来声明第三方lib依赖关系

通常Android Studio项目一共有3种依赖方式：

1. 本地依赖、库依赖和远程依赖。本地依赖可以对本地的Jar包或目录添加依赖关系
2. 库依赖可以对项目中的库模块添加依赖关系
3. 远程依赖则可以对jcenter库上的开源项目添加依赖关系.



## 其它声明







