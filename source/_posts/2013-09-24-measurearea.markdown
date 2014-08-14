---
layout: post
title: "测量面积的工具"
date: 2013-09-24 08:41
comments: true
categories: [android, java]
---
一个还没正式开始就被技术上劝下来的项目，曾经花了我很多时间来设想，下载了好几个相关传感器的Demo。

之前的基本构思是，通过加速度计(重力感应使用的传感器)，获取瞬时加速度，通过不断的积分而获得当前速度，然后计算距离，然后绘制行动路径的多边形，然后计算面积。

致命缺点：由于速度经过积分而产生，定位误差随时间而增大，长期精度差；手机上面的加速度计本来精度就低，测量加速度的时候还要受重力加速度影响，通过一次卡尔曼(Kalman Filter)过滤，数据已经完全不能用来再计算速度了，已经废了，我还以为我们要怎么忙怎么忙，怎么辛苦做这个东西呢，结果根本就不能做。。

反正，不是因为这个不可能，而是因为设备精度太低，惯性导航仅被用在飞机等高造价的设备上。

下面是一些相关资料

-  [Android Developers - Motion Sensors](https://developer.android.com/intl/zh-cn/guide/topics/sensors/sensors_motion.html)
-  [StackOverflow - using-accelerometer-to-calculate-speeds](http://stackoverflow.com/questions/10921395/using-accelerometer-to-calculate-speeds)
-  [reddit - sensor_fusion_algorithm_for_inertial_navigation](http://ds.reddit.com/r/Android/comments/1ibwmg/sensor_fusion_algorithm_for_inertial_navigation/)
-  [Wikipedia 卡夫曼滤波](http://zh.wikipedia.org/wiki/卡尔曼滤波)
