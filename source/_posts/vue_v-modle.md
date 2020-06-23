---
title: vue双向绑定原理
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:14:38
tags: [vue,v-model,双向绑定原理]
anout: xxxxx
---

![imge-text](bg.jpg)


<!--more-->


```shell
	var keyvalue = 1;
	var obj = {}
	//vue 双向绑定的原理  它接收三个参数，要操作的对象，要定义或修改的对象属性名，属性描述符。重点就是最后的属性描述符。
	Object.defineProperty(obj,'key',{
		enumerable: true,
        configurable: true,
		get :function(){
			return keyvalue
		},
		
		set:function(data){
			//当设置obj的值时，就会触发这个函数
			keyvalue = data
			console.log('keyvalue的值已经发生变化了'+keyvalue)
		}
		
	})
	//console.log(obj,key)
	
```

> 面试题



**1. vue-loader是什么？使用它的用途有哪些？**
```
是webpack的一个loader，使用脚手架他会自动安装这个模块，也可以npm -install 。是用来处理.vue文件的

```

**2. v-show和v-if指令的共同点和不同点?**

```
他们都可以配合css完成动画效果。不同点：v-show只是简单的使用display的显示与隐藏，元素会一直留在DOM中，
而v-if渲染的元素，当为true元素创建，false元素销毁，变成一组html注释

```
**3. 如何让CSS只在当前组件中起作用?**
```
如果是css的作用域的话，那就是 在style标签后面加上 scoped关键字

```
**4. 请简述vue的生命周期有哪些以及你对vue生命周期的理解？**
```
> beforeCreate 与 created

beforeCrete：这是实例将要被创建的状态，类似于  var a；但是没有赋值，是存在的
             这个beforeCreate 可以用来做ajax请求，提前去后台拿到数据
created：这是已经被创建好的状态，crete 里面是可以访问到当前实例的任何成员
          可以初始化一些数据（检测数据或者初始化数据）

> beforeMount 与 mounted

beforeMount：开始挂在元素，挂载虚拟DOM之前，在这里获取到的还是一个id为app的元素，但是获取不到组建的元素
mounted:元素挂在之后，app元素已经被组建给替换掉了

> beforeUpdate  与 updated

beforeUpdate：只有在你改变那个数据 并且和模板有关系，才回发生变化 ，模板更新之前
updated： 模板更新之后他们两个是同步变化的，可以用来获取更新之前和更新之后dom的东西

> beforeDestroy 与 destroyed
beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。该钩子在服务器端渲染期间不被调用。
               实例销毁后是不能够调用的
destroyed：vue实例销毁之后调用，所有事件也会被销毁

> actived 与 deactived
actived：keep-alive 组件激活时调用。
deactived：keep-alive 组件停用时调用。

```

**5. 请简述Vue的双向数据绑定原理是什么？**
```
利用了 Object.defineProperty() 这个方法重新定义了对象获取属性值(get)和设置属性值(set)的操作来实现的。
var keyvalue = 1;
	var obj = {}
	//vue 双向绑定的原理  它接收三个参数，要操作的对象，要定义或修改的对象属性名，属性描述符。重点就是最后的属性描述符。
	Object.defineProperty(obj,'key',{
		enumerable: true,
        configurable: true,
		get :function(){
			return keyvalue
		},
		
		set:function(data){
			//当设置obj的值时，就会触发这个函数
			keyvalue = data
			console.log('keyvalue的值已经发生变化了'+keyvalue)
	}
		
})



```

**6. 请简述mvvm框架是什么？它和其它框架（jquery）的区别是什么？哪些场景适合？**
```
mvvm:就是 m：model v：view vm：viewmodel
MVVM在概念上是真正将页面与数据逻辑分离的模式，它把数据绑定工作放到一个JS里去实现，而这个JS文件的主要功能是完成数据的绑定，即把model绑定到UI的元素上

jquery框架值封装了js，并且集成了许多的方法供使用者调用，采用链式语法，当时会频繁的操作DOM节点，
而MVVM是用数据驱动的，即数据改变DOM改变，减少对DOM的修改

MVVM适用于许多场景，比如：购物网站许多的dom节点
```
**8. 在Vue中如何使用插件例如 iview？**
```
如果是外部插件就先npm -install *** 安装插件
再vue.use(***)去注册插件，在导入他的内置css

```

**9. 请简述vuex由哪几个部分组成，他们之间有什么关系？**


```
state：这个是用来定义数据的值 key：value
getters：这里可以订阅，查询state里面值的变化，但是不能去修改它

mutations：这里面试方法，而且有一个state参数，可以获取到state里面的数据，并且可以重新赋值 
actions：这里面试方法，可以执行mutations里面的方法，而且可以一次执行多个mutations里面的方法

vuex的辅助函数 用 import {} form ‘vuex’ 进行导入
mapstate：
mapgetters：
mapmutations：
mapactions：


```
**10. 使用vue开发项目时，如何处理跨域请求？**
```
使用asiox做跨域请求，配置webpack就可以


```

**11. 你所了解的vue的ui框架有哪些，请列出5个以上的ui框架名称？**
```
iview ：
elelemnt ui ：
cube-ui ： 滴滴的移动端框架
mint
vuetify

```
**12. 请简述webpack loader选项的作用是什么？**
```
通过使用不同的loader，webpack通过调用外部的脚本或工具可以对各种各样的格式的文件进行处理，如分析JSON文件并把它转换为JavaScript文件

```

**13. 请简述webpack的作用，以及它是如何工作的？**
```
承担了很多前端代码的自动化生成的工作。搭配很多loader，可以完成不同的事情。
比如说把繁杂的项目中用到的js打包并压缩成你设定的一个或多个文件去发布到生产环境。

依赖管理：方便引用第三方模块、让模块更容易复用、避免全局注入导致的冲突、避免重复加载或加载不需要的模块。

合并代码：把各个分散的模块集中打包成大文件，减少HTTP的请求链接数，配合UglifyJS可以减少、优化代码的体积。

各路插件：babel把ES6+转译成ES5- ，转换less为css

原理：最简单地说，就是分析代码，找到require、exports、define等“关键词”，并替换成对应模块的“引用”

```
**14. vue的事件修饰符的作用是什么,能否自定义修饰符?**
```
vue的事件修饰符是用来处理事件的， 比如：v-on：keyup.enter.37.38.39.40

可以通过全局 config.keyCodes 对象自定义按键修饰符别名
Vue.config.keyCodes.f1 = 112

```

**15. 全局组件和局部组件有何区别，什么情况下使用全局组件和局部组件？**
```
全局组件不需要注册就能够使用，而局部组件需要在APP.vue的 $el中注册才能够使用

我们可以吧html中的各个部分用vue组件来完成，而一个页面就是由一个个小组件组成的，而全局组件就是在
全局中都能够用到，比如：页面的header部分
```
**16. 路由切换时需要动画效果，可使用什么组件完成该动画效果?**
```
使用vue内置的组件：<transition></transition>
enter-active
leave-active


```
**17. 请列出Vue的路由有哪些模式，有什么区别？**
```
 1、hash ——即地址栏URL中的#符号
2. history -- 不会再地址栏url上留下标记

back、forward、go三个方法，对应浏览器的前进，后退，跳转操作

```

**18. `{{message}}` 在插值表达式中，message的值是`“你好vue”`如何过滤掉message里的vue几个字**
```
在computed上写一个方法：
{{ message | capitalize }} 这个capitalize就是方法，可以有多个

filters:{
            capitalize:function(value){
                console.log(value)
                return value.replace(/[\u4e00-\u9fa5]/g,'')
            }
        }



```
**19. 请列出vue中插槽有哪几种。简述它们的作用？**
```

<slot>
定义一个组件，然后在组件中添加一个<slot>插槽，
当其他的组件引入这个插槽组件并注册的组件，就可以在组件中插入元素了

```
**20. Vue.directive() 的作用是什么，用来解决什么问题？**
```
注册或获取全局指令

注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
   当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    聚焦元素
    el.focus()
  }
})

如果想注册局部指令，组件中也接受一个 directives 的选项：
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}

可以自己定义函数，让插入DOM中使用

```