---
layout: new
title: ES6-let和const命令
date: 2019-04-29 19:44:57
tags: es6
---
# ES6

## es6简介及转码

ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。

ES6 从开始制定到最后发布，整整用了 15 年。

<!-- more -->  

### Babel 转码器

Babel 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在现有环境执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。

下面的命令在项目目录中，安装 Babel。

	$ npm install --save-dev @babel/core

Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。

Babel 提供命令行工具@babel/cli，用于命令行转码。

它的安装命令如下。

	$ npm install --save-dev @babel/cli

### Traceur 转码器

Google 公司的Traceur转码器，也可以将 ES6 代码转为 ES5 代码。

作为命令行工具使用时，Traceur 是一个 Node 的模块，首先需要用 npm 安装。

	$ npm install -g traceur

## let与const命令

### let命令

#### 作用域

ES6 新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。

for循环的计数器，就很合适使用let命令。

	```
	
		for (let i = 0; i < 10; i++) {
		  // ...
		}
		
		console.log(i);
		// ReferenceError: i is not defined
	
	```

上面代码中，计数器i只在for循环体内有效，在循环体外引用就会报错。

for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

	```
		
		for (let i = 0; i < 3; i++) {
		  let i = 'abc';
		  console.log(i);
		}
		// abc
		// abc
		// abc

	```

上面代码正确运行，输出了 3 次abc。这表明函数内部的变量i与循环变量i不在同一个作用域，有各自单独的作用域。

#### 不存在变量提升

var命令会发生“变量提升”现象，即变量可以在声明之前使用，值为undefined。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。

为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

	```

		// var 的情况
		console.log(foo); // 输出undefined
		var foo = 2;
		
		// let 的情况
		console.log(bar); // 报错ReferenceError
		let bar = 2;

	```

上面代码中，变量foo用var命令声明，会发生变量提升，即脚本开始运行时，变量foo已经存在了，但是没有值，所以会输出undefined。变量bar用let命令声明，不会发生变量提升。这表示在声明它之前，变量bar是不存在的，这时如果用到它，就会抛出一个错误。

#### 暂时性死区

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

	```

		var tmp = 123;
		
		if (true) {
		  tmp = 'abc'; // ReferenceError
		  let tmp;
		}

	```

上面代码中，存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。

ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

	```

		if (true) {
		  // TDZ开始
		  tmp = 'abc'; // ReferenceError
		  console.log(tmp); // ReferenceError
		
		  let tmp; // TDZ结束
		  console.log(tmp); // undefined
		
		  tmp = 123;
		  console.log(tmp); // 123
		}
		

	```


上面代码中，在let命令声明变量tmp之前，都属于变量tmp的“死区”。

“暂时性死区”也意味着typeof不再是一个百分之百安全的操作。作为比较，如果一个变量根本没有被声明，使用typeof反而不会报错。


	```
		typeof x; // ReferenceError
		let x;

		typeof undeclared_variable // "undefined"

	```

ES6 规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。这样的错误在 ES5 是很常见的，现在有了这种规定，避免此类错误就很容易了。

总之，暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

#### 不允许重复声明

let不允许相同作用域内重复声明同一个变量；因此不能在函数内部重新声明参数

	```

		// 报错
		function func() {
		  let a = 10;
		  var a = 1;
		}
		
		// 报错
		function func() {
		  let a = 10;
		  let a = 1;
		}
		
		function func(arg) {
		  let arg;
		}
		func() // 报错
		
		function func(arg) {
		  {
		    let arg;
		  }
		}
		func() // 不报错

	```
#### 块级作用域

ES5只有全局作用域和函数作用域，没有块级作用域，这可能会带来以下问题：

* 内层变量可能会覆盖外层变量
* 用来计数的循环变量泄露为全局变量

ES6：let实际上为 JavaScript 新增了块级作用域。

块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（IIFE）不再必要了。

	```
		
		// IIFE 写法
		(function () {
		  var tmp = ...;
		  ...
		}());
		
		// 块级作用域写法
		{
		  let tmp = ...;
		  ...
		}

	```

#### 块级作用域与函数声明

ES5规定：函数只能在顶层作用域和函数作用域之中声明，不能再块级作用域声明；

但是浏览器并没有遵循这个规定，为了兼容以前的旧代码，还是支持在块级作用域之中声明。

ES6引入了块级作用域，明确允许在块级作用域之中声明函数，
ES6 规定，块级作用域之中，函数声明语句的行为类似于let，在块级作用域之外不可引用。
