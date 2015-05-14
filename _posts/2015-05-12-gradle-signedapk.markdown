---
layout: post
title:  "使用gradle批量打包"
date:   2015-05-12
categories: jekyll update
---

去年开始使用 _Android Studio_ 开发，到现在已经用的得心应手了，效率提高很多， 黑色的主题也很酷。  
几天纪录下如何使用gradle 批量打包以及 某些常量的动态配置。  
首先需要理解[gradle][0]基础, 一种新的项目结构，类似maven， 但更好用  

打包的所有配置都在module下的 _build.gradle_ 文件中。[文件结构][1]  
首先在配置你的签名（一下都在 _android_ 目录中配置）：  
{% highlight ruby %}
signingConfigs {
    release {
        keyAlias 'xxxx'
        keyPassword 'xxxx'
        storeFile file('xxxxx')
        storePassword 'xxxx'
    }
}
{% endhighlight %}  
你可以配置多个签名如：一个release 一个debug  
接下来配置buildType:  
{% highlight ruby %}
 	buildTypes {
        debug {
            buildConfigField "String", "HOST", '"xxxx"'
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            signingConfig signingConfigs.release
        }
        release {
            buildConfigField "String", "HOST", '"xxxx"'
            minifyEnabled true
            shrinkResources true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-project.txt'
            signingConfig signingConfigs.release
        }
    }
{% endhighlight %}  
buildType 配置了你的apk输出类型，可以配置多个，每个类型中可做详细定义：  

- buildConfigField 定义一个名为host的字符串，用于区分debug和release不同的服务器地址
- minifyEnabled 是否进行混淆 默认false
- shrinkResources 是否去除无用的res文件 
- proguardFiles 制定混淆规则文件 [具体规则][2]
- signingConfig 制定签名 就是上面配置过的  

如果希望配置更多的类型可以使用productFlavors 如友盟多渠道配置  
{% highlight ruby %}
	productFlavors {
        mi {
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "mi"]
        }
        '360' {
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "360"]
        }
        baidu {
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "baidu"]
        }
        wandoujia {
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "wandoujia"]
        }
        qq{
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "qq"]
        }
        '1' {
            manifestPlaceholders = [UMENG_CHANNEL_VALUE: "1"]
        }
    }
{% endhighlight %}  
注：闭包数字需要加''  
这样每个buildType 类型对应了n个productFlavors类型，打包数量为：buildType * productFlavors个，别忘了修改manifest里友盟配置  
{% highlight ruby %}
  <meta-data
            android:name="UMENG_CHANNEL"
            android:value="${UMENG_CHANNEL_VALUE}"></meta-data>
{% endhighlight %}  

最后加上
{% highlight ruby %}
	//禁止lint错误
	lintOptions {
        abortOnError false
    }
{% endhighlight %}  

> 补充：buildConfigField可自由定义：buildConfigField 类型, 名称, 赋值  
> 调用方式：BuildConfig.名称 即可

[0]: http://gradle.org/
[1]: http://ask.android-studio.org/?/article/40
[2]: http://blog.csdn.net/fengyuzhengfan/article/details/43876197