---
title: js面向对象与高级
date: 2018-04-25 18:25:25
tags: js
---
# JavaScript重点

## 数据类型
- 简单数据类型（基本数据类型）
    + number
    + string
    + boolean
    + undefined
    + null

- 复杂数据类型（引用数据类型）
    + object

<!-- more -->

#### js有几种数据类型？
- 6种

#### js提供了哪些内置对象？
- Array、Math、Date、Error、RegExp、
Function、String、Number、Boolean、Object、JSON

## 基本数据类型与引用数据类型的存储与赋值

#### 基本数据类型
- 赋值时赋的是值的copy版本

#### 引用数据类型
- 赋值赋的是对象的引用地址

#### 关于引用数据类型的考题补充
- 如果修改变量的引用，那么不会产生连带影响
```javascript
var o = { a:1 };
var o2 = o;
o2 = { a: 100 } // 这是修改变量
console.log(o.a); // 1
```

- 如果修改变量引用对象的属性值，那么会产生连带影响
```javascript
var o = { a:1 };
var o2 = o;
o2.a =100 // 这是修改变量引用对象的属性值
console.log(o.a); // 100
```

## 运算符

#### 逻辑运算符 && || !

- && 
    + 从左向右寻找转布尔为false的值，找到返回这个值，找不到返回最后一个值。
    + 注意：返回的结果不一定是true或false

- ||
    + 从左向右寻找转布尔为true的值，找到返回这个值，找不到返回最后一个值。
	+ 注意：返回的结果不一定是true或false
	
- !
    + 一个!可对数据取反
    + 两个!求数据布尔值
    + 注意：返回值不是true就是false

- 转换布尔为false的数据有哪些？
    + 0、undefined、null、false、''、NaN
    + 除此之外的数据转换布尔都为true

#### 相等运算符 == ===

- ==
    + 先对数据类型进行转换，数据类型一致后再比较值
    + NaN不等于任何值，包括自己
    + null与undefined互等，但不等于其他任何值(尤其是0和false)
    + 数字与布尔数据，和其他任何值比较，全部转换成数字再比较
    + 对象与对象比较内存地址
    + 对象与字符串，转字符串再比较

- ===
    + 双重比较，先比较数据类型，再比较值

- 三元运算符 ? :
    + 先计算?号前面表达式的结果
    + 结果布尔为true返回:号前面表达式的运行结果
    + 结果布尔为false返回:号后面表达式的运行结果

#### 其他

- typeof
    + 作用：用于检测数据类型
    + 无法检测null，因为检测结果为'object'
    + 检测对象不准(因为null结果也为object)，检测对象不具体，因为全部都是object
    + 唯独检测函数类型对象比较准确

- in
    + 作用：用来检测对象中是否含有某属性
    + 语法：属性名 in 对象
    ('inObj' in obj)

- delete
    + 作用：删除对象属性
    + 语法：delete 对象.属性名 || delete 对象[属性名]
    (delete o.a;)

- 对象的属性访问方式
    - .语法
        + 不能访问数字开头的属性
        + 不能使用变量
    - []语法
        + 可以使用数字
        + 可以使用变量
        + 注意：属性名记得加引号，数字可加可不加，变量千万不要加

## 语句

#### 分支语句
- if，if else , switch case

#### 循环语句
- for，while，do while，for in

## 关键字

- break
    + 终止循环

- continue
    + 跳出当次循环，继续下一次

- return
    + 函数返回值
    + 注意：如果不在函数内，千万不要使用return

- arguments
    + 一个伪数组对象
    + 该对象中以下标的方式存储了函数调用时传递进行的实参
    + 该对象还有一个length属性用来获知实参个数
    + 使用场景：对于参数不定的情况可以使用arguments

- throw
    + 作用：抛出自定义错误，可以在必要的时候中断程序执行

- try,catch
    + 作用：捕获错误，然后解决，可以防止程序的报错中断

# 类型相等比较
> 约定：空数据类型表示null和undefined两种数据类型。

- 任何数据和NaN相比结果都为false
- null等于undefined
- null和非空类型相比结果为false
- undefined和非空类型相比结果为false
- 数字和非空类型比较，先转换为数字再比较
- 布尔和非空类型比较，先转换为数字再比较
- 对象与对象比较内存地址
- 对象与字符串，对象先转换为字符串再比较

类型 | 类型 | 规律
---|---|---
NaN | 任意类型 | false
null | undefined | true
null | 非空类型 | false
undefined | 非空类型 | false
数字 | 非空类型 | 转换为数字再比较
布尔 | 非空类型 | 转换为数字再比较
对象 | 对象 | 内存地址比较
对象 | 字符串 | 转换为字符串再比较


## 概念

#### 对象
- 任何事物都可以看作是对象。

#### 面向对象与面向过程的概念
- 面向过程
    + 凡是自己亲力亲为，自己按部就班的解决现有问题。
- 面向对象
    + 自己充当一个指挥者的角色，指挥更加专业的对象帮我解决问题。
- 联系
    + 面向对象仍然离不开面向过程，可以认为它是对面向过程更高一层的封装。

## 创建对象的方式

#### 字面量形式
```javascript
var p = {};
p.name = '中国人';
p.age = '500';
```

#### 构造函数形式 ==> 复用性更强
```javascript
function Person(name, age) {
	this.name = name;
	this.age = age;
}
var p = new Person('中国人', 500);
var p2 = new Person('中国人2', 500);
```

## 构造函数

#### 概念
- 如果一个函数配合new关键字创建对象，那么这个函数也叫构造函数
    + 构造函数与普通函数本质上是一样的
    + 编写构造函数时，首字母通常会大写，但不是必须的(类似变量驼峰命名法)

#### 返回值特点
- 如果构造函数没有return语句，那么new它，得到一个新实例
- 如果构造函数return了一些基本类型数据，那么new它，得到一个新实例
- 如果构造函数return了一个对象，那么new它，得到return的对象

## 类与实例的概念

#### 类
- 类是对一些具有相同特征与特性事物的抽象描述
    + 比如动物类的定义是比较抽象的，它抽取了动物与动物之间的相同特征。
    + 同样植物类、哺乳动物类、人类的定义也都是比较抽象的，也是提取他们的共同特征而形成的定义，这就是类。
    + 在js中，可以把构造函数看作是类

#### 实例
- 实实在在的具体事物就是某个类的实例。
    + 比如我家的旺财，是狗类的实例
    + 我的弟弟妹妹，是人类的实例
    + 在js中，通过构造函数创建的对象就是实例

#### 联系
- 如果把类看作是模子，实例则是模子印出来的东西。

#### 对象类型
- 对象的类型就是其构造函数的名字
    + 比如数组是Array类型的对象，日期是Date类型的对象
    + Array和Date就是其构造函数的名字
    + 那么通过Person创建一个实例，那么这个实例就是Person类型的对象。

## 原型
- 原型是一个对象，它的属性可以供其他对象共享
    + js中有很多原型对象，基本每个对象都有属于自己的原型
    + 原型对象的存在可以大大的节省内存开销

#### 原型的使用
- 每个构造函数都有一个prototype属性，可以给其赋值
- 然后通过构造函数创建的实例就可以共享其属性与方法

## 面向对象与面向过程优缺点

#### 面向对象
+ 缺点
    - 通常比面向过程消耗内存，因为有很多实例要存储
    - 前期开发比较缓慢，但是复用性强，后期开发与维护进度会逐渐加快
+ 优点
    - 变量的管理比较清晰，可读性较高
    - 因为代码与对象间的职责比较清晰，所以后期可维护性和可扩展性也比较高
    - 复用性更强

#### 面向过程
+ 缺点
    - 变量混乱，可读性较差
    - 通常有新需求出现，代码改动比较大，所以可维护性和可扩展性比较差
+ 优点
    - 开发迅速，只要能解决当前问题即可

## 面向对象3大特征
- 封装性
    + 对象可以把很多属性与方法集中在一起管理，就是js的封装性。
- 继承性
    + 对象可以使用其原型对象的属性与方法，就是js的继承性。
- 多态性
    + js没有多态。如果非要说，那么对象形态、继承关系可以随时被改变，可以认为是js的多态性。

## 面向对象的书写过程
- 根据需求提取解决该问题所需的对象
    + 比如我要逛街，需要一个导购，需要一个保镖，需要一个女朋友
- 编写每一个对象所对应的构造函数
    + 构造函数可以重复性创建实例，因为我可能需要多个保镖
    + function Person() {}
- 抽取对象所需的属性
    + 就是该对象应该拥有的特征，比如人有名称、年龄、性别、四肢、双眼。
    + function Person(name) { this.name = name; }
- 抽取对象所需的方法
    + 就是该对象应该拥有的特性，比如人会学习创造，狗会看门逗你笑
    + Person.prototype.study = function(){};
- 根据写好的构造函数创建实例，调用属性方法解决实际需求
    + 就是调度实例干事
    + var p = new Person(); p.study();

## 原型其他

#### 谁有prototype与__proto__
- 每个函数都有prototype属性
- 每个对象都有__proto__属性
- 函数比较特殊，即是函数又是对象，所以prototype与__proto__都有

#### prototype与__proto__联系
- 通过构造函数创建的实例
- 当前构造函数的prototype属性指向谁，实例的__proto__属性就指向谁

#### 如何得到一个对象继承的原型
- 通过__proto__属性（但是它是非标准属性，不建议开发中使用）
- 通过constructor属性得到对象的构造函数，再访问其prototype得到原型

#### 创建对象时内在的4个步骤
- 创建一个新实例(本质上就是开辟了一块内存空间)
- 设置新对象的原型
    + 给新实例设置__proto__属性值
    + 这个值与构造函数的prototype属性有关
    + 赋值过程相当于这样：新实例.__proto__ = 构造函数.prototype
- 执行构造函数，执行时设置其this指向新实例
- 返回新实例的地址

#### 对象的属性访问规则
- 优先从自身查找
- 找不到就去原型找
- 还找不到继续去原型的原型找
- 直到终点，终点也没有返回undefined

#### 对象的属性赋值
- 给一个对象的属性赋值
- 如果之前没有该属性那么就是新增，有就是修改
- 对象的属性赋值只影响自己，不会对其他对象和原型对象造成影响

## 原型常见书写方式

#### 1、默认原型
```javascript
function P() {}
P.prototype.fun = function(){};
var p = new P();
```

#### 2、置换原型
```javascript
function P() {}
P.prototype = {
	constructor: P,
	fun: function(){}
};
var p = new P();
```

#### 3、extend复制扩展
```javascript
function P() {}
extend(P.prototype, {}, {
	fun: function(){}
}, {
	fun2: function(){}
});
var p = new P();
```

#### 4、Object.create
```javascript
var proObj = {
	fun: function(){}
};
var p = Object.create(proObj);
```

#### 实现属性复制函数封装
```javascrpt
function extend() {
	var target = arguments[0];
	for(var i = 1, len = arguments.length; i < len; i++) {
		for(var key in arguments[i]) {
			target[key] = arguments[i][key];
		}
	}
	return target;
}
```

#### 类成员与实例成员
- 类成员(静态成员)
    + 添加给类自己的属性与方法
- 实例成员
    + 添加给实例自己的属性与方法
    + 原型上供实例使用的属性与方法

## 原型链

#### 概念
- 一个对象继承的所有由__proto__属性串联在一起的对象，称为该对象的原型链。

#### 对象原型链的研究方案
- 先通过__proto__得到对象的原型
- 然后访问这个原型的constructor属性，确定该原型的身份
- 然后继续按照上诉两个步骤，往上研究原型，最终就得到了对象的原型链。

#### 规律与常见对象原型链结构
- 原型链的终点统一是Object.prototype
- 对象的原型和该对象的类型有关
    + 比如Person的实例，原型是Person.prototype
    + 比如Animal的实例，原型是Animal.prototype
    - []的原型链结构
        + [] ==> Array.prototype ==> Object.prototype ==> null
    - {}的原型链结构
        + {} ==> Object.prototype ==> null
    - /abc/的原型链结构
        + /abc/ ==> RegExp.prototype ==> Object.prototype ==> null
    - Person的原型链结构
        + Person ==> Function.prototype ==> Object.prototype ==> null
    - Function的原型链结构
        + Function ==> Function.prototype ==> Object.prototype ==> null
    - Object的原型链结构
       + Object ==> Function.prototype ==> Object.prototype ==> null
- 构造函数默认的prototype，它统一都继承Object.prototype
    + 比如Person.prototype，原型是Object.prototype
    + 比如Animal.prototype，原型是Object.prototype
- 通过这个规则，可以自由猜想出任意一个实例所有的原型
    + 比如Book的实例，其原型结构为： Book实例 ==> Book.protoype ==> Object.prototype ==> null

## 运算符与方法

#### in -- 运算符
- 作用：判断能否使用某个属性（包含继承的属性）
- 语法：属性名 in 对象
- 返回值：boolean

#### hasOwnProperty -- 方法
- 作用：判断一个属性是不是自己的（不包含继承的属性）
- 语法：对象.hasOwnProperty(属性名)
- 返回值：boolean

#### 关于for in遍历的补充
- for in可以遍历对象继承的属性，不过一些内置的属性是不可遍历的。

#### delete -- 运算符
- 作用：删除对象的属性
- 语法：delete 对象.属性名 || delete 对象[属性名]
- 返回值：boolean

#### instanceof -- 运算符
- 作用：判断一个对象的原型链中是否含有某个构造函数的prototype
- 语法：对象 instanceof 构造函数
- 返回值：boolean

#### Function -- 内置构造函数
- 作用：创建函数实例
- 语法：new Function(形参1，形参2，...，代码体)
- 返回值：新创建的函数实例
- 特点：能够把字符串当做js脚本执行

#### eval -- 内置的全局函数
- 作用：执行字符串代码
- 语法：eval(字符串代码)

## 函数四种调用模式
> 谨记：函数调用时，内部的this的值和这个函数定义无关，和运行(调用)有关。

### 1、函数调用模式 ==> 函数名()
这种方式调用，函数运行时内部的this指向全局对象window。

### 2、方法调用模式 ==> 对象.函数名()
这种方式调用，函数运行时内部的this指向调用该函数的对象。
(dom中事件绑定的函数，就是这种调用方式，所以this指向对应的dom对象)

### 3、构造函数调用模式 ==> new 构造函数()
这种方式调用，函数运行时内部的this指向新创建的实例对象。

### 4、上下文调用模式(间接调用模式) 
1. 函数名.call(this, arg1, arg2);
2. 函数名.apply(this, [arg1, arg2]);
这种方式调用，函数运行时内部的this指向call或apply传入的第一个参数；
如果没有传第一个参数，或者第一个参数为null、undefined，那么this统一指向window。

### call和apply
> 函数调用call和apply，实际上是间接调用自己;
例如fn.call()，表面上看是调用call方法，
实际上连fn自己也被调用了，和fn()直接调用的区别是，this变了。
- 都来自Function.prototype，所以所有的函数都可以使用。
- 相同之处是都可以改变函数this的指向
- 不同之处是传参的方式

### call和apply方法借用的原理
- 如果一个方法内部操作的是this，那么我们就可以通过call或apply指定该方法this，
this改变成谁，那么该方法最终操作的就是谁。
- 如果一个方法内部没有操作this，那么是无法借用的。

### apply的技巧
- apply可以把真数组或者伪数组平铺，然后传递给函数。
- 利用这个特征，可以很方便的对数组或伪数组进行传递操作。

### call和apply使用技巧

1. toString使用
var dateType = Object.prototype.toString.call(date).slice(8, -1);
var dateType = ({}).toString.call(date).slice(8, -1);  // 等价于上面

2. 借用数组的push方法，来操作arguments(arguments不能直接使用数组的方法)
Array.prototype.push.call(arguments, 1);
[].pop.call(arguments);

3. 通过伪数组获取一个真数据(获取后，伪数组不会被改变。本质上，是把伪数组中的数据存到一个真数组里面了)
var argArr = [].slice.call(arguments);

4. 属性继承(借用父类构造函数，来给子类的实例添加属性，相当于复用了父类中的代码)
```
// 人类
function Person(name, age) {
    this.name = name;
    this.age = age;
}
// 学生类
function Student(name, age) {
    // 因为所有的学生，都是人类，所以人类的属性学生一定有，
    // 为了代码复用，所以有如下代码
    //Person.call(this, name, age);  
    Person.apply(this, arguments);  // 上下两种方式等价
}
var stud = new Student();
```

## 作用域

#### 概念
- 变量的有效范围。

#### 全局变量
- 在全局都有效的变量。
- 定义方式：函数外定义。
- 生命周期：从定义开始，到页面被卸载结束。

#### 局部变量
- 只在局部有效的变量。
- 定义方式：函数内定义。
- 生命周期：一般情况下，是从定义开始，到函数执行完毕结束。

#### 函数作用域
- 只有函数才可以产生新的作用域
- 只有函数可以限定变量的有效范围

#### 块级作用域 ==> js没有
- 凡是代码块就可以产生新的作用域
- 凡是代码块就可以限定变量的有效范围

#### 词法作用域(静态作用域) 
- 说的是变量的查找规则，特点是变量查找与函数定义有关，与调用无关
    + 先在当前作用域查找
    + 找不到就去定义该函数的作用域找
    + 一直找到全局作用域为止，全局也没有则报错

#### 作用域的产生
- 函数可以被多次重复调用，调用一次就会产生一个新的作用域。

#### 作用域链
- 函数在定义的时候，将来它执行时的上级作用域就被确定好了，上级作用域可能还有上级，函数所有的上级作用域称之为作用域链。
- 一个函数作用域可以访问的所有上级作用域，称为它的作用域链。

#### 垃圾回收机制原则
- 一个对象没有被其他变量或者属性引用，那么就会被释放。
    + 同时还要保证该对象能够被使用，对于那些无法使用，又存在循环引用的对象，也会被释放。
- 一个局部变量没有被其他函数引用，那么就会被释放。

#### 注意：有一个容易搞混，又没有什么联系的知识点，这里强调一下
- 函数内的this，与函数的定义无关，与调用有关。
```javascript
var obj = {
	fn: function() { console.log(this) };
};
var fn = obj.fn;

// 同一个fn，三种调用方式，this分别不同
obj.fn(); // obj
fn();     // window
new fn(); // fn实例
```
- 变量的查找，与函数的定义有关，与调用无关。
```javascript
function fn() {
	console.log(a); // 报错，自己找不到，去定义fn的全局找，所以这里和fn的定义有关，与fn的调用无关。
}
(function() {
	var a = 10;
	fn();
})();
```

## 闭包

#### 概念
- 在js中访问了自由变量的函数就是闭包

#### 自由变量
- 函数可访问的外部局部变量，称之为该函数的自由变量

#### 特点
- 闭包的自由变量生命周期会被拉长，与闭包的生命周期进行了捆绑

#### 计数器案例
```javascript
function getCounter() {
    var total = 0;
    return {
        add: function() {
            total++;
        },
        get: function() {
            return total;
        }
    };
};
var counter = getCounter();
counter.add();
counter.get();
var counter2 = getCounter();
counter2.add();
counter2.get();
```

#### 缓存操作
```javascript
var cache = (function() {
    var cache = {};
    return {
        set: function(key, val) {
            cache[key] = val;
        },
        get: function(key) {
            return cache[key];
        }
    };
}());
cache.set('张锐', '中国人');
cache.get('张锐');
```

#### for循环i面试题
```javascript
var arr = ['第一句话', '第二句话', '第三句话'];
for(var i = 0, len = arr.length; i < len; i++) {
    setTimeout(function(i) {
        return function() {
            console.log(arr[i]);
        }
    }(i), 1000 * i + 1000);
}
```

## 预解析
- 可以理解为js解析引擎在逐行执行代码前，对一些特殊代码的预先执行。
- 预解析过后代码才会从上到下逐行执行，但是预解析时已经定义的变量与函数，是不会重复定义的。
- 预解析的本质就是变量对象初始化。

#### 预解析做了两件事情
+ 1、变量声明提升：检测到变量声明那就率先进行声明
+ 2、函数声明提升：检测到函数声明也率先进行声明

#### 变量声明
- 使用通过var定义的变量，才属于变量声明
    + 例如：var a; 属于变量声明。
    + 例如：b = 10; 不属于变量声明。
- var关键字可以通过逗号连续声明多个变量
    + 例如：var a, b, c = 20, d = 30; 
    + a,b,c,d全部属于声明。
- var关键字在声明变量的时候，可以给其赋值，如果赋值表达式中含有一些变量，这些变量不属于变量声明。
    + 例如：var a = b = 10; 
    + 其中a属于变量声明，b不属于。

#### 函数声明
- 在js中，函数声明式写法比较单一，好区分。
    + 要么定义在全局
    + 要么定义在另一个函数主体内

#### 预解析的特点
- 在变量声明之前访问它不会报错
- 在函数声明之前调用它不会报错

#### 预解析相关细节
- js预解析分全局预解析与局部预解析，区别在于局部预解析在函数调用时发生。
- 变量声明重名 -- 最终只留一个
```javascript
	console.log(a); // 预解析后值保留一个变量a，值为undefined
	var a = 1;
	var a = 2;
```
- 函数声明重名 -- 保留后面的函数
```javascript
	console.log(test); // 预解析后test为打印2的函数
	function test(){ console.log(1) }
	function test(){ console.log(2) }
```
- 变量与函数重名 -- 保留函数
```javascript
	console.log(test); // 预解析后test值为函数
	var test = 10;
	function test(){}
	var test = 20;
```

#### 函数执行时形参会优先执行
- 形参定义与赋值优先于变量与函数声明。
```javascript
(function(a) {
	console.log(a);  // a函数
	var a = 200;
	function a(){}
	console.log(a);  // 200
}(100));
```

#### 函数表达式的名称
```javascript
	// 函数fnName的名字在外面无法访问，但是可以在函数内访问，
	// 相当于自己的一个局部变量，值为自己的引用。
	var fn = function fnName(){
		console.log(fnName);  // 里面可以访问
	};
	console.log(fnName);   // 外面访问报错
```

## 函数的四种调用模式

#### this的特点
- 函数中的this，调用方式不同，指向不同
- this与调用有关，与定义无关

#### 函数调用模式
- 函数名() || (function(){}()) ==> window

#### 方法调用模式
- 对象.方法名() || 对象[方法名]() || 祖对象.父对象.子对象.方法名() ==> 宿主对象

#### 构造器调用模式
- new 构造函数() || new 对象.构造函数() ==> new出来的新实例

#### 间接调用模式(上下文调用模式)
- call
    + 函数.call(指定的this，实参1，实参2，...)
    + 对象.方法.call(指定的this，实参1，实参2，...)
- apply
    + 函数.apply(指定的this，[实参1，实参2，...])
    + 函数.apply(指定的this，{0: 实参1， 1：实参2， length: 2})
    + 对象.方法.apply(指定的this，[实参1，实参2，...])
    
#### call和apply的使用范例
```javascript
// 方法借用 -- 给伪数组对象添加属性值
var obj = {};
Array.protype.push.call(obj, '要添加的第一个值', '要添加的第二个值')
```
```javascript
// 方法借用 -- 获取对象类型
var arr = [];
Object.prototype.toString.call(new Date).slice(8, -1)
```
```javascript
// 方法借用 -- 借用父类构造函数给子类实例添加属性
function Parent(name, age) {
	this.name = name;
	this.age = age;
}
function Son() {
	Parent.apply(this, arguments);
}
var p = new Son('火星人', 999);
```
```javascript
// apply拆分数组或伪数组值依次传递给函数
var arr = [1, 10, 20, 40];
Math.max.apply(null, arr)
```

## ES5数组新增的3个方法

#### forEach
- 作用：帮我们遍历数组，每遍历到一个值，就会调用一次回调，把这个值与它的下标传递过去
- 语法：数组.forEach(function(v, i){ console.log('使用forEach帮我们遍历好的值与下标') })
- 返回值：undefined

#### map 
- 作用：可以用来代替forEach，但是map可以接收回调的返回值，最终通过一组数据映射为回调返回的另外一组数据
- 语法：var mapArr = 数组.map(function(v, i){ return v * v })
- 返回值：回调所有的返回值组成的新数组

#### filter
- 作用：可以用来代替forEach，但是还可以过滤数组中的值
- 语法：var filterArr = 数组.filter(function(v, i){ if(v % 2 ==0){ return true; } })
- 返回值：所有返回回调返回true的对应值组成的新数组

## call&apply的补充
- 如果不传参 ==> this指向window
- 传null ==> this指向window
- 传undefined ==> this指向window
- 传123 ==> this指向123的包装类型对象(Number对象)
- 传'abc' ==> this指向'abc'的包装类型对象(String对象)
- 传true ==> this指向true的包装类型对象(Boolean对象)
- 传对象 ==> this指向传入的对象

## 严格模式
- ES5新增的一个特性，使用该特性可以让js以一种新的模式运行js脚本。
- 该模式下可以强制我们抛弃那些不推荐不友好的写法
- 该模式下可以让js之前的一些设计不太合理的api表现的合理一些
- 该模式下可以让js拥有一些新的特性，比如ES6/ES7规范中定义的某些语法，必须在严格模式下才有效

#### 严格模式的分类
- 全局模式
    + 在全局代码的最上面书写一句话'use strict';
    + 使用该模式，所有的代码都按照严格模式执行
- 局部模式
    + 在函数内部的最上面书写一句话'use strict';
    + 使用该模式，只有该函数内的代码才会按照严格模式执行

#### 需要记住的几条严格模式规则
- 定义变量必须使用var
- 函数调用模式this为undefined
- 真正实现了call谁this就为谁

#### 其他
- 不能使用with语句
- 废除函数.caller与arguments.callee
- eval拥有了单独的作用域
- ......