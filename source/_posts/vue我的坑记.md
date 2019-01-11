---
title: vue我的坑记
date: 2018-06-07 21:42:30
tags: vue
---

#### element UI select下拉选项位置问题

在使用elementUI下拉选项时，可能存在下拉时下拉列表选项框的位置距离下拉框所在的位置距离过大，这个是由于elementUI自己设置的根据下拉框位置定位，而他可能是根据position:absolute;来进行定位的,而我们要在全局设置他的 position:fixed !important;即可。(注意使用!important增加权重)


<!-- more -->

附加position各种值

* absolute:生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
* fixed:生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
* relative:生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
* static:默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
* inherit:规定应该从父元素继承 position 属性的值。


#### element UI 组件默认传参和自定义传参的解决方法

如下代码
```

        <div v-for="(item,index) in object.cooperationDepartmentNumber">
          <div class="entrustingPartyList">
            <el-row>
              <el-col :span="12"> 
                <el-form-item label="协办单位">
                <el-autocomplete
                  class="inline-input"
                  v-model="object.cooperationDepartment.otherArray[index].unit"
                  :fetch-suggestions="unitQuerySearch"
                  placeholder="请输入协办单位"
                  :trigger-on-focus="false"
                  @select="unitHandleSelect"
                ></el-autocomplete>
                </el-form-item>
              </el-col>
              <el-col :span="12"> 
                <el-form-item label="协办部门" v-show="interior">
                  <el-input v-model="object.cooperationDepartment.otherArray[index].cooperation" placeholder="协办部门"></el-input>
                </el-form-item>
              </el-col>
              <el-col :span="12"> 
                <el-form-item label="协办单位联系人" v-show="external">
                  <el-input v-model="object.cooperationDepartment.otherArray[index].cooperation" placeholder="协办部门"></el-input>
                </el-form-item>
              </el-col>
            </el-row>
          </div>
        </div>

```

当我们v-for有很多个相同的组件时，我们需要知道选中的是第几个组件,那么我们肯定想要知道对应的[index],你会想到下面这样[item]是默认的值
```

	  <el-col :span="12"> 
	    <el-form-item label="协办单位">
	    <el-autocomplete
	      class="inline-input"
	      v-model="object.cooperationDepartment.otherArray[index].unit"
	      :fetch-suggestions="unitQuerySearch"
	      placeholder="请输入协办单位"
	      :trigger-on-focus="false"
	      @select="unitHandleSelect(item, index)"
	    ></el-autocomplete>
	    </el-form-item>
	  </el-col>
```
解决办法是写个闭包，这样index就表示你的第几个组件
```

	  <el-col :span="12"> 
	    <el-form-item label="协办单位">
	    <el-autocomplete
	      class="inline-input"
	      v-model="object.cooperationDepartment.otherArray[index].unit"
	      :fetch-suggestions="unitQuerySearch"
	      placeholder="请输入协办单位"
	      :trigger-on-focus="false"
	      @select="((item)=>{unitHandleSelect(item, index)})"
	    ></el-autocomplete>
	    </el-form-item>
	  </el-col>
```
这样你在调用这个方法的时候就可以知道是第几个组件对应的了，然后就可以对那个组件进行操作了。


#### vue路由跳转参数传递


发送方路由跳转方法时
```

	  clickRowValFun(data){
        this.$router.push({path:'/pending-particulars/'+data.id});
      },
```
在需要跳转的路由后面加上你需要传递的参数

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


#### vue2 "Cannot read property 'length' of undefined"

最近在项目中总是遇见报错"length of undefined"的问题，因为项目的需要要显示存在的个数，所以通过length来进行求职

```

	     
          this.projectReportSumNum = val.reportArray.length;
```

虽然界面可以显示length数据，但是控制台肥肠傲娇一直报错。大概是说找不到一个undefined的length

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20180619120350.png)

这明明不是找到了，为什么还报错呢？
花了点时间研究下才知道，vue的数据绑定在刚开始只是和内存建立联系，并没有真正的和后台的数据挂上钩，所以一开始的val.reportArray只是一个空值，必须在之前加个if判断，确保有值以后再开始计算length

```

	       if(val.reportArray){
            this.projectReportSumNum = val.reportArray.length;
          }
```

这样就不会在控制台显示报错了。。


#### vscode使用vue中的v-for提示错误

在项目中是用v-for时，vscode提示错误信息

![Image text](https://raw.githubusercontent.com/chen-Devin/img-folder/master/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20180619121857.png)


```

	      
        <div v-for="(item,index) in object.cooperationDepartmentNumber">
```
Vue 2.2 之后，要求 component 进行列表渲染时，必须指定 key，因此这里可能是 vscode 的一个误报（tr 不是 component），如果不想看到这样的提示，你可以绑定一个 key：<tr v-for="(word,index) in list" :key="index">

```

	      
        <div v-for="(item,index) in object.cooperationDepartmentNumber" :key:"index">
```
如上所示：在v-for循环中加入：key值即可消除该提示。

#### vue 改变对象属性。视图不刷新问题

在vue的data数据中心定义一个对象obj，然后在触发事件时给obj添加或修改属性的时候，页面中的视图不会同步更新，只有当其他数据发生改变时，视图才会同步更新数据，按理来说vue data数据中心的数据是双向绑定的，当数据中心的数据发生改变时，视图就会同步更新才对。

后来通过查阅官网资料发现：

Vue 不能检测到对象属性的添加或删除。由于 Vue 会在初始化实例时对属性执行 getter/setter 转化过程，所以属性必须在 data 对象上存在才能让 Vue 转换它，这样才能让它是响应的。例如：


```

	      
        var vm = new Vue({
		data:{
		a:1
		}
		})
		// `vm.a` 是响应的
		vm.b = 2
		// `vm.b` 是非响应的
```

Vue 不允许在已经创建的实例上动态添加新的根级响应式属性(root-level reactive property)。然而它可以使用 Vue.set(object, key, value) 方法将响应属性添加到嵌套的对象上：


```

	      
        Vue.set(vm.someObject, 'b', 2)
```

您还可以使用 vm.$set 实例方法，这也是全局 Vue.set 方法的别名：

```

	      
        this.$set(this.someObject,'b',2)
```
