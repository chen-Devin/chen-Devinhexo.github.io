---
title: vue项目详情(1)-项目搭建
date: 2019-04-23 18:29:58
tags: vue
---
### vue项目搭建的基本环境

1：安装node.js
首先电脑需要安装node.js，安装node.js会自带npm;查看node和npm的安装版本，

如果安装了可输入：node -v   和  npm -v;可以查看当前安装版本的版本号；

<!-- more -->  

![](https://img-blog.csdnimg.cn/2019042219162525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

弹出版本号，则说明已安装， 

2:下载淘宝镜像 cnpm；

上面我们下载的是npm包管理工具；但是由于npm服务器是在国外的，而在国内下载有时速度会很慢很慢，所以阿里巴巴免费在国内搭建了一个cnpm库。同步频率目前为 10分钟 一次，以保证尽量与官方服务同步

输入： npm install -g cnpm --registry=https://registry.npm.taobao.org

如果安装了可输入：cnpm -v 可查看当前版本号

![](https://img-blog.csdnimg.cn/2019042219322191.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)


3：安装webpack

因为要搭建的事vue+webpack项目，所以需要先下载webpack;

输入：npm install webpack -g

如果安装了可输入webpack -v 查看版本号

![](https://img-blog.csdnimg.cn/20190422193637689.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)


4：安装vue-cli脚手架搭建工具： 

输入：npm install vue-cli -g

如果安装了可输入：vue -V  查看当前版本号 

![](https://img-blog.csdnimg.cn/20190422194602120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

至此，确保上面的依赖已经安装完成了； 接下来需要找到一个文件夹。来搭建vue项目了；

### vue-cle脚手架构建项目；

1：打开我们需要创建项目的文件夹，打开git管理工具。


![](https://img-blog.csdnimg.cn/20190422195103619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)
 

2： 用vue-cli搭建项目

输入：vue init webpack ‘项目名称’

注意：项目名称根据我们的项目来定义，但不能用中文和大写字母

![](https://img-blog.csdnimg.cn/20190422195848603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

也可以自己在这里输入项目名称，但是个人不太习惯；

 输入：vue init webpack vue-basic-building

![](https://img-blog.csdnimg.cn/20190422202025441.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

 中间会让我们输入名称或者提示，以及一些依赖的选择，可以直接回车选择默认选项，然后选择（Y/N）的可以根据自己需求选择，建议除了eslint检测可以选择no其他的都选择yes；

至此，项目已经搭建完成；

cd进入工程目录：cd  '项目名称'

下载项目依赖(个人习惯cnpm)： cnpm install  

运行项目：npm run dev

![](https://img-blog.csdnimg.cn/20190422202649432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

然后浏览器打开运行的网址， 

![](https://img-blog.csdnimg.cn/20190422202801451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

如图所示：一个基本的vue项目已经搭建完成基本目录结构如下：

![](https://img-blog.csdnimg.cn/20190422202858138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlfX2Fu,size_16,color_FFFFFF,t_70)

一个基本的项目已经搭建完成。那么项目结构是怎么样的？我们应该对项目进行哪些初始化。 关于axios封装，反向代理，vuex存储传值，路由跳转，路由守卫等怎么实现，后续更新