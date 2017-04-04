
---
title: Android导入jar和so文件（高德地图配置心得）
date: 2016-10-22
---

> 最近在项目需要使用地图，学习了一下高德sdk的使用，在配置的过程中遇到了一些问题，记录下来。

#### 遇到的问题
高德地图sdk配置的时候需要导入so文件，由于导入的时候一直没有导入成功，所以一直报***No implementation found for long com.autonavi.amap.mapcore.MapCore***错误，后面google一下，成功解决了这个问题

项目中所使用到的高德地图sdk主要分为两个 **定位sdk**　和 **地图sdk** ，**定位sdk**的配置比较简单，直接将jar导入即可。下面简单说下导入jar的步骤吧

#### 导入jar包的步骤
1.  将需要导入的jar直接拷贝到app目录下的libs目录中。
2.  然后再app 的build.gradle中添加依赖即可
```
dependencies {
        compile 'com.android.support:support-v4:19.1.0'
        compile files('libs/libammsdk.jar')
        compile files('libs/universal-image-loader-1.8.6-with-sources.jar')
       compile files('libs/YoumiSdk_v5.00_2015-01-08.jar')
    } 
```
<!-- more -->

或者是打开project structure，添加依赖
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/l2P51)

配置完后重新build一下就行了


#### 导入so文件的步骤
1.  将so文件拷贝到app的libs目录中
2.  然后再app build.gradle中的android标签下添加sourceSets设置
完整的builde.gradle示例如下：

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.3"

    defaultConfig {
        applicationId "cn.smile.demo"
        minSdkVersion 14
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    //重要的是设置下源目录
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs']//将so文件目录指向libs目录
        }
    }    
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
}
```

现在重新build一下，so文件就成功的导入到了项目中来。



