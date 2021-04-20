# 概览

不同于Eclipse，Android Studio是采用Gradle来构建项目的。Gradle是一个非常先进的项目构建工具，它使用了一种基于Groovy的领域特定语言（DSL）来声明项目设置，摒弃了传统基于XML（如Ant和Maven）的各种烦琐配置。

## 项目中的build.gradle配置

所在位置，app目录外层build.gradle，配置后会作用到该项目下的**所有Module**，通常这个文件我们是不进行修改的。

**示例及解析；**

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.
//翻译：顶级构建文件，您可以在其中添加所有子项目/模块通用的配置选项。
buildscript {
    repositories { //远程仓库配置
        google()
        jcenter()//它是一个代码托管仓库，很多Android开源项目都会选择将代码托管到jcenter上，声明了这行配置之后，我们就可以在项目中轻松引用任何jcenter上的开源项目了。

    }
    //依赖关系
    dependencies {
        //声明了一个Gradle插件。为什么要声明这个插件呢？因为Gradle并不是专门为构建Android项目而开发的，Java、C++等很多种项目都可以使用，Gradle来构建。因此如果我们要想使用它来构建Android项目，则需要声明
        classpath 'com.android.tools.build:gradle:3.4.2'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        // 翻译：注意：请勿在此处放置应用程序依赖项它们属于单个模块build.gradle文件。

    }
}

allprojects {
    repositories {
        google()
        jcenter()

    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```



## 模块中的build.gradle

所在路径；Module下，通常表现形式就是 app目录下的build.gradle 

配置后**只会作用到当前的Module上**

**示例及解析；**

```groovy
apply plugin: 'com.android.application'//应用了一个插件，一般有两种值可选：com.android.application 表示这是一个应用程序模块，com.android.library 表示这是一个库模块。应用程序模块和库模块的最大区别在于，一个是可以直接运行的，一个只能作为代码库依附于别的应用程序模块来运行。

//在这个闭包中我们可以配置项目构建的各种属性
android {
    compileSdkVersion 29 //用于指定项目的编译版本(API 版本代号)
    buildToolsVersion "29.0.2"//用于指定项目构建工具的版本
    //defaultConfig闭包中可以对项目的更多细节进行配置
    defaultConfig {
        applicationId "top.miku.helloworld"//用于指定项目的包名
        minSdkVersion 19 //用于指定项目最低兼容的Android系统版本
        targetSdkVersion 29 //指定的运行的目标SDK 大于这个版本的新特性内容将无法使用
        versionCode 1 //用于指定项目的实际版本号
        versionName "1.0" //用于指定项目的版本名
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    //buildTypes闭包中用于指定生成安装文件的相关配置
    /*
    通常只会有两个子闭包，一个是debug，一个是release。debug闭包用于指定生成测试版安装文件的配置，release闭包用于指定生成正式版安装文件的配置。另外，debug闭包是可以忽略不写的。
    */
    buildTypes {
    //release闭包
        release {
            minifyEnabled false //用于指定是否对项目的代码进行混淆 true或false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'//用于指定混淆时使用的规则文件
            /*
                这里指定了两个文件，第一个proguard-android.txt 是在Android SDK目录下的，里面是所有项目通用的混淆规则，第二个proguard-rules.pro 是在当前项目的根目录下的，里面可以编写当前项目特有的混淆规则。

            */
        }
    }
}
//dependencies闭包
/*它可以指定当前项目所有的依赖关系。通常Android Studio项目一共有3种依赖方式：
    1.本地依赖、库依赖和远程依赖。本地依赖可以对本地的Jar包或目录添加依赖关系
    2.库依赖可以对项目中的库模块添加依赖关系
    3.远程依赖则可以对jcenter库上的开源项目添加依赖关系.
*/
dependencies {
    /*
        fileTree声明本地依赖关键词
        compile远程依赖声明关键词
        compile project库依赖声明关键词        
    */
    implementation fileTree(dir: 'libs', include: ['*.jar'])//声明本地依赖
    implementation 'androidx.appcompat:appcompat:1.0.2'//
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test:runner:1.2.0'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}
```







