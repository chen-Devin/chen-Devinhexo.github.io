---
title: vuex
date: 2018-07-25 16:49:20
tags: vue
---

VUEX 


每一个 Vuex 应用的核心就是 store（仓库）。

“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和单纯的全局对象有以下两点不同

* Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

* 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

<!-- more -->  

1：安装vuex

	npm install vuex --save-dev

2:建立全局store

* 在src文件夹下，新建文件夹（一般我们取名store），并在该文件夹下创建存储数据的js文件。
* 在main.js文件下，我们需要将存储的数据文件设置为全局形式，方便引用

```

		import store from './你新建的文件夹文字/你文件夹下的文件名字'
		new Vue({
		  el: '#app',
		  router,
		  store, //这里不要忘记咯
		  render: h => h(App)
		})

```

3:编写js文件
1：定义state，用来装所需要存储的数据，初始值是空。

```

		const state = {
			user: {
		
			}
		}

```

2. 接下来我们定义mutation，编写我们要改变的事件，去接受值，参数为两个，一个是state，一个是payLoad（就是我们要存储的所有数据）

```

	const mutations = {
	  setUserInfo(state, payload) {
	    state.user = payload //现在我们把存储的值都放在state的user对象下
	  }
	}

```

3. 将我们的state和mutation暴漏出去，用于全局引用

```

	export default new Vuex.Store({
	  state,
	  mutations
	})

```

4. 登录存储
在我们获取登录接口并且服务器返回成功后，进行数据存储

```

	this.$store.commit('setUserInfo', {data:rep.data.data})

```


5.调用存储数据
```

	this.$store.state.user//输出结果就是我们存储进去的信息

```



