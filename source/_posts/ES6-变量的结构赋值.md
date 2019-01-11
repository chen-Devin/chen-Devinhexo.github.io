---
title: ES6-变量的结构赋值
date: 2018-09-25 11:21:09
tags: es6
---


## es6变量的结构赋值

### 解构基本用法

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

以前，为变量赋值，只能直接指定值。
	
	```
		let a = 1;
		let b = 2;
		let c = 3;

		ES6 允许写成下面这样。
		
		let [a, b, c] = [1, 2, 3];
	```

<!-- more -->

上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子。

	```
		let [foo, [[bar], baz]] = [1, [[2], 3]];
		foo // 1
		bar // 2
		baz // 3
		
		let [ , , third] = ["foo", "bar", "baz"];
		third // "baz"
		
		let [x, , y] = [1, 2, 3];
		x // 1
		y // 3
		
		let [head, ...tail] = [1, 2, 3, 4];
		head // 1
		tail // [2, 3, 4]
		
		let [x, y, ...z] = ['a'];
		x // "a"
		y // undefined
		z // []
	```
如果解构不成功，变量的值就等于undefined。

	```
		let [foo] = [];
		let [bar, foo] = [1];
	```
以上两种情况都属于解构不成功，foo的值都会等于undefined。

另一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。

	```
		let [x, y] = [1, 2, 3];
		x // 1
		y // 2
		
		let [a, [b], d] = [1, [2, 3], 4];
		a // 1
		b // 2
		d // 4
	```
上面两个例子，都属于不完全解构，但是可以成功。

如果等号的右边不是数组（或者严格地说，不是可遍历的结构，参见《Iterator》一章），那么将会报错。

	```
		// 报错
		let [foo] = 1;
		let [foo] = false;
		let [foo] = NaN;
		let [foo] = undefined;
		let [foo] = null;
		let [foo] = {};
	```
上面的语句都会报错，因为等号右边的值，要么转为对象以后不具备 Iterator 接口（前五个表达式），要么本身就不具备 Iterator 接口（最后一个表达式）。

备注：JavaScript 原有的表示“集合”的数据结构，主要是数组（Array）和对象（Object），ES6 又添加了Map和Set。这样就有了四种数据集合，用户还可以组合使用它们，定义自己的数据结构，比如数组的成员是Map，Map的成员是对象。这样就需要一种统一的接口机制，来处理所有不同的数据结构。

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。



对于 Set 结构，也可以使用数组的解构赋值。

	```
		let [x, y, z] = new Set(['a', 'b', 'c']);
		x // "a"
	```
事实上，只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

	```
		function* fibs() {
		  let a = 0;
		  let b = 1;
		  while (true) {
		    yield a;
		    [a, b] = [b, a + b];
		  }
		}
		
		let [first, second, third, fourth, fifth, sixth] = fibs();
		sixth // 5
	```
上面代码中，fibs是一个 Generator 函数（参见《Generator 函数》一章），原生具有 Iterator 接口。解构赋值会依次从这个接口获取值。

备注：Generator 函数有多种理解角度。语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。

执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。

形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）。

### 默认值
解构赋值允许指定默认值。

	```
		let [foo = true] = [];
		foo // true
		
		let [x, y = 'b'] = ['a']; // x='a', y='b'
		let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'

	```
注意，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。

	```
		let [x = 1] = [undefined];
		x // 1
		
		let [x = 1] = [null];
		x // null

	```
上面代码中，如果一个数组成员是null，默认值就不会生效，因为null不严格等于undefined。

备注： 

* Undefined类型只有一个值，即undefined。当声明的变量还未被初始化时，变量的默认值为undefined。
* Null类型也只有一个值，即null。null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。


js 代码
 
* alert(null == undefined); //output "true"  
* alert(null === undefined); //output "false"  
* alert(typeof null == typeof undefined); //output "false"  

如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

	```
		function f() {
		  console.log('aaa');
		}
		
		let [x = f()] = [1];

	```
上面代码中，因为x能取到值，所以函数f根本不会执行。上面的代码其实等价于下面的代码。

	```
		let x;
		if ([1][0] === undefined) {
		  x = f();
		} else {
		  x = [1][0];
		}

	```
默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

	```
		let [x = 1, y = x] = [];     // x=1; y=1
		let [x = 1, y = x] = [2];    // x=2; y=2
		let [x = 1, y = x] = [1, 2]; // x=1; y=2
		let [x = y, y = 1] = [];     // ReferenceError: y is not defined

	```
上面最后一个表达式之所以会报错，是因为x用y做默认值时，y还没有声明。

### 对象解构赋值

解构不仅可以用于数组，还可以用于对象。

	```
		let { foo, bar } = { foo: "aaa", bar: "bbb" };
		foo // "aaa"
		bar // "bbb"
	```
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

	```
		let { bar, foo } = { foo: "aaa", bar: "bbb" };
		foo // "aaa"
		bar // "bbb"
		
		let { baz } = { foo: "aaa", bar: "bbb" };
		baz // undefined
	```
上面代码的第一个例子，等号左边的两个变量的次序，与等号右边两个同名属性的次序不一致，但是对取值完全没有影响。第二个例子的变量没有对应的同名属性，导致取不到值，最后等于undefined。

如果变量名与属性名不一致，必须写成下面这样。

	```
		let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
		baz // "aaa"
		
		let obj = { first: 'hello', last: 'world' };
		let { first: f, last: l } = obj;
		f // 'hello'
		l // 'world'
	```
这实际上说明，对象的解构赋值是下面形式的简写（参见《对象的扩展》一章）。

	```
		let { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };
	```
也就是说，对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

	```
		let { foo: baz } = { foo: "aaa", bar: "bbb" };
		baz // "aaa"
		foo // error: foo is not defined
	```
上面代码中，foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。

与数组一样，解构也可以用于嵌套结构的对象。

对象的解构也可以指定默认值。

	```
		var {x = 3} = {};
		x // 3
		
		var {x, y = 5} = {x: 1};
		x // 1
		y // 5
		
		var {x: y = 3} = {};
		y // 3
		
		var {x: y = 3} = {x: 5};
		y // 5
		
		var { message: msg = 'Something went wrong' } = {};
		msg // "Something went wrong"
	```
默认值生效的条件是，对象的属性值严格等于undefined。

	```
		var {x = 3} = {x: undefined};
		x // 3
		
		var {x = 3} = {x: null};
		x // null
	```
上面代码中，属性x等于null，因为null与undefined不严格相等，所以是个有效的赋值，导致默认值3不会生效。

如果解构失败，变量的值等于undefined。
