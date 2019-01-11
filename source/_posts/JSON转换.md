---
title: JSON转换
date: 2018-03-08 20:21:07
tags: json
---

### json字符串转化成json对象
    
#### jquery的方法
var jsonObj = $.parseJSON(jsonStr)

#### js 的方法
var jsonObj =  JSON.parse(jsonStr)

### json对象转化成json字符串 

#### js方法
var jsonStr1 = JSON.stringify(jsonObj)

<!-- more -->

 
### json对象和json字符串之间的相互转换 

##### 列一：

	比如我有两个变量，我要将a转换成字符串，将b转换成JSON对象：

	var a={"name":"tom","sex":"男","age":"24"};

	var b={"name":"Mike","sex":"女","age":"29"};

	在Firefox，chrome，opera，safari，ie9，ie8等高级浏览器直接可以用JSON对象的stringify()和parse()方法。

	JSON.stringify(obj)将JSON转为字符串。JSON.parse(string)将字符串转为JSON格式；

	上面的转换可以这么写：
    
	var a={"name":"tom","sex":"男","age":"24"};
 
	var b={"name":"Mike","sex":"女","age":"29"};
 
	var aToStr=JSON.stringify(a);
 
	var bToObj=JSON.parse(b);
 
	alert(typeof(aToStr));  //string
 
	alert(typeof(bToObj)); //object

	JSON.stringify()

	ie8(兼容模式),ie7和ie6没有JSON对象，不过http://www.json.org/提供了一个json.js,这样ie8(兼容模式),ie7和ie6就可以支持JSON对象以及其stringify()和parse()方法；

	你可以在https://github.com/douglascrockford/JSON-js上获取到这个js，一般现在用json2.js。

	ie8(兼容模式),ie7和ie6可以使用eval()将字符串转为JSON对象，

	var c={"name":"Mike","sex":"女","age":"29"};
 
	var cToObj=eval("("+c+")")；
 
	alert(typeof(cToObj));

	JQuery中也有将字符串转为JSON格式的方法jQuery.parseJSON( json )，接受一个标准格式的 JSON 字符串，并返回解析后的 JavaScript （JSON）对象。

	当然如果有兴趣可以自己封装一个jQuery扩展，jQuery.stringifyJSON(obj)将JSON转为字符串。

 

##### 例二：
    
	<script type="text/javascript">
        var jsonStr = '[{"id":"01","open":false,"pId":"0","name":"A部门"},
	{"id":"01","open":false,"pId":"0","name":"A部门"},
	{"id":"011","open":false,"pId":"01","name":"A部门"},<br>
	{"id":"03","open":false,"pId":"0","name":"A部门"},
	{"id":"04","open":false,"pId":"0","name":"A部门"}, 
	{"id":"05","open":false,"pId":"0","name":"A部门"}, 
	{"id":"06","open":false,"pId":"0","name":"A部门"}]';
      //  var jsonObj = $.parseJSON(jsonStr);
      var jsonObj =  JSON.parse(jsonStr)
        console.log(jsonObj)
     var jsonStr1 = JSON.stringify(jsonObj)
     console.log(jsonStr1+"jsonStr1")
 	</script>

 

    json对象转化成数组 
	<script type="text/javascript">
        var jsonStr = '[{"id":"01","open":false,"pId":"0","name":"A部门"},
	{"id":"01","open":false,"pId":"0","name":"A部门"},
	{"id":"011","open":false,"pId":"01","name":"A部门"},<br>
	{"id":"03","open":false,"pId":"0","name":"A部门"},
	{"id":"04","open":false,"pId":"0","name":"A部门"}, 
	{"id":"05","open":false,"pId":"0","name":"A部门"}, 
	{"id":"06","open":false,"pId":"0","name":"A部门"}]';
      //  var jsonObj = $.parseJSON(jsonStr);
      var jsonObj =  JSON.parse(jsonStr)
        console.log(jsonObj)
     var jsonStr1 = JSON.stringify(jsonObj)
     console.log(jsonStr1+"jsonStr1")
     var jsonArr = [];
     for(var i =0 ;i < jsonObj.length;i++){
            jsonArr[i] = jsonObj[i];
     }
     console.log(typeof(jsonArr))
	</script>