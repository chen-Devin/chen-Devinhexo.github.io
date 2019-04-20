---
layout: w
title: vue项目axios请求之qs用法详解
date: 2019-04-17 12:37:31
tags: vue
---
### axios请求报错作用


#### 在项目中。利用axios发送请求的时候，有时候会报一个错误：404 BadRequest

请求代码如下：

<!-- more -->  

![](https://img-blog.csdnimg.cn/2019041911590429.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)


请求结果如下： 

![](https://img-blog.csdnimg.cn/20190419115330720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

同一个项目中同样的发送请求方式，为啥这个接口会出错呢？

后来经过用postman 以及与后台对接及根据之前请求成功的接口数据进行对比，发现这个接口的传输数据中有数组存在。

经过各方面查验。找到了引入qs的解决办法，代码如下：

![](https://img-blog.csdnimg.cn/20190419120135218.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

请求成功了，但是，为什么要引入qs呢？？qs的作用是什么呢？

简单来说：qs是查询字符串解析和将对象序列化的库；而vue在请求的时候，当我们的data中有数组的时候，是需要序列化才能与后台进行通讯的。

qs的应用：

npm 下载qs库：npm i qs
在vue项目页面或者封装的axios中引用： import Qs from 'qs'；
qs主要有两种使用方法：qu.stringify()和qs.parse();
qu.stringify():将对象序列化成url的形式；以&进行拼接
qs.parse():将url解析成对象形式；

