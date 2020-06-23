---
title: summary
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:12:20
tags: [javascript,js经验总结]
---

![image](null-18cd3a529784b774.jpg)

<!--more-->

原始值存在栈内存里的，原始值是不可以有属性和方法的
	
1.原始值   栈stark
2.引用值   堆heap


> 包装类  (在另一片文章有详细的案例encapsulation)
```bash
	var a = 'abc';
	var num = new Number(123)
	num.abc = 'abc';
	var num1 = 123
	num1.abc = 'abc'
```

```bash
原型
	Person.prototype.lastName = 'li';
	function Person(){
		var this={
		
		_proto_:Person.prototype   //没有就向父级 的原型上去找
		}
		
	}
person = new Person();

```


```bash
var demo = {
		lastName :"den"
	}
	var obj = Object.create(demo) // 是创建对象的，必须填，对象必须有原型，所以object。creat创建出来必须指定
	obj = {
		__proto__:demo
	}

```



> 一旦经历了var的操作，所得出的属性，window，这种属性叫做不可配置属性，
> 不可配置的属性 delect不掉
```	bash
函数对象借用
//	function person(name,age){
//		this.name = name;
//		this.age= age
//	}
//	function student(name,age,sex){
		//var this = Object.creat(student.prototype)
//		person.call(this,name,age)
//		this.sex = sex
//	}
//	
//	var stuDent = new student('sun',18,'male')
```

```bash
闭包的知识点
	var li = document.getElementsByTagName('li');
	for(var i=0;i<li.length;i++){
	(function(i){
		li[i].addEventListener('click',function(){
			console.log(i);
		},false)
		
	}(i))
	}
```

> 两个对象的copy
> 
```bash
 var  inherit = (function(){
 	var F = function(){}
 	
 	return  function(Target,Origin){   //
 		F.prototype = Origin.prototype;
 		Target.prototype = new F();
 		Target.prototype.constructor = Target;
 	}	
 })



 function inherit(target,origin){
//	function F(){};
//	F.prototype = origin.prototype;
//	target.prototype = new F();
//	target.prototype.constructor = target;
//	target.prototype.uber = origin.prototype;
//}



事例:

Father.prototype.lastName = 'haha'
function Father(){
	var f = (function(){})
	
	return f
}
function Son(){
	
}
inherit(Son,Father) // 为什么非要函数先执行呢
var son = new Son()
var father = new Father()
```


> 2014阿里巴巴题
```bash
var a = 1;
var fn = function(){}
fn.c = 4
function test(x,y){
	x = 4;
	y.c = 6
	return y;
}
var b = test(a,fn)
alert(a+fn.c)
alert(b)
```


* 预编译，构建AO，在函数执行前
* 1.找变量声明赋值为undefined
* 2.找变量声明
* 3.形参实参相统一
* 4.找函数声明，函数名为变量值

* 值类型
* 不可变的原始值（栈数据）
* number、string、boolean、undefined、null
* 引用值（堆数据）
* array、object、function


> 传值与传址
```	bash
    var a = [1,2,3,4,5];;
    var b = a;
    var c = a[0];
    alert(b);//1,2,3,4,5
    alert(c);//1
      //改变数值        
    b[4] = 6;
    alert(b)
    alert(a)
    c = 7;
    alert(a)

```

> 浅拷贝

```bash

var a = {
        key1:"11111"
   }
    function Copy(p) {
        var c = {};
        for (var i in p) { 
    　　                       c[i] = p[i];
        }
        return c;
 　　}


 //实例     
   a.key2 = ['小辉','小辉'];
   var b = Copy(a);
 　　   b.key3 = [1,2,3];
 
   alert(b.key1);     //1111111
   alert(b.key3);    //33333
   alert(a.key3);    //undefined
   
   b.key2.push('大辉')
   alert(a.key2)

```

> 深入拷贝

```bash
　　function Copy(p, c) {
          var c = c || {};
          var target = target ||{},   //判断传入的值是不是有
	          toStr = Object.prototype.toString, //用来判断是不是对象object
	          arrStr = '[object Array]';
          for (var i in p) {
         　  　if (p[i]!=='null'&& typeof p[i] === 'object') {
          　　　　　c[i] = (p[i].constructor === Array) ? [] : {}; //
         　　　　　Copy(p[i], c[i]);
          　　} else {
         　　　　　c[i] = p[i];
          　　}
         }
         return c;
   　　  }  

//实例  
   a.key2 = ['小辉','小辉'];
   var b={};
   b = Copy(a,b);        
   b.key2.push("大辉");
   alert(b.key2);    //小辉，小辉，大辉
   alert(a.key2);    //小辉，小辉

```

```
JSON=>obj  toString
obj=>json  JSON.parseiyf
```


```
function outer(){
	inner()
}
function inner(){
	alert(arguments.callee.caller) // outer()
}
outer()

```