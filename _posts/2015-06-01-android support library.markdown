---
layout: post
title:  "android support library"
categories: [android]
tags: [2015-06]
---

Android Lollipop用google的话说到目前为止最伟大的android版本，很大程度上
是由于引进了Material Design新性设计语言。同时对开发者也是一个挑战，尤其在
向下的兼容性方面， 2015 IO刚刚结束除了android m的预发,android support库也添加了
名为design的新库.  
顾名思义,这个库主要为5.0以下版本提供_Material_设计风格的支持.下面具体描述：  

### 侧滑导航 ###  
<img style="margin-left: auto;margin-right: auto;width:200px;" src="/assets/image/drawer.png">  

提供了非常新的侧滑栏支持，使用起来十分方便，代码如下： 
{% highlight ruby %}
<android.support.v4.widget.DrawerLayout 
        xmlns:android = "http://schemas.android.com/apk/res/android" 
        xmlns:app = "http://schemas.android.com/apk/res-auto" 
        android:layout_width = "match_parent" 
        android:layout_height = "match_parent" 
        android:fitsSystemWindows = "true" > 

    <!--内容布局--> 

    <android.support.design.widget.NavigationView 
            android:layout_width = "wrap_content" 
            android:layout_height = "match_parent" 
            android:layout_gravity = "start" 
            app:headerLayout = "@layout/drawer_header" 
            app:menu = "@menu/drawer" /> 
</android.support.v4.widget.DrawerLayout>
{% endhighlight %}

### 编辑文本浮动标签 ###  
<img style="margin-left: auto;margin-right: auto;width:200px;" src="/assets/image/textinputlayout.png">  

float 方式的显示hint