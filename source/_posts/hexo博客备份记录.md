---
title: hexo博客备份记录
date: 2019-01-11 18:40:28
tags: 学习
---

### 备份
针对博客已经搭建并发布过文章的。

1. 在你的博客仓库创建一个分支Hexo（这个命名随意）；

2. 设置Hexo为默认分支（不知道怎么设的可以百度）；

3. 将博客仓库clone至本地，将之前的Hexo文件夹中的_config.yml，themes/，source，scffolds/，package.json，.gitignore复制到你克隆下来的仓库文件夹，即Username.github.io；（Username是你自己的用户名）

<!-- more -->

4. 将themes/next/(我用的是NexT主题)中的.git/删除，否则无法将主题文件夹push；

5. 在Username.github.io；文件夹执行npm install，npm install hexo-deployer-git(这里可以看看分支是不是显示为Hexo)

6. 执行git add，git commit -m "提交文件"，git push origin Hexo来提交Hexo网站源文件；

7. 执行hexo g -d 生成静态网页部署到github上。

这样，Username.github.io仓库就有master分支保存静态网页，hexo分支保存源文件。


### 修改
在本地对博客修改（包括修改主题样式、发布新文章等）后

1. 执行git add，git commit -m "提交文件"，git push origin Hexo来提交Hexo网站源文件；

2. 执行hexo g -d 生成静态网页部署到github上；

（每次发布重复这两步，它们之间没有严格的顺序）

### 恢复

新建文件夹下载博客：
1. 安装git；

2. 安装Nodejs和npm；

3. 使用克隆命令将仓库拷贝至本地；

4. 在文件夹内执行命令npm install hexo-cli -g、npm install、npm install hexo-deployer-git；