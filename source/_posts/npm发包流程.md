---
title: npm发包流程
date: 2019-03-05 18:44:12
tags: npm
---
### npm发包
由于工作需要，发布一个npm包供我们使用

发布npm 包的过程实际上就是把你本地的node 项目上传，供自己或者别人使用的过程。

所以发布操作包含以下三个部分：本地创建node 项目编写代码、申请npm 账号、本地进行发布。

### 创建项目

vue init webpack project-name

此命令创建我们的项目的目录，创建文件夹和文件，目录结构如下：
 
<!-- more -->

![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/2452.png)

安装element-ui和axios 依赖

vue install element-ui axios –save


修改将要打包到npm的目录配置

Formdefined文件夹为自定义表单插件文件目录结构如下：

![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/245242452.png)
 
Index.js为组件入口加载文件

formDefined.vue为自定义表单页面插件

example为演示文件

Libs文件夹为自定义表单所引用的子组件库 （为原有表单自定义系统的演示组件）
 
![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/2758277827.png)



### 修改配置项
修改Package.json文件

因为需要上传到npm需要设置private为false

main是我们打包后的文件入口
 
![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/578%E6%A8%A1%E5%85%B7.png)

修改Webpack.base.conf.js文件
配置webpack的入口文件
 
![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/rtyjtyjzz.png)

修改webpack.prod.conf.js文件

导出文件以及css文件导出
 

![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/ryujmfy25.png)

修改.gitignore 文件

因为要用dist文件夹，所以在.gitignore文件中把dist/去掉。

引用原有css样式文件
 
![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/dtyjdtjy.png)


### Npm包发布

注册npm账号

Npm登录时将网址切换到npmjs网址

npm config set registry http://registry.npmjs.org/  否则登录的是淘宝镜像

Npm publish 


### 报错处理
 
![](https://raw.githubusercontent.com/chen-Devin/img-folder/master/rsthrhrsh.png)

报错：
npm ERR! code E405
npm ERR! Registry returned 405 for PUT on undefined


// 如果npm login或者npm adduser时报如下错误：npm ERR! 404 Registry returned 404 for PUT on undefined

// 则更换npm源

npm set registry https://registry.npmjs.org/

// 或者更新npm至最新版本

npm install -g npm
