+ `apply plugin: 'com.android.application'` -- 表示这是一个应用程序模块。
+ `apply plugin: 'com.android.library` -- 表示这是一个库模块。

```gradle
android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "android.coolweather_test.com.coolweatherdemo"  # 用于指定项目的包名
        minSdkVersion 15 #用于指定项目最低兼容的android系统版本,“15”表示最低兼容到android4.0系统。
        targetSdkVersion 25  
        versionCode 1  # 用于指定项目的版本号
        versionName "1.0" # 用于指定项目的版本名
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false # 表示是否要进行代码混淆
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
} 
```
+ Android Studio 项目一共有3种依赖方式：本地依赖、库依赖和远程依赖。