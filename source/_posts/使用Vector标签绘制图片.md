title: 使用Vector标签绘制图片
date: 2015-12-09 19:39:59
categories: 技术文章
tags:
- android 
- vector
---

下面介绍一下 Android 5.0 官方推出了一个全新的标签 `vector`  --> [官网地址](http://developer.android.com/intl/zh-cn/training/material/drawables.html)

## 创建矢量图片
在 Android 5.0（API 级别 21）及更高版本中，您可定义矢量图片，而且图片可在不丢失定义的情况下缩放。您只需一个资产文件即可创建一个矢量图像，而位图图像则需要为每个屏幕密度提供一个资产文件。如果要创建一个矢量图像，请您在 <vector> XML 元素中定义形状的详情。

下列示例以心形定义一个矢量图像：

```xml
<!-- res/drawable/heart.xml -->
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    <!-- intrinsic size of the drawable -->
    android:height="256dp"
    android:width="256dp"
    <!-- size of the virtual canvas -->
    android:viewportWidth="32"
    android:viewportHeight="32">

  <!-- draw a path -->
  <path android:fillColor="#8fff"
      android:pathData="M20.5,9.5
                        c-1.955,0,-3.83,1.268,-4.5,3
                        c-0.67,-1.732,-2.547,-3,-4.5,-3
                        C8.957,9.5,7,11.432,7,14
                        c0,3.53,3.793,6.257,9,11.5
                        c5.207,-5.242,9,-7.97,9,-11.5
                        C25,11.432,23.043,9.5,20.5,9.5z" />
</vector>
```

矢量图像在 Android 中以 VectorDrawable 对象表示。如果要了解更多有关 pathData 语法的信息，[请参阅 SVG 路径参考文档](http://www.w3.org/TR/SVG11/paths.html#PathData)。如果要了解更多有关为矢量图片属性添加动画的信息，[请参阅为矢量图片添加动画](http://developer.android.com/intl/zh-cn/training/material/animations.html#AnimVector)

<!--more-->

## 源码：
drawable：plaid_no_connection.xml
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
        android:width="56dp"
        android:height="213dp"
        android:viewportWidth="56"
        android:viewportHeight="213">

    <path
        android:name="cloud"
        android:pathData="M45.15,14.0933333 C43.5633333,6.04333333 36.4933333,0 28,0 C21.2566667,0 15.4,3.82666667 12.4833333,9.42666667 C5.46,10.1733333 0,16.1233333 0,23.3333333 C0,31.0566667 6.27666667,37.3333333 14,37.3333333 L44.3333333,37.3333333 C50.7733333,37.3333333 56,32.1066667 56,25.6666667 C56,19.5066667 51.2166667,14.5133333 45.15,14.0933333 L45.15,14.0933333 Z"
        android:fillColor="#888888"/>

    <group
        android:name="connection">

        <clip-path
            android:name="connection_mask"
            android:pathData="@string/connection_line_mask_hidden" />

        <path
            android:strokeColor="#888888"
            android:pathData="M28,67 L28,75"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,79 L28,87"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,91 L28,99"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,103 L28,111"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,115 L28,123"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,127 L28,135"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,139 L28,147"
            android:strokeWidth="4"/>

        <path
            android:strokeColor="#888888"
            android:pathData="M28,151 L28,159"
            android:strokeWidth="4"/>

    </group>

    <group
        android:name="cross_group"
        android:pivotX="28"
        android:pivotY="58.65"
        android:scaleX="0"
        android:scaleY="0">

        <path
            android:name="cross"
            android:pathData="M27.6568542,58.6568542 L22,53 L27.6568542,58.6568542 L33.3137085,53 L27.6568542,58.6568542 Z M27.6568542,58.6568542 L33.3137085,64.3137085 L27.6568542,58.6568542 L22,64.3137085 L27.6568542,58.6568542 Z"
            android:strokeWidth="4"
            android:strokeColor="#888888"/>

    </group>

    <!--<path
        android:name="phone"
        android:pathData="M37.6666667,161 L19,161 C15.1266667,161 12,164.126667 12,168 L12,205.333333 C12,209.206667 15.1266667,212.333333 19,212.333333 L37.6666667,212.333333 C41.54,212.333333 44.6666667,209.206667 44.6666667,205.333333 L44.6666667,168 C44.6666667,164.126667 41.54,161 37.6666667,161 L37.6666667,161 Z M33,207.666667 L23.6666667,207.666667 L23.6666667,205.333333 L33,205.333333 L33,207.666667 L33,207.666667 Z M40.5833333,200.666667 L16.0833333,200.666667 L16.0833333,168 L40.5833333,168 L40.5833333,200.666667 L40.5833333,200.666667 Z"
        android:fillColor="#888888"/>-->

    <path
        android:name="phone"
        android:pathData="M37.6666667,161 L19,161 C15.1266667,161 12,164.126667 12,168 L12,205.333333 C12,209.206667 15.1266667,212.333333 19,212.333333 L37.6666667,212.333333 C41.54,212.333333 44.6666667,209.206667 44.6666667,205.333333 L44.6666667,168 C44.6666667,164.126667 41.54,161 37.6666667,161 L37.6666667,161 Z M40.5833333,200.666667 L16.0833333,200.666667 L16.0833333,168 L40.5833333,168 L40.5833333,200.666667 L40.5833333,200.666667 Z"
        android:fillColor="#888888"/>

    <path
        android:name="button"
        android:pathData="@string/phone_button"
        android:strokeWidth="4"
        android:strokeLineCap="round"
        android:strokeColor="@color/background_dark"/>

</vector>
```

avd_plaid_no_connection.xml
```xml
<animated-vector
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/plaid_no_connection">

    <target
        android:name="connection_mask"
        android:animation="@animator/plaid_nonet_show_connection_line" />

    <target
        android:name="cross_group"
        android:animation="@animator/plaid_nonet_show_connection_cross" />

    <target
        android:name="button"
        android:animation="@animator/plaid_nonet_button_frown" />

</animated-vector>
```

## 动画
animator：plaid_nonet_button_frown.xml
```xml
<objectAnimator
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:propertyName="pathData"
    android:valueFrom="@string/phone_button"
    android:valueTo="@string/phone_button_frown"
    android:startOffset="1700"
    android:duration="300"
    android:interpolator="@android:interpolator/fast_out_slow_in"
    android:valueType="pathType" />
```
animator：plaid_nonet_show_connection_cross.xml
```xml
set xmlns:android="http://schemas.android.com/apk/res/android"
     android:ordering="together">

    <objectAnimator
        android:propertyName="scaleX"
        android:valueFrom="0"
        android:valueTo="1"
        android:startOffset="500"
        android:duration="@android:integer/config_shortAnimTime"
        android:interpolator="@android:interpolator/linear_out_slow_in" />

    <objectAnimator
        android:propertyName="scaleY"
        android:valueFrom="0"
        android:valueTo="1"
        android:startOffset="500"
        android:duration="@android:integer/config_shortAnimTime"
        android:interpolator="@android:interpolator/linear_out_slow_in" />

</set>
```
animator：plaid_nonet_show_connection_line.xml
```xml
<objectAnimator
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:propertyName="pathData"
    android:valueFrom="@string/connection_line_mask_hidden"
    android:valueTo="@string/connection_line_mask_shown"
    android:valueType="pathType"
    android:startOffset="1000"
    android:duration="1000"
    android:interpolator="@android:interpolator/linear" />
```