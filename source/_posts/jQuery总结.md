---
layout: w
title: jQuery总结
date: 2017-07-07 22:33:23
tags: jQuery
---


# jQuery
## 选择器
>所有选择器获取的对象均为包装集，需通过[index]或get(index)获取，jQuery内部有隐式迭代，通过$.each()实现

<!-- more -->

### 基本选择器
>id选择器$(#id) 				选中对应id的标签
>
>类名选择器$(.className)		选中对应类名的标签，获得为多个
>
>标签选择器$(tagName)			选中对应标签名的标签，获得为多个
>
>交集选择器$(tagName.className#id) 选中对应标签名中对应类名（或其他）的标签，获得为多个
>
>并集选择器$(a,b,c,)
>

### 层级选择器
      
>子代选择$("选择器a>选择器b")		选中选择器a的亲儿子中对应选择器b的标签

>后代选择$("选择器a 选择器b")		选中选择器a的子级标签中对应选择器b的标签
      
>相邻选择器$("选择器a+选择器b")   选中选择器a的下一个兄弟标签对应选择器b,中间不能有间隔
      
>兄弟选择器$("选择器a～选择器b")   获取选择器a的后面的所有符合选择器b的兄弟级标签，有间隔也没事
>
> $("选择器a“).children()   表示获取所有的选择器a中的子类标签（亲儿子）
> 
> $("选择器a“).children(“选择器b")   表示获取选择器a中的子类标签中(所有亲儿子中)的符合选择器b要求的标签，相当于拿到子类标签后用.filter(“选择器b")方法
> 
> $("选择器a“).find(“选择器b")  必须带参数，表示查找选择器a的子级元素符合选择器b要求的标签
>
> $("选择器a“).siblings() 	表示获取自己的所有的兄弟姊妹级标签，不包括自己
>
> $("选择器a“).next()/.prev()			表示获取选择器a的下一个/或前一个兄弟标签
>
> $("选择器a“).nextAll()	/.prevAll()		表示获取选择器a的后面／或前面所有兄弟标签
>

### 父级选择器	
>$("选择器a").parent()			获取当前元素选择器a的父元素，亲父亲。
>
>$("选择器a").parents()			获取当前元素选择器a的父级元素，一直到html级
>
>	如不想所有父级元素都拿，可在（）中传入参数
>
>$("选择器a").parents("选择器b")			获取当前元素选择器a的父级元素中"选择器b"的元素
>
>offsetParent() 这是方法！拿到最近的有定位的父级元素，如没有则拿到html。


### 伪类选择器

>$("ul li:first")	同$("ul li").first()选中元素中第一个
>同$("ul li:eq(0)")同$("ul li").eq(0)
>
>$("ul li:last")		同$("ul li").last()	选中元素中最后一个
>
>$("ul li:even")				选中元素中偶数个，从0开始，第一个元素为偶数。
>
>$("ul li:odd")				选中元素中奇数个,第二个元素为奇数。
>
>$("ul li:eq(n)")	同$("ul li").eq(n)		n表示第n个。(筛选、过滤选择器)
>

### filter和not选择器
>filter用法：$("选择器a").filter("选择器b"）从选择器a取到的数组里用选择器b过滤
>
>not用法：$("选择器a").not("选择器b"）从选择器a取到的数组里去掉选择器b对应的

### 索引
>$(this).index()  返回this所在父元素中的标签顺序，只与亲兄弟有关

>	return ( this[0] && this[0].parentNode ) ? 	this.first().prevAll().length : -1;
>

## 事件对象
### 注册事件
>简单注册事件
>
		click(handler)              单击事件
		blur(handler)               失去焦点事件
		mouseenter(handler)         鼠标进入事件
		mouseleave(handler)         鼠标离开事件
		dbclick(handler)            双击事件
		change(handler)             改变事件，如：文本框值改变，下来列表值改变等
		focus(handler)              获得焦点事件
		keydown(handler)            键盘按下事件
		
>
>bind方式
>
	.bind( eventType [, eventData ], handler )
	可在第一个参数传入多个事件，用空格隔开，同时注册，缺点是不支持动态创建的元素。
>
>delegate方式
>
	$(selector).delegate( selector, eventType, handler );
	第一个参数：selector，对$(selector)包装集下的所有子元素进行过滤，用于指定哪些后代元素可以触发绑定的事件。
	第二个参数：事件类型
	第三个参数：事件处理函数

>on的方式注册事件
>
	$(selector).on(events[,selector][,data],handler);
	第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
	第二个参数：selector, 对$(selector)包装集下的所有子元素进行过滤，用于指定哪些	后代元素可以触发绑定的事件。
	第三个参数：data，传递给处理函数的数据，事件触发的时候在事件处理函数中通过event.data来使用
	第四个参数：handler，事件处理函数

### 事件解绑

#### unbind undelegate

>.unbind() 解绑 bind方式绑定的所有事件
>
>.unbind("click") 解绑 bind方式绑定的指定事件
>
>undelegate同unbind，仅解绑的是delegate方式注册的事件
>
>off解绑on方式绑定的事件
>
	$(selector).off(); 解绑匹配元素的所有事件，包括代理的。
	$(selector).off("click"); 解绑匹配元素的所有click事件,包括代理的。
	$(selector).off( "click", "**" );  解绑所有代理的click事件(子元素事件)，元素本身的事件不会被解绑 

	
### 阻止冒泡

>同原生js，.stopPropagation();

### 阻止默认行为(如a标签跳转，等)

>同原生js，.preventDefault();

### 事件触发 trigger
	$(selector).triggerHandler( type, data )调用了trigger，等于jQuery.event.trigger( type, data, $(selector)[0], true )
	触发绑定的处理函数，但不触发其默认行为。只影响 jQuery 对象的第一个匹配元素。
	返回的是事件处理函数的返回值，而不是具有可链性的 jQuery 对象。此外，如果没有处理程序被触发，则这个方法返回 undefined。
	
 	trigger( event, data, elem, onlyHandlers ) 触发事件，event传入事件名即可,默认onliHandlers为false，是否由handler引发。
 	trigger(event,[arguments]*)	可在trigger中传入参数。
 	trigger默认会触发事件冒泡，会引起事件（比如表单提交）的默认行为。 会操作 jQuery 对象匹配的所有元素。返回是jQuery对象。


### 几个属性

	this	指代当前对象，执行处理程序的对象
	currentTarget	指代当前对象，执行处理程序的对象
	delegateTarget 指代委托对象，执行处理程序的对象，谁注册指代谁。
	target	最原始的事件源，同原生(原生中ie8为srcElement)。

### 几个坐标

	screenX/screenY 同原生，鼠标点击位置到屏幕左上角坐标
	clientX/clientY 同原生，点击位置到浏览器左上角位置
	pageX/pageY 同原生，没有兼容性问题，点击位置到页面左上角位置，包括滚动长度
	
## 常用方法

### 文本和属性
>方法均通过jQuery对象调用
>
>text()	获取文本，有标签会忽略
>
>text("需要设置的文本")	设置文本，有标签先转义
>
>表单内容获取使用 .val() 同样，如果带参数表示设置value值
>
>css("需要获取的属性如width") 如只有一个参数，则用来获取属性，如果调用css方法的对象为具有多个元素的包装集，则只返回第一个元素的属性。如$("ul li").css("font-size")默认返回第一个ul下第一个li的文字尺寸。
>
>但如第一个参数为键值对则用来设置属性，如有两个参数为设置属性。
>
>举例（均为设置属性）：
>
		$("div").css("width","600");
		$("div").css({
          'width':'300px',
          'height':'500px',
          'background-color':"blue"
        })

### 操作类样式
>
>$("div").addClass('demo'); 为div增加demo类，保留原有其他类
>
>$("div").removeClass('demo'); 为div移除demo类，保留原有其他类
>
>$("div").toggleClass('demo'); demo切换类，如有demo类则移除没有则增加，对原有其他类无影响。
>
### end()方法

>返回jQuery对象持有的prevObject。每个jQuery均有此属性，默认为document。链式编程中每对原对象造成一次破坏性的返回则对现有对象prevObject属性增加原对象的引用。

## 动画

所有speed参数均可传入字符串或是数字，对应slow=600，normal=400，fast=200，不传或是传入字符串不对则默认normal(show及hide方法例外)。如果为number类型，则表示动画的持续时间毫秒值。所有的动画都可带回调函数，当动画结束时调用。
### 隐藏和显示、切换
>show() 
>
>>无参数		此时表示显示对象，注意无动画效果，相当于css("display","block);
>>
>>带第一个参数，表示speed参数。
>>
>>带两个参数，第一个参数同上，第二个参数为动画完成后的回调函数。
>>
>>hide()		类似show方法。
>>
>
>toggle()	
>>
>>类似show方法。在调用对象显示时调用hide方法，隐藏时调用show方法。
>>
>>以上三个方法均可传键值对对象。属性包括duration持续时间 easing动画类型（默认swing，还有linear等） complete回调函数 queue是否加入队列。还有其他较少用参数。


### slide 滑入滑出改变的是高度

>高度只是暂时改变，再调用fade、show之类方法会回复原状。
>
>slideDown(speed,callback)	用法及参数传入均同show方法，注意无参会有动画效果。
>
>slideUp()			往上拉
>
>slideToggle()
>

### fade 淡入淡出改变的是不透明度
>fadeIn 		淡入，显示出来
>
>fadeOut		淡出，慢慢消失
>
>fadeToggle
>
>fadeTo(speed,to)	to必须位于第二个参数，第一个参数同speed。注意，经fadeTo改变后的不透明度，其他fadeIn或是fadeToggle重新显示出来时只会等于to，同样fadeTo也可以有回调函数。
>

### 动画
>.animate({params}, speed, callback) 第一个参数必选且需为键值对对象。
>
>.stop(clearQueue, jumpToEnd) 默认两个参数均为false，表示立即停止现有动画并执行下一个动画。第一个参数表示后续动画是否不执行true不执行，false执行(动画队列，链式编程可能会有动画队列)。第二个参数true时立即跳至当前动画结束位置，false时立即停止当前动画。动画还未执行完时调用stop方法则回调函数不执行。
>	
>举例 $ele.animate(1).animate(2),如1过程中执行stop()，则1停止并马上执行2. stop(true,true)立即跳至1动画末不动。stop(false,true)立即跳至1动画末位置并执行2.stop(true)全部停止。


## 动态创建元素

## 创建方式

>使用$("<a href="#">这是一个a标签</a>")  
>
>html() 不传参数则获取标签内容，传参数为设置内容，同innerHtml。

## 添加元素方法

>append()与appendTo() 		同appendChild()方法，调用举例：
>
>		$parentNode.append($node)同$node.appendTo($parentNode)
>		同parentNode.appendChild(node)
>表示在子元素最后增加node节点，方法由父元素调用。
>
>如果是给多个目标追加一个元素，那么append()方法的内部会复制多份这个元素，然后追加到多个目标里面去(原有元素删除)。
>
>prepend()与prependTo()		由父元素节点调用，调用举例：
>
>		$parentNode.prepend($node)同$node.prependTo($parentNode)
>		同parentNode.insertBefore(node,parentNode.firstElementChild);
>
>after()和insertAfter()	
>
>before()和insertBefort()		由兄弟节点调用，调用举例：
>
> 		A.after(B)同B.insertAfter(A) 表示A节点后面增加B节点
> 		A.before(B)同B.insertBefore(A) 表示A节点前面增加B节点    
>
>
>
>clone() jQuery对象的clone方法都是深度克隆，也可以传入boolean参数，但是true表示克隆事件，false则不克隆事件。
>
>

## 清空节点
>
>$node.empty()同$node.html("")，清空标签内容，但标签名仍在。empty()会清除标签事件所以推荐使用，html不会不建议使用。
>
>$node.remove() 如果无参数或是传入可转为false的字符如undefined、NaN等则删除node自身，标签名都删除。如果传入参数则相当于传入filter，根据选择器删除node集合中匹配的节点。	


## 属性

### 设置及获取
>
>attr()
>
>prop() 如果设置单属性值，比如checked,disabled,selected时使用，原因：checked属性被选中后如鼠标点选改变选中属性此时行内属性不改变，所以设置过一次后再设置无效。
>
>注意：prop设置了属性后检查元素时行内属性看不出改变，但实际有效果，原因不明。
>
>可以设置为空，比如.prop("onclick",null);ie8,9,11需用这种方式移除行内onclick。
>
>removeAttr() 传入参数，移除对应属性，连属性名一起移除.如无参数则不移除。多参数可用空格隔开。

### 位置

>.offset()  offset() 返回一个对象，此对象里面有两个属性  left  top  获取的left  top值，始终是以页面为准.这是一个可读写的属性，设置时传入键值对，格式为.offset(left:num1,top:num2)设置,num1、num2为number类型。如元素本身无定位则会强制给其增加一相对定位,此定位是以border外边框为基准计算的。
>
>
>.position()   返回一个对象，此对象里面有两个属性  left  top获取的自身的margin到离自己最近的定义的父盒子的border内边框之间的距离，获取的为number类型数据 。只能获取属性，同node.style.left获取到的距离(带px)。
>
>>$(selector).css("height");  字符串类型 带单位px。
>
>width、height	获取对象可视区宽度或高度，均为number类型。获取的是实际宽高，padding内边框区域。
>
>scrollTop/scrollLeft(offset) 方法返回或设置匹配元素的滚动条的垂直位置/水平位置。

	注释：该方法对于可见元素和不可见元素均有效。
	注释：当用于获取值时，该方法只返回第一个匹配元素的scrollTop/scrollLeft(offset)。
	注释：当用于设置值时，该方法设置所有匹配元素的 scrollTop/scrollLeft(offset)。

## 其他
### each
>对应原生js为foreach，用法：

	原生forEach
	var arr=[10,20,30,40,50];
	arr.forEach(item,index){
		console.log(index+":"+item);
	}
	也可写成：
    arr.forEach(function (item,index) {
        console.log(index+":"+item)
    })
	输出：0:10,1:20,2,30,3:40,4:50
	只能遍历数组。
>	

	jQuery中的each
	用法一遍历数组：
	$.each(arr,callback(key,value));
	var arr=[10,20,30,40,50];
    $.each(arr,function (index,item) {
        console.log(index+":"+item)
    })
    输出：0:10,1:20,2,30,3:40,4:50
 
	用法二遍历对象：
	$.each(obj,callback(key,value));
	
	用法三遍历jQuery对象
	$(selector).each(function(index,ele){}),注意其中ele为Dom对象



											