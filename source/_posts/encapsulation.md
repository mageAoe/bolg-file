---
title: encapsulation
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:04:41
tags: [function,封装]
---

![IMAGES TEXT](null5a9746014f80840c.jpg)

<!--more-->

> 获取计算后样式的方法
```bash
	function getStyle(ele,attr){
		return ele.currentStyle? ele.currentStyle[attr]:getComputedStyle(ele)[attr]
	} 
```

> 获取元素
```	shell
	function $( selector,content){
		var firstChar = selector.charAt(0);
		if( firstChar === "#" ){
		return document.getElementById(selector.substring(1));
		}else{
		var c = content || document;
		return c.getElementsByTagName(selector);
	}
	} 

```


> 运动函数  兼容IE6 7 8
> 回调函数 定时器停止后 干的事
```	bash
  function doMove(obj,attr,target,speed,callBack1){
		
		function  getStyle(obj,attr){  //样式的兼容
		
		if(obj.currentStyle){
			return obj.currentStyle[attr];   // []去读取不确定的属性值  变量
		}else{
			return getComputedStyle(obj)[attr];
		}
		
	}
		var cur = parseFloat(getStyle(obj,attr)); //先取的元素身上的
		
		speed = cur<target?speed:-speed  // 判断  如果当前位置《目标位置 ，就为+   否则为  -

		clearInterval(obj.time);  //防止快速点击
		obj.time = setInterval(function(){
		cur +=speed;  
		if(cur>=target && speed >0 ||cur<=target && speed <0){
			clearInterval(obj.time)
			cur=target;
			obj.style[attr] = cur+'px';
			typeof  callBack1 === 'function' && callBack1();
//			typeof  callBack2 === 'function' && callBack2();
//			typeof  callBack3 === 'function' && callBack3();
			
		}else{
			obj.style[attr] = cur+'px';
		}
		
		},30)
		
	}

```


> 抖函数
```bash
function shake(obj,attr){
		var pos=parseInt(getStyle(obj,attr))
			var arr=[];
			for(var i=20;i>0;i-=2){
				arr.push(i,-i)
			}
			var num=-1
			arr.push(0)
			obj.timer=setInterval(function(){
	    	num++
	    	obj.style[attr]=pos+arr[num]+'px';
	    	if(num==arr.length){
	    		clearInterval(obj.timer)
	    	}
    },30)	
	} 

 ```  

> 按照字符长度排
```bash

	function retBytes(str){
		var num = str.length;
		for(var i=0;i<str.length;i++){
			if(str.charCodeAt()>255){
				num++
			}
		}
		return num;
	}

```	

> 我们用的方法都来自于原型链上，模拟系统的方法：push
```bash

	Array.prototype.push = function(target){
		for(var i=0;i<arguments.length;i++){
			this[this.length] = target
		}
		return length;
	}

```	

> 区别包装类new number，普通类string
```bash

function type(target){
	var tar = typeof(target)
	var template = {
		"[object Array]":'array-object',
		"[object Object]":'object-object',
		"[object Boolean]":'boolean-object',
		"[object Number]":'number-object',
		"[object String]":'string-object',
	}
	if(target===null){
		return "null";
	}else if(tar=='object'){
		var str = Object.prototype.toString.call(target);
		return template[str];
	}else{
		return tar;
	}
}

```

> 数组去重
```bash

Array.prototype.unique = function(){
	var temp = {},
	    arr = [],
	    len = this.length;
	   for(var i=0;i<len;i++){
	   	if(!temp[this[i]]){  //如果对象里没有这个属性就为undefined，然后取反
	   		temp[this[i]] ='abc';
	   		arr.push(this[i]);
	   	}
	   }
	   return arr;
}
```

> addEventListener   ie的兼容
```bash

	function addevent(elem,type,handle){
		if(elem.addEventListener){
			elem.addEventListener(type,handle,false)
		}else if(elem.attachEvent){
			elem.attachEvent('on'+type,function(){
				handle.call(elem)
			})
           }else{
           	elem['on'+type]=handle;
           }
		}
```

> 雅虎的继承函数封装方法
```bash

var inherit = (function(){
	var F = function(){}
	return function(target,oringin){
		F.prototype = oringin.prototype;
		target.prototype = new F();
		target.prototype.constructor = target;
		target.prototype.uber = oringin.prototype
	}
}())

```

---
> 作者：scq