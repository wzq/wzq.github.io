---
layout: post
title:  "kotlin+gradle开发android"
categories: [android]
tags: [2015-11]
---

该方案的优缺点如下 

优点: 

 * [Kotlin](https://kotlinlang.org/) jvm语言，性能进于java，支持函数式编程。
 * 对java的全面兼容
 * android studio全面支持，官方提供了专门针对android的教程
 * sdk体积很小，这对android很重要

缺点: 

* 非常年轻的语言当前还是beta版

***

必要工作：安装 ``kotlin`` 和 ``kotlin extensions for android ``两个插件

创建android项目，配置project build.gradle 
<pre><code>
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.0'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$KOTLIN_VERSION"
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
</code></pre> 

配置 module build.gradle (kandroid 不是必须依赖)
<pre><code>
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.1"

    defaultConfig {
        applicationId "com.wzq.kltest"
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

    sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.1.0'
    compile 'com.android.support:design:23.1.0'
    compile "org.jetbrains.kotlin:kotlin-stdlib:$KOTLIN_VERSION"
    compile 'com.pawegio.kandroid:kandroid:0.3.1@aar'
}
</code></pre>

编写代码 贴上部分代码 

<img src="/assets/image/kotlin_code.png" /> 

项目地址[KLTest](https://github.com/wzq/KLTest)