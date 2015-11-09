---
layout: post
title:  "scala+gradle开发android"
categories: [android]
tags: [2015-11]
---

该方案的优缺点如下 

优点: 

 * [Scala](http://www.scala-lang.org/) 成熟强大稳定的jvm语言，性能进于java，支持函数式编程。
 * 对java的全面兼容。 
 * 有[macroid](http://macroid.github.io/ScalaOnAndroid.html), [scaloid](https://github.com/pocorall/scaloid)等丰富的开源项目

缺点: 

* Scala庞大的库会导致你的apk体积变大，同时增加了学习成本
* Scala提倡使用sbt构件项目而android提倡使用gradle构件

***

必要工作: 

* 下载scala－sdk,我这边是2.11.7
* 安装studio上scala, android scala两个插件 

建立一个android项目, 配置preject build.gradle  
<pre><code>
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.2.3'
        classpath "jp.leafytree.gradle:gradle-android-scala-plugin:1.4"
    }
}

allprojects {
    repositories {
        jcenter()
    }
}
</code></pre>

配置module的build.gradle
<pre><code>
apply plugin: 'com.android.application'
apply plugin: "jp.leafytree.android-scala"

android {
    compileSdkVersion 22
    buildToolsVersion "22.0.1"

    defaultConfig {
        applicationId "com.wzq.scalatest"
        minSdkVersion 14
        targetSdkVersion 22
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile "org.scala-lang:scala-library:2.11.7"
    compile 'com.android.support:appcompat-v7:22.2.1'
    compile 'com.wzq.easyblur:library:1.0.0'
}
</code></pre>

编写你的程序，这里贴上部分代码 

<img src="/assets/image/scala_code.png" /> 

项目地址[ScalaTest](https://github.com/wzq/ScalaTest)