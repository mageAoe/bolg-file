---
title: H5C3属性
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:06:55
tags: [H5C3]
---
### HTML5十个新特性

（一）  语义标签

（二）增强型表单

（三）视频和音频

（四）Canvas绘图

（五）SVG绘图

（六）地理定位

（七）拖放API

（八） WebWorker

（九） WebStorage

（十）WebSocket


![images](bg.jpg)

<!--more-->



### （一）  语义标签

### （二）增强型表单/表单2.0

1)新的input type

 2)新的表单元素

```shell
 <input><textarea><select><option>....

 <datalist>：数据列表，为input提供输入建议列表

<progress>：进度条，展示连接/下载进度

<meter>：刻度尺/度量衡，描述数据所处的阶段，红色(危险)=>黄色(警告)=>绿色(优秀)

<output>：输出内容，语义上表示此处的数据是经过计算而输出得到的

```
3)表单元素的新属性

   通用属性：

          placeholder：占位提示文字

          mutiple：是否允许多个输入

          autofocus：自动获得输入焦点

          form：指定输入元素所从属的表单，可以实现输入框放在表单外部并能被提交的效果


验证属性(了解即可)：

          required：输入框内容不能为空

          min：允许输入的数字最小值

           max：允许输入的数字最大值

           minlength：允许输入的字符串最小长度

          maxlength：允许输入的字符串最大长度

           pattern：输入框内容必须符合的正则表达式

### （三）视频和音频

视频播放：

           查看视频的所有属性、方法、事件：console.log(videoBirds);

           音频播放：<audio src=""></audio>

           查看视频的所有属性、方法、事件：console.log(bgMusic);



### （四）Canvas绘图

[canvas笔记](http://note.youdao.com/noteshare?id=925e3d063c42d4be5e9f045955b91096&sub=0743C2D2565841F9B6C34F7C4C59C4DD)

### （五）SVG绘图


Canvas与SVG的不同：

(1)Canvas是位图；SVG是矢量图

(2)Canvas是JS绘图技术(不是DOM元素)；SVG是标签绘图技术(是DOM元素)

(3)Canvas内容不能使用CSS；SVG内容可以使用CSS；

(4) Canvas内容不方便绑定事件处理；SVG内容方便进行事件绑定



> 常用的SVG图形：

```

(1)矩形

<rect width="100" height="50" x="400" y="350" fill="#f0f" fill-opacity="0.3" stroke="#00f" stroke-width="6" stroke-opacity=".3"></rect>

(2)圆形

<circle r="100" cx="400" cy="300" fill="#f0f" fill-opacity="0.4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></circle>

(3)椭圆

<ellipse rx="100" ry="50" cx="400" cy="350" fill="#f0f" fill-opacity=".4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></ellipse>        

(4)直线（没有fill只有stroke）

<line x1="45" y1="350" x2="450" y2="350" stroke="#f00" stroke-width="4px" stroke-opacity=".4"></line>

(5)折线（fill必须设置透明/stroke必须手工指定）

<polyline points="150,200  250,100  350,300  450,50" stroke="#00f" stroke-width="6" stroke-opacity=".4" fill="transparent"></polyline>

(6)多边形

<polygon points="100,150 100,300  400,300  400,150  250,220" fill="#f0f" fill-opacity=".4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></polygon>

(7)文本

<text alignment-baseline="before-edge" font-size="40" fill="#f0f" stroke="#00f">达内科技2018ajgy</text>

(8)图像

<image xlink:href="img/p3.png" x="400" y="200" width="100" height="200"></image>

```

### （六）地理定位 —— 了解

通过浏览器获取当前用户的所在地理坐标，以实现“LBS服务”（Location Based Service），如实时导航、周边推荐。

           情形1：用户使用手机浏览器——可以根据内置GPS芯片读取数据

           情形2：用户使用PC浏览器——可以根据电脑的IP地址进行反向查询(需要很大的IP分配库)

window.navigator.geolocation

### （七）拖放API

H5之前没有拖放API，可以使用“鼠标按下 + 鼠标移动”两个事件来模拟用户拖动事件。

           H5之后专门提供了七个鼠标拖动相关事件句柄：

> 拖动的源对象(source)可能触发的事件：

                    dragstart：拖动开始

                    drag：拖动中

                    dragend：拖动结束

> 拖动的目标对象(target)可能触发的事件：

                    dragenter：拖动进入

                    dragover：拖动悬停

                    drop：松手释放

                    dragleave：拖动离开

           注意：拖放API事件句柄中所有的事件对象都有一个dataTransfer属性（数据运输对象），用于在源对象和目标对象间传递数据。

           源对象：event.dataTransfer.setData(key, value)

           目标对象：var value = event.dataTransfer.getData(key)


### （八） WebWorker

背景：Chrome浏览器中发起资源请求的有6个线程；但是只有1个线程负责渲染页面——称为UI主线程——浏览器中所有的代码只能由一个线程来执行。

问题：若浏览器加载了一个很耗时的JS文件(可能影响DOM树结构)，浏览器必须等待该文件执行完成才会继续执行后续的代码

(HTML/CSS/JS等)——如果一个JS文件要执行10s(可能有很深的循环/递归等科学计算/解密)，会发生什么？——执行耗时JS任务过程

中，会暂停页面中一切内容的渲染以及事件的处理。

解决方案：H5新特性——Web Worker

Worker的本质：就是一个执行指定任务的独立线程；且该线程可以与UI主线程进行消息数据传递。使用方法：

 HTML文件中：

```
var w = new Worker('js/x.js')

w.postMessage('发送给Worker线程的消息');

w.onmessage = function(e){

e.data; //来自Worker线程的消息

  }
```

           JS文件中：

```
onmessage = function(e){

    var data = e.data;  //接收UI线程的消息

    //执行耗时任务....

     postMessage(result);   //给UI线程发送消息

      }
```

注意：Worker任务不允许直接操作DOM树，也不允许使用任何的BOM对象！需要的数据只能由UI主线程来传递，处理的结果也必须交由UI线程来显示。

### （九） WebStorage

(1)服务器端存储

  1.数据库存储，如商品、用户等核心数据

  2.Session/内存存储，如用户的登录信息

(2)客户端存储

   3.Cookie存储，如用户偏好、访问历史，浏览器兼容性好但处理麻烦且容量限制

   4.H5 WebStorage存储，如用户偏好、访问历史等安全要求的数据，老IE不兼容但易使用且容量大

H5WebStorage存储具体涉及到两个对象：

 (1)window.sessionStorage：类数组对象，通过key=>value对存储字符串数据——会话级存储

 (2)window.localStorage：类数组对象，通过key=>value对存储字符串数据——本地/跨会话级/永久存储

### （十）WebSocket



### 补充 

暂无
