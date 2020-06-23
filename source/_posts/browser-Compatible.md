---
title: 浏览器兼容
typora-root-url: ../ArrayNot/
date: 2019-07-29 20:57:07
tags: [浏览器兼容]
---
### 前端浏览器兼容知识点整理

   做前端，总会涉及到浏览器兼容的问题，之所以存在浏览器兼容的问题，是因为各个浏览器的内核不同，相对应的同一套代码，不的浏览器解析后，所呈现的页面效果也会存在一定的差异

![images](bg.jpg)

<!--more-->



### 一 浏览器内核差异

- Trident(IE内核)：

　　　　IE6、IE7、IE8（Trident 4.0）、IE9（Trident 5.0）、IE10（Trident 6.0）、360安全浏览器（1.0-5.0为Trident，6.0为Trident+Webkit，7.0为Trident+Blink）猎豹极轻浏览器，360极速浏览器（7.5之前为Trident+Webkit，7.5为Trident+Blink）猎豹安全浏览器（1.0-4.2版本为Trident+Webkit，4.3及以后版本为Trident+Blink）猎豹极轻浏览器，傲游浏览器（傲游1.x、2.x为IE内核，3.x为IE与Webkit双核）、百度浏览器（早期版本）、世界之窗浏览器[2]  （最初为IE内核，2013年采用Chrome+IE内核）、2345浏览器、腾讯TT、淘宝浏览器、采编读浏览器、搜狗高速浏览器（1.x为Trident，2.0及以后版本为Trident+Webkit）、阿云浏览器（早期版本）、瑞星安全浏览器、Slim Browser、 GreenBrowser、爱帆浏览器（12 之前版本）、115浏览器、155浏览器、闪游浏览器、N氧化碳浏览器、糖果浏览器、彩虹浏览器、瑞影浏览器、勇者无疆浏览器、114浏览器、蚂蚁浏览器、飞腾浏览器、速达浏览器、佐罗浏览器、海豚浏览器（iPhone/iPad/Android）、UC浏览器（Blink内核+Trident内核）等。


- Gecko(Firefox内核):

　　　　Mozilla Firefox、Mozilla SeaMonkey、waterfox（Firefox的64位开源版）、Iceweasel、Epiphany（早期版本）、Flock（早期版本）、K-Meleon。

　　Presto(Opera前内核) (已废弃)：

　　　　Opera12.17及更早版本曾经采用的内核，现已停止开发并废弃。


- Webkit(Safari内核,Chrome内核原型,开源)：

　　　　傲游浏览器3、[1]  Apple Safari (Win/Mac/iPhone/iPad)、Symbian手机浏览器、Android 默认浏览器。

　　Blink：

　　　　这一渲染引擎是开源引擎WebKit中WebCore组件的一个分支，并且在Chrome（28及往后版本）、Opera（15及往后版本）和Yandex浏览器中使用。

　　浏览器内核的区别，我们只做了解即可，感兴趣的同学，可以自己去搜搜啊~


### 二 兼容问题处理细则


1、浏览器默认会有一些自己独有的属性，像内外边距啦，图片边框啊、input自带的样式啊等等，当我们用到这些标签及样式时，就需要手动的清楚浏览器默认样式，比如清除补丁和边距：*{margin:0;padding:0;}，像这样使用通配符强制将补丁和边距置为零，简单粗暴，但是这样处理比较消耗性能，我一般倾向于使用一些CSS样式重置库，常见的有以下几种，大家可以根据实际需求来选择：

　　Neat.css：解决Bug，特别是低级浏览器的常见Bug；统一效果，但不盲目追求重置为0；向后兼容；考虑响应式；考虑移动设备。

　　　　　　　http://thx.github.io/cube/doc/neat

　　Reset.css：对浏览器样式的重置（杀伤力偏大）

　　　　　　　  http://meyerweb.com/eric/tools/css/reset/

　　Normalize.css：修复浏览器样式

　　　　　　　　　　https://yuilibrary.com/yui/docs/cssnormalize/

　　除了这些，大家还可以借鉴百度、淘宝的样式重置表。


2、块级元素浮动后，又使用margin来控制相邻块级元素的间距的情况下，在IE6下，margin值要比我们设置的值大，这样，后面浮动的元素就会被挤到下面去，解决方案是：将浮动的块级元素的display属性值设为inline-block。

---

3、设置标签的高度小于10px的时候，在IE6，IE7，遨游中标签的高度会超出自己设置高度。解决方案：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。

---

4、行内属性标签，设置display:block后采用float布局，又有横行的margin的情况，ie6间距bug。解决方案：在display:block;后面加入display:inline;display:table;。

---

5、几个img标签放在一起的时候，有些浏览器会有默认的间距。解决方案：使用float属性为img布局。

---
6、min-height设置标签最小高度的时候不兼容。解决方案：如果我们要设置一个标签的最小高度200px，需要进行的设置为：{min-height:200px; height:auto !important; height:200px; overflow:visible;}

---
7、CSS Hack技巧

类内属性前缀法+选择器前缀法：

　　　　在标准模式中：

　　　　“-″减号是IE6专有的hack
　　　　“\9″ IE6/IE7/IE8/IE9/IE10都生效
　　　　“\0″ IE8/IE9/IE10都生效，是IE8/9/10的hack
　　　　“\9\0″ 只对IE9/IE10生效，是IE9/10的hack
　　　　*html *前缀只对IE6生效
　　　　*+html *+前缀只对IE7生效
　　　　@media screen\9{...}只对IE6/7生效
　　　　@media \0screen {body { background: red; }}只对IE8有效
　　　　@media \0screen\,screen\9{body { background: blue; }}只对IE6/7/8有效
　　　　@media screen\0 {body { background: green; }} 只对IE8/9/10有效
　　　　@media screen and (min-width:0\0) {body { background: gray; }} 只对IE9/10有效
　　　　@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {body { background: orange; }} 只对IE10有效


---

8、!important

　　在ie6下，同一个大括号里对同一个样式属性定义，其中一个加important 则important标记是被忽略的，例：{background:red!important; background:green;} ie6下解释为背景色green，其它浏览器解释为背景色red；如果这同一个样式在不同大括号里定义，其中一个加important 则important发挥正常作用，例：div{background:red!important} div{background:green}，这时所有浏览器统一解释为背景色red。

---
9、点击超链接后，hover、active样式不生效。解决方案，css属性排列为L-V-H-A。

---
10、给块级元素设置高度高度的时候，最好也同时设置上line-height属性值。

---

11、去除超链接虚线边框的问题。当点击超链接时，ff、ie6、ie7、ie8会出现虚线边框。

　　　　解决方案：ie6/7中 设置为a {blr:expression_r(this.onFocus=this.blur()) }

　　　　　　　　　ie8 和 ff 都不支持expression 在ie8 、ff中设置为  :focus { outline: none; }
---

12、css滤镜的问题：ff、safari、chrome、opera使用opacity属性，ie使用设置filter:alpha(opacity=50)时，ie6/7失效，还要设置zoom:1width:100%。

---
13、IE8不兼容Bootstrap框架的解决方案。

　　　　引入respond.min.js库，兼容响应式布局。不过需要注意的是，这个库不能放在本地路径下（Fill://），要用静态资源链接或者放在服务器上才能生效。

---
14、不兼容H5标签的解决方法：引入html5shiv.min.js文件。

---
16、IE8下，父级div或者兄弟div有浮动或定位属性的时候，div模块设置背景颜色会失效，或者div本身有浮动属性，设置背景色也可能会失效，此时注意布局的方法，我遇到过的是第一种情况，我的解决方法时给父级div设置相对定位，相邻div不设置定位或浮动，本身使用绝对定位，到想要去的位置，可以让背景颜色生效。


### 补充一些知识

IE6双边距问题；在 IE6中设置了float , 同时又设置margin , 就会出现边距问题

解决方案：设置display:inline;

当标签的高度设置小于10px，在IE6、IE7中会超出自己设置的高度
解决方案：超出高度的标签设置overflow:hidden,或者设置line-height的值小于你的设置高度

图片默认有间距
解决方案：使用float 为img 布局

IE9一下浏览器不能使用opacity
解决方案：
```
opacity: 0.5;filter: alpha(opacity = 50);filter: progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);

```
边距重叠问题；当相邻两个元素都设置了margin 边距时，margin 将取最大值，舍弃最小值；
解决方案：为了不让边重叠，可以给子元素增加一个父级元素，并设置父级元素为overflow:hidden；

两个块级元素，父元素设置了overflow:auto；子元素设置了position:relative ;且高度大于父元素，在IE6、IE7会被隐藏而不是溢出；
解决方案：父级元素设置position:relative


### 接着补充一些细节问题

NO1.我们所熟悉的hack

代码: 使用hacker我可以把浏览器分为3类：IE6 ；IE7和遨游；其他（IE8 chrome ff safari opera等）

IE6认识的hacker 是下划线_ 和星号 *

◆IE7 遨游认识的hacker是星号 *

比如这样一个CSS设置：

```
height:300px;*height:200px;_height:100px; 

```
IE6浏览器在读到height:300px的时候会认为高时300px；继续往下读，他也认识*heihgt， 所以当IE6读到*height:200px的时候

会覆盖掉前一条的相冲突设置，认为高度是200px。继续往下读，IE6还认识_height,所以他又会覆盖掉200px高的设置，把高度设置

为100px；

IE7和遨游也是一样的从高度300px的设置往下读。当它们读到*height200px的时候就停下了，因为它们不认识_height。所以它们

会把高度解析为200px，剩下的浏览器只认识第一个height:300px;所以他们会把高度解析为300px。因为优先级相同且想冲突的属性

设置后一个会覆盖掉前一个，所以书写的次序是很重要的。


1、针对I E 系列浏览器的网站设计代码 

针对 IE 6的专属CSS Hack网站设计代码#id{display:block;}也就是在网站设计CSS属性前加一个小划线就好。

针对 IE 7的专属CSS Hack网站设计代码#id{*display:block;}即在网站设计CSS属性前加上一个星号即可        针对 IE 8的

专属CSS Hack网站设计代码#id{margin-top:10px 9;/*IE8*/}

如上所示，解决办法为在网站设计CSS属性后分号前加上空格与斜线并加入一个数字9即可 。

---
2、针对火狐的CSS Hack 网站设计代码        

火狐可谓是最标准的浏览器之一了，网站设计技术只要稍稍不到位就能体现得淋漓尽致，所以不少网站设计师也很头痛，其实想要解

决火狐的兼容性除了要把网站设计的基础知识扎牢之外只要将CSS代码写入到 
```

@-moz-document url-prefix()的{ } 里面就行了        

例如:@-moz-document url-prefix(){#id{ display: block; }}。

```
3、针对Safari的CSS Hack网站设计代码

Safari是苹果计算机的最新作业系统Mac OS X中新的浏览器，用来取代之前的Internet Explorer for Mac，使用了KDE的KHTML作为浏览器的运算核心。

```
@media screen and (-webkit-min-device-pixel-ratio:0){#id { display: block; }}兼容性做法和火狐相近。

```

4、针对 Opera 的CSS Hack 网站设计代码

Opera即Opera Software ASA，是台式机、各种设备和移动网络浏览器市场的商业领袖，因快速、小巧和比其他浏览器更佳的标准兼

容性获得了国际上的最终用户和业界媒体的承认，并在网上受到很多人的推崇。

```
@media all and (-webkit-min-device-pixel-ratio:10000), not all and (-webkit-min-device-pixel-ratio:0)

{head~body #id { display: block; }} 

```
(前面的一堆是在做浏览器的初始化)


NO9.透明度兼容设置

```
transparent_class {   

    filter:alpha(opacity=50);   

       -moz-opacity:0.5;   

       -khtml-opacity: 0.5;   

       opacity: 0.5;   

 } 
```
