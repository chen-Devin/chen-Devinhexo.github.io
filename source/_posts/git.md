---
title: git
date: 2018-03-15 21:16:16
tags: 版本管理工具
---

## 版本管理工具
版本管理工具分为集中式和分布式：

* 集中式版本控制系统：版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。 集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊
* 

<!-- more -->
* 分布式版本控制系统：没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。
* 分布式和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。
* 在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已
* Git的优势不单是不必联网这么简单，后面我们还会看到Git极其强大的分支管理，把SVN等远远抛在了后面。


## git指令
	git init 创建git库
	touch xxx.html 创建文件
	mkdir xxx 创建文件夹
	pwd 显示当前目录
	git add xxx.html 添加到暂存区
	git commit -m '提交的备注'  提交到当前分支
	git diff xxx.html 查看当前文件的具体修改
	git status  查看当前提交状态
	git log 查看历史记录	
	git log --pretty=oneline 查看历史记录(只有版本号和备注)
	git reset --hard HEAD^ 回退到之前的版本，HEAD表示当前版本，HEAD^就表示上一版本，^多了也可写成HEAD~100表示回退前一百个版本
	git reflog 记录你的每次命令 ，同时也记住commit_id
	git reset --hard commit_id 回退到指定版本
	cat xxx.html 查看文件内容
	git checkout -- xxx.html  把该文件在工作区的修改全部撤销，回到最近一次git commit 或 git add 的状态
	git reset HEAD xxx.html 把add到暂存区的回退到工作区
	rm xxx.html 删除一个文件(工作区)
	git rm xxx.html 删除一个文件(版本库)
	git checkout --- xxx.html 版本库中的版本替代工作区的版本
	git push 把当前分支推送到远程
	git remote add origin 'github地址' 把本地仓库与GitHub仓库关联
	git push -u origin master 把本地仓库内容推送到远程库上，第一次推送加上-u,不仅可以推送远程，并把本地和远程关联
	git brank 列出所有分支
	git checkout -b dev 创建并切换到分支dev
		* 相当于git branck dev 创建分支dev
		* git checkout dev 切换到分支dev
	git marge xxx 合并指定分支xxx到当前分支
	git branch -d xxx 删除xxx分支
	git log --graph --pretty=online --abbrev-commit 
	git log --graph 看到分支合并图
	
	npm list -g 查看已安装的所有全举包
	npm info webpack 查看某个包(如webpack)的具体信息