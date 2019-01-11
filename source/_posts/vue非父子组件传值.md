---
title: vue非父子组件传值
date: 2018-07-10 21:08:44
tags: vue
---

### 非父子组件之间传值

#### 路由跳转传值

发送方路由跳转方法时

	```

	  clickRowValFun(data){
        this.$router.push({path:'/pending-particulars/'+data.id});
      },
```
在需要跳转的路由后面加上你需要传递的参数


<!-- more -->


设置路由时
	```

	     {
          path: '/pending-particulars/:projectId',
          name: 'pendingParticulars',
          component: PendingParticulars
        },
	```

接收方接收时

	```

 		created(){
      		this.projectId = this.$route.params.projectId;
    	}
	```


#### 中央事件总线

在vue项目中，各组件之间是需要传值的，有时候非父子关系的组件也需要通信。在简单的场景下，使用一个空的Vue实例作为中央事件总线。称为中央事件总线传值。

通过建立中间的事件bus总线。实现非父子组件之间的数据通信。

首先建立事件bus，我会新建一个bus.js文件；注册bus。
分别在组件中使用emit和on实现数据之间的通信；

##### bus.js 

	```

		//bus.js，注册Bus
		import Vue from 'vue'
		export default new Vue()
	```

##### 页面A发送方(组件emit触发事件)

	```


		<template>
			 <div class="add-task" :class="{'ishide':isAdding}"  @click="addtask()">
   			<i class="fa fa-plus-circle" aria-hidden="true"></i>
   			添加任务
 			</div>
		</template>
		<script>
 		import Bus from '@/bus'
 		export default {
 		methods: {
		props: ['index'],
   		data () {
     		return {
       			isAdding: false
     		}
   		},
     	addtask () {
       	this.isAdding = true
       	Bus.$emit('adding-task', this.isAdding, this.index)  // 这里触发的事件是'adding-task'，
       	传递了两个参数，分别是this.isAdding和this.index
       	this.$emit('addtask')
     			}
   			}
 		}

	```

##### 页面B接收方(on接收事件)

	```

		// 模板中的代码就不展示了。
		主要展示的是script中的代码
		export default{
		data() //  这里的数据也不一一显示啦；
		created () {
		// 这里使用on监听了adding-task事件，接收到两个参数。所以一旦上面的组件中的adding-task事件触发，这里就会监听到。
    	Bus.$on('adding-task', (state, index) => {
      		if (this.index === index) {
        		this.isShow = state
      		}
    		})
  			}
		}
	```

#### 中央事件总线的坑

当完成上述中央事件总线传值之后，就可以在接收方接收到正常的值，但是会存在一些问题：

就是我第一次进去list页面的时候，我随便点击一下list下的任何一个item，控制台没有输出。但是当我第二次再点击触发事件的时候，就会输出一个测试数据。再一次进去点击，就输出两个数据。。。依次增加了。（控制台上那个“这是从上个页面传来的数据”就是测试数据）

所以，有两个问题。

问题：

* 问题1： 为什么第一次触发的时候页面B中的on事件没有被触发
* 问题2： 为什么后面再一次依次去触发的时候会出现，每一次都会发现好像之前的on事件分发都没有被撤销一样，导致每一次的事件触发执行越来越多。


##### 问题一

第一次触发的时候页面B中的on事件没有被触发

###### 产生原因
当我们还在页面A的时候，页面B还没生成，也就是页面B中的 created中所监听的来自于A中的事件还没有被触发。这个时候当你A中emit事件的时候，B其实是没有监听到的。

###### 解决办法
我们可以把A页面组件中的emit事件写在beforeDestory中去。因为这个时候，B页面组件已经被created了，也就是我们写的$on事件已经触发了，所以可以在beforeDestory的时候，$emit事件

###### 示例代码

	```

		// 修改一下A页面中的代码：
		// 这是原先的代码
  		editList (index, date, item) {
		//  点击进入编辑的页面，需要传递的参数比较多。
      		console.log(index, date, item)
      		this.item = item.type
      		this.date = date
      		this.$router.replace({path: '/moneyRecord'})
    		}
		// 重新在data属性内部定义新的变量，来存储要传过去的数据；
		然后：
 		beforeDestroy () {
 		console.log(this.highlight, '这是今年的数据', this, '看看组件销毁之前会发生什么')
 		bus.$emit('get', {
        		item: this.item,
        		date: this.date
      		})
 		},
	```
##### 问题二

后面再一次依次去触发的时候会出现，每一次都会发现好像之前的on事件分发都没有被撤销一样，导致每一次的事件触发执行越来越多。


###### 产生原因

就是说，这个$on事件是不会自动清楚销毁的，需要我们手动来销毁。（不过我不太清楚这里的external bus 是什么意思，有大神能解答一下的吗，尤大大也提到如果是注册的是external bus 的时候需要清除）

###### 解决办法

在B组件页面中添加Bus.$off来关闭

######示例代码

	```
	
		// 在B组件页面中添加以下语句，在组件beforeDestory的时候销毁。
  		beforeDestroy () {
    		bus.$off('get', this.myhandle)
  		},

	```

###### 总结

 所以，如果想要用bus 来进行页面组件之间的数据传递，需要注意亮点，组件A$emit事件应在beforeDestory生命周期内。其次，组件B内的$on记得要销毁