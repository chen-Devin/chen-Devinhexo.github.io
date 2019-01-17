---
title: vue文档阅读笔记
date: 2019-01-17 16:18:05
tags: vue
---
## vue

### vue声明式渲染

vue: Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统


```

	<div id="app">
	  {{ message }}
	</div>


	var app = new Vue({
	  el: '#app',
	  data: {
	    message: 'Hello Vue!'
	  }
	})

```

<!-- more -->

### vue实例

每个vue应用都是通过用vue函数创建一个新的vue实例开始的：


```

	var vm = new Vue({
		 // 选项
	})

```
#### 数据和方法

当一个 Vue 实例被创建时，它向 Vue 的响应式系统中加入了其 data 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

```

	// 我们的数据对象
	var data = { a: 1 }
	
	// 该对象被加入到一个 Vue 实例中
	var vm = new Vue({
	  data: data
	})
	
	// 获得这个实例上的属性
	// 返回源数据中对应的字段
	vm.a == data.a // => true
	
	// 设置属性也会影响到原始数据
	vm.a = 2
	data.a // => 2
	
	// ……反之亦然
	data.a = 3
	vm.a // => 3

```

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 data 中存在的属性才是响应式的。也就是说如果你添加一个新的属性，比如：

```

	vm.b = 'hi'

```

那么对 b 的改动将不会触发任何视图的更新。如果你知道你会在晚些时候需要一个属性，但是一开始它为空或不存在，那么你仅需要设置一些初始值

这里唯一的例外是使用 Object.freeze()，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化。

```

	var obj = {
	  foo: 'bar'
	}
	
	Object.freeze(obj)
	//页面中foo不会更新
	
	new Vue({
	  el: '#app',
	  data: obj
	})

```

除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。例如：

```

	var data = { a: 1 }
	var vm = new Vue({
	  el: '#example',
	  data: data
	})
	
	vm.$data === data // => true
	vm.$el === document.getElementById('example') // => true
	
	// $watch 是一个实例方法
	vm.$watch('a', function (newValue, oldValue) {
	  // 这个回调将在 `vm.a` 改变后调用
	})

```

### 生命周期钩子

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。

注意：

	不要在选项属性或回调上使用箭头函数，比如 
	created: () => console.log(this.a) 或 
	vm.$watch('a', newValue => this.myMethod())。
	因为箭头函数是和父级上下文绑定在一起的，this 不会是如你所预期的 Vue 实例，经常导致 
	Uncaught TypeError: Cannot read property of undefined 或 
	Uncaught TypeError: this.myMethod is not a function 之类的错误。

![](https://cn.vuejs.org/images/lifecycle.png)

#### beforeCreate

在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

#### created

在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。

#### beforeMount

在挂载开始之前被调用：相关的 render 函数首次被调用。

该钩子在服务器端渲染期间不被调用。


#### mounted

el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。

注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted：

```

	mounted: function () {
	  this.$nextTick(function () {
	    // Code that will run only after the
	    // entire view has been rendered
	  })
	}

```
该钩子在服务器端渲染期间不被调用。

#### beforeUpdate

数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。

#### updated

由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。

注意 updated 不会承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 vm.$nextTick 替换掉 updated：

```

	updated: function () {
	  this.$nextTick(function () {
	    // Code that will run only after the
	    // entire view has been re-rendered
	  })
	}

```
该钩子在服务器端渲染期间不被调用。

#### activated

keep-alive 组件激活时调用。

该钩子在服务器端渲染期间不被调用。

#### deactivated

keep-alive 组件停用时调用。

该钩子在服务器端渲染期间不被调用。

#### beforeDestroy

实例销毁之前调用。在这一步，实例仍然完全可用。

该钩子在服务器端渲染期间不被调用。

#### destroyed

Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

该钩子在服务器端渲染期间不被调用。
