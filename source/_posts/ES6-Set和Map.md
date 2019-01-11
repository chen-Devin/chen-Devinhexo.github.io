---
title: ES6-Set和Map
date: 2018-12-10 14:51:42
tags: es6
---
## ES6   Set 和 Map 数据结构 ##

### Set ###

ES6提供了新的数据结构Set。类似于数组，只不过其成员都是唯一的，没有重复的值；  （set本身是一个构造函数，用来生成Set数据结构。）

     ```
          var s = new Set();
  
          //通过add方法向Set结构中加入成员
          [2,3,5,4,5,2,2].map(x => s.add(x));
 
          for (i of s){ console.log(i)}
          // 2 3 4 5 （表明set结构不会添加重复的值）
     ```

<!-- more -->

 Set结构接收一个数组作为参数 ，用来初始化。
      
      ```
          var items = new Set([1, 2, 3, 4, 5, 5, 5]) ;

          items.size
          //5
      ```

 注意：向Set加入值的时候。不会发生类型转换。 这意味着，在Set中 5 和 "5" 是不同的值；

 
**Set结构有以下属性：**
  
1. Set.prototype.constructor :构造函数，默认就是Set函数。
2. set.prototype.size ： 返回Set的成员总数。

**Set结构有以下方法**  
- add（value) ：添加某个值。   
- delete（value) :删除某个值。  
- has（value) ： 返回以一个布尔值，表示该值是否为Set的成员。  
- clear（value) ：清除所有成员。  
 
    ```
        s.add(1).add(2).add(2); //注意‘2’被加入了两次
        s.size  //2  
    
        s.has(1) //true
        s.has(2) //true
        s.has(3) //false
     
        s.delete(2);
        s.has(2) //false

    ```

下面对比以下，看看在判断是否包括一个键上面，对象个Set的写法有哪些不同。

   ```
        //对象写法
        var properties = {
          "width": 1,
          "height": 1
        };

         if ( properties[someName]) {
           // do something
         }

        /****************************************/

         // Set的写法
         var properties = new Set();

         properties.add('width');
         peoperties.add('height');

         if ( properties.has(someName) ) {
           // do something
         }
     ```

**注意** ：Array.from方法可以将Set结构转换为数组。
    
     ```
         var items = new Set([1,2,3,4,5]);
         var array = Array.from(items);

     ```
  这也提供了一组数组中重复元素的方法;  

     ```
         function dedupe(array) {
           return Array.from( new Set(array) );
         }
     ```


### Map ###
 
 js对象本质上是键值对的集合。但是只能使用字符串充当键。这在一定程度上给我们的使用带来了很大的限制。

   ```   
       var data = {};
       var element = document.getElementById('myDiv');

       //将DOM节点 (即element）当做对象data的键
       // 但是对象只接受字符串作为键名，所以element被自动转换为字符串 '[Object HTMLDivElement]'
       data[element] = metadata;
   ```

而ES6正是为了解决这个问题才提供的Map结构。它类似于对象，也是键值对集合，但是键的范围不不限于字符串，对象也可以当做键。
 
   ```
       var m = new Map();
       o = {p: "hello world"};

       m.set(o,'content');
       console.log( m.get(o) ); //content
   ```
  set 和 get 是对象的方法 不要和Set数据结构混淆; 在上面的代码中，将对象o当做是m的一个键；

  Map函数可接收一个数组进行初始化。

   ```
       var map = new Map([["name", "小明"], ["title", "Author"]]);

       map.size //2
       map.has('name') //true
       map.get('name') //小明
       map.has("title"); //true
       map.get("title"); //Author
   ```

**注意：只有针对同一对象的引用，Map结构才将其视作同一个键。这一点要谨慎**
  
    ```
        var map = new Map();
   
        map.set(['a'],555);
        map.get(['a']); //undefined
    ```

上面代码中set 和get 方法表面上是针对同一个键，但实际上这是两个值，内存地址是不一样的，因为get方法无法读取该键，返回undefined。

再看看下面一段代码：
  
    ```
         var map = new Map();
 
         var k1 = ['a'];
         var k2 = ['a'];

         map.set(k1, 111);
         map.set(k2, 222);

         map.get( k1 );  //111
         map.get( k2 );  //222

    ```
上面代码，变量k1和K2的值是一样的，但是他们在Map机构中被视为两个键，即同样值的两个实例，在Map中视为两个键。

**Map的属性和方法**
- size：返回成员总数。
- set（key，value）：设置一个键值对。
- get（key）：读取一个键。
- has（key）：返回一个布尔值，表示某个键是否在Map结构中。
- delete（key）：删除某个键。
- clear()：清楚所有成员。
   
    ```
        var m = new Map();
    
        m.set("edition", 6); // 键是字符串
        m.set(262, "standard"); // 键是数字
        m.set(undefined, "nah"); //键是undefined

        var hello = function() {
          console.log("hello");
        }
        m.set(hello, "Hello ES6!");  //键是函数 

        m.has("edition");  //true
        m.has("years");  //false
        m.has(262);  //true
	    m.has(undefined);  //true
	    m.has(hello);  //true
 
        m.delete( undefined );  
	    m.has( undefined );  //false

	    m.get( hello );  //hello ES6!
	    m.get("edition");  //6
   
    ```

 **遍历**   
Map原生提供三个遍历器。

1. key() : 返回键名的遍历器。
1. values() : 返回键值的遍历器。
1. entries() : 返回所有成员的遍历器。

     ```   
         for( let key of map.key() ) {
          console.log("key: %s", key);
          }

         for ( let value of map.value() ) {
          console.log("value: %s", value);
         } 

         for ( let item of map.entries() ) {
          console.log("Key: %s, Value: %s", item[0], item[1]);
         } 

           // same as using map.entries()
          for (let item of map) {
           console.log("Key: %s, Value: %s", item[0], item[1]);
          }
      ```

另外，Map还有一个forEach方法，与数组中的forEach方法类似，也可以实现遍历。 

     ```  
        var reporter = {
        report: function(key, value) {
         console.log("key: %s, Value: %s", key, value);
         }
        };

        map.forEach(function(value, key, map) {
          this.report(key, value)
         }, reporter);
     ```

 上面代码中，forEach()方法的回调函数中的this, 就指向reporter。


   转载处：https://blog.csdn.net/u014695532/article/details/51815017 

   
