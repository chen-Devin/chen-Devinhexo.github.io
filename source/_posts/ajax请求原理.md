---
title: ajax请求原理
date: 2018-07-07 06:58:51
tags: ajax
---

### 浏览器输入url发生了什么

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%871.png)

<!-- more -->

#### DNS域名解析

* 在浏览器DNS缓存中搜索
* 在操作系统DNS缓存中搜索查找系统host文件看是否有对应IP
* 路由器缓存搜索
* 向本地首选DNS服务器发送域名解析请求

#### 建立TCP连接

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%872.jpg)

###### 三次握手

发送端首先发送一个带SYN（synchronize）标志的数据包给接收方，接收方收到后，回传一个带有SYN/ACK(acknowledegment)标志的数据包以示传达确认信息。最后发送方再回传一个带ACK标志的数据包，代表握手结束。在这过程中若出现问题中断，TCP会再次发送相同的数据包。

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%873.png)

###### 四次挥手

四次挥手（Four-Way Wavehand）即终止TCP连接，就是指断开一个TCP连接时，需要客户端和服务端总共发送4个包以确认连接的断开

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%874.jpg)

###### 三次握手与四次挥手

* 三次握手流程
	* 客户端发个请求“开门呐，我要进来”给服务器
	* 服务器发个“进来吧，我去给你开门”给客户端
	* 客户端有很客气的发个“谢谢，我要进来了”给服务器

* 四次挥手流程
	* 客户端发个“时间不早了，我要走了”给服务器，等服务器起身送他
	* 服务器听到了，发个“我知道了，那我送你出门吧”给客户端，等客户端走
	* 服务器把门关上后，发个“我关门了”给客户端，然后等客户端走
	* 客户端发个“我知道了，我走了”，之后自己就走了

#### 发起http请求

##### 请求方法
* GET:获取资源
* POST:传输实体主体
* HEAD:获取报文首部
* PUT:传输文件
* DELETE:删除文件
* OPTIONS:询问支持的方法
* TRACE:追踪路径


#### 接收响应结果

##### http响应常见代码
* 1**：信息性状态码
* 2**：成功状态码
* 200：OK 请求正常处理
* 204：No Content请求处理成功，但没有资源可返回
* 206：Partial Content对资源的某一部分的请求
* 3**：重定向状态码
* 301：Moved Permanently 永久重定向
* 302：Found 临时性重定向
* 304：Not Modified 缓存中读取
* 4**：客户端错误状态码
* 400：Bad Request 请求报文中存在语法错误
* 401：Unauthorized需要有通过Http认证的认证信息
* 403：Forbidden访问被拒绝
* 404：Not Found无法找到请求资源
* 5**：服务器错误状态码
* 500：Internal Server Error 服务器端在执行时发生错误
* 503：Service Unavailable 服务器处于超负载或者正在进行停机维护

#### 浏览器解析html


#### 浏览器布局渲染

##### html解析
标记化是词法分析过程，将输入内容解析成多个标记。HTML 标记包括起始标记、结束标记、属性名称和属性值。标记生成器识别标记，传递给树构造器，然后接受下一个字符以识别下一个标记；如此反复直到输入的结束


![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%875.png)

在创建解析器的同时，也会创建 Document 对象。在树构建阶段，以 Document 为根节点的 DOM 树也会不断进行修改，向其中添加各种元素。标记生成器发送的每个节点都会由树构建器进行处理。规范中定义了每个标记所对应的 DOM 元素，这些元素会在接收到相应的标记时创建。这些元素不仅会添加到 DOM 树中，还会添加到开放元素的堆栈中。此堆栈用于纠正嵌套错误和处理未关闭的标记

##### css解析

解析器会将 CSS 文件解析成 StyleSheet 对象，且每个对象都包含 CSS 规则。CSS 规则对象则包含选择器和声明对象，以及其他与 CSS 语法对应的对象

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%9B%BE%E7%89%876.png)