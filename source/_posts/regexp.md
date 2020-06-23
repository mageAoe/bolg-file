---
title: 正则表达式
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:10:39
tags:
---
一个个音符杂乱无章的组合在一起，弹奏出的或许就是噪音，同样的音符经过作曲家的手，就可以谱出非常动听的乐曲，一个演奏者同样可以照着乐谱奏出动听的乐曲，但他/她或许不知道该如何去改变音符的组合，使得乐曲更动听。

作为正则的使用者也一样，不懂正则引擎原理的情况下，同样可以写出满足需求的正则，但是不知道原理，却很难写出高效且没有隐患的正则。所以对于经常使用正则，或是有兴趣深入学习正则的人，还是有必要了解一下正则引擎的匹配原理的。
![Image text](bg.png)



<!-- more -->


定义
正则表达式（regular expression）是一个描述字符模式的对象，使用正则表达式可以进行强大的模式匹配和文本检索与替换功能。

JavaScript 的正则表达式语法是 Perl5 的正则表达式语法的大型子集，所以对于有 Perl 编程经验的程序员来说，学习 JavaScript 中的正则表达式是小菜一碟。

正则表达式是描述字符模式的对象，用于对字符串模式匹配及检索替换，是对字符串执行模式匹配的强大工具。
JavaScript中的正则表达式用RegExp对象表示，可以使用RegExp()构造函数来创建RegExp对象，不过RegExp对象更多是通过字面量的语法来创建。

```bash
<!-- // 不推荐写法 -->
var patt = new RegExp(pattern模式,modifiers修饰符)
<!-- // 匹配所有的a或A -->
var reg = new RegExp("a","gi")
```
> 字面量

```bash
<!-- // 推荐写法 -->
var patt = /pattern/modifiers
<!-- // 匹配所有的a或A -->
var reg = /a/gi
```

```bash
function getRE(){
	var re = /[a-z]/
	re.foo = 'bar'
	return re
}
var reg = getRE()
re2 = getRE()
console.log(reg === re2)
reg.foo = 'baz'
console.log(re2.foo)
ECMAScript3同一对象
<!-- // true -->
<!-- // "baz" -->
ECMAScript5不同对象
<!-- // false -->
<!-- // "bar" -->

```
### 表达式

表达式|	描述
:----:|:----
i	|执行对大小写不敏感的匹配
g	|执行全局匹配模式（查找所有匹配而非在找到第一个匹配后停止）
m	|执行多行匹配模式

```bash
var str='HwwwwLwello orllld lLll!'
console.log(str.match(/l/))
<!-- // ["l", index: 8, input: "HwwwwLwello orllld lLll!"] -->
console.log(str.match(/l/i))
<!-- // ["L", index: 5, input: "HwwwwLwello orllld lLll!"] -->
console.log(str.match(/l/g))
<!-- // ["l", "l", "l", "l", "l", "l", "l", "l"] -->
var str='Hwwwwl\nwello orllld lLll!'
console.log(str)
<!-- // Hwwwwl -->
<!-- // wello orllld lLll! -->
console.log(str.match(/l$/))
<!-- // null -->
console.log(str.match(/l$/m))
<!-- // ["l", index: 5, input: "Hwwwwl↵wello orllld lLll!"] -->

```
### 元字符

与其他语言中的正则表达式类似，模式中使用的所有元字符都必须转义。正则表达式中的元字符包括：
```	
( [ { \ ^ $ | ) ? * + . ] }

```
这些元字符在正则表达式中都有一或多种特殊用途，因此如果想要匹配字符串中包含的这些字符，就必须对它们进行转义。
下面给出几个例子。

```bash
var pattern1 = /[bc]at/i
<!-- // 匹配第一个"bat"或"cat"，不区分大小写 -->
var pattern2 = /\[bc\]at/i
<!-- // 匹配第一个" [bc]at"，不区分大小写 -->

```

### 直接量字符
字符	|描述
:----:|:----
字母数字|	自身
\0	|查找 NUL 字符（\u0000）
\t	|查找制表符（\u0009）
\v	|查找垂直制表符（\u000A）
\n	|查找换行符（\u000B）
\f	|查找换页符（\u000C）
\r	|查找回车符（\u000D）
\xdd	|查找以十六进制数 dd 规定的字符（\x0A => \n）
\uxxxx	|查找以十六进制数 xxxx 规定的 Unicode 字符（\u0009 => \t）
\cX	|控制字符^X （\cJ => \n）

```bash
var str='null \t \n \f \r '
console.log(str.match(/\n/))
// ["↵", index: 7, input: "null 	 ↵   "]
console.log(str.match(/\f/))
// ["", index: 9, input: "null 	 ↵   "]
var str='null'
console.log(str.test(/\0/))
//
```


![Image text](my-first-boke/Hong_Kong_Skyline_by_HKHSBC.jpg)
### 字符类

字符	|描述
:----:|:----
.	|查找单个字符，除了换行和行结束符
\w	|(word)查找单词字符：[a-zA-Z_0-9]（单词字符包括：a-z、A-Z、0-9，以及下划线）
\W	|查找非单词字符：[^a-zA-Z_0-9]（单词字符包括：a-z、A-Z、0-9，以及下划线）
\s	|(white space)查找空白字符
\S	|查找非空白字符
\d	|(digit)查找数字：0-9
\D	|查找非数字字符：[^0-9]
0-9	|查找任何从 0 至 9 的数字
[a-z]	|查找任何从小写 a 到小写 z 的字符
[A-Z]	|查找任何从大写 A 到大写 Z 的字符
[A-z]	|查找任何从大写 A 到小写 z 的字符
[…]	|查找方括号之间的任何字符（没有顺序同级）
[^…]	|查找不在方括号之间的任何字符
[adgk]	|查找给定集合内的任何字符
[^adgk]	|查找给定集合外的任何字符

```bash
var str='3 o !_..'
console.log(str.match(/\w/g))
<!-- // ["3", "o", "_"] -->
var str='3 o !_..'
console.log(str.match(/\W/g))
<!-- // [" ", " ", "!", ".", "."] -->
var str='3 o !_..'
console.log(str.match(/\s/g))
<!-- // [" ", " "] -->
var str='3 o !_..'
console.log(str.match(/\S/g))
<!-- // ["3", "o", "!", "_", ".", "."] -->
var str='3 o !_..'
console.log(str.match(/\d/g))
<!-- // ["3"] -->
var str='3 o !_..'
console.log(str.match(/\b/g))
<!-- // ["", "", "", "", "", ""] -->
注：单词前后
var str='3 o A!_..'
console.log(str.match(/[A-Z]/g))
<!-- // ["A"] -->
var str='3 o A!_..'
console.log(str.match(/[A-z]/g))
<!-- // ["o", "A", "_"] -->
注：此处出现了"_"，a-z、A-Z，以及下划线
var str='12323 orllbld lLll!'
console.log(str.match(/[abc]/g))
<!-- // ["b"] -->
console.log(str.match(/[ro3]/g))
<!-- // ["3", "3", "o", "r"] -->
console.log(str.match(/[^abc]/g))
<!-- // ["1", "2", "3", "2", "3", " ", "o", "r", "l", "l", "l", "d", " ", "l", "L", "l", "l", "!"] -->

```

### 重复字符

字符	|描述
:----:|:----
X{n,m}	|匹配包含 n 至 m 个 X 的序列的字符串。
X{n,}	|匹配包含至少 n 个 X 的序列的字符串。
X{n}	|匹配包含 n 个 X 的序列的字符串。
X?	|(有吗?)匹配任何包含零个或一个 X 的字符串 {0,1}
X+	|(加号是追加的意思)匹配任何包含至少一个 X 的字符串 {1,}
X*	|(任意次)匹配任何包含零个或多个 X 的字符串 {0,}


```bash
var str='Hwwwwlllll orlllld lll!'
console.log(str.match(/l{3,5}/))
<!-- // ["lllll", index: 5, input: "Hwwwwlllll orlllld lll!"] -->
console.log(str.match(/l{2,3}/))
<!-- // ["lll", index: 5, input: "Hwwwwlllll orlllld lll!"] -->
注：匹配出去l为3、4、5
console.log(str.match(/l{0,1}/))
<!-- // ["", index: 0, input: "Hwwwwlllll orlllld lll!"] -->
console.log(str.match(/l?/))
<!-- // ["", index: 0, input: "Hwwwwlllll orlllld lll!"] -->
console.log(str.match(/l{1,}/))
<!-- // ["lllll", index: 5, input: "Hwwwwlllll orlllld lll!"] -->
console.log(str.match(/l+/))
<!-- // ["lllll", index: 5, input: "Hwwwwlllll orlllld lll!"] -->
var str='Hwwwwwello orllld llll!'
console.log(str.match(/l{3,5}/))
<!-- // ["lll", index: 13, input: "Hwwwwwello orllld llll!"] -->
console.log(str.match(/l{1,4}/))
<!-- // ["ll", index: 7, input: "Hwwwwwello orllld llll!"] -->
console.log(str.match(/l{2}/))
注：匹配两个l
<!-- // ["ll", index: 7, input: "Hwwwwwello orllld llll!"] -->
console.log(str.match(/l{4,}/))
<!-- // ["llll", index: 18, input: "Hwwwwwello orllld llll!"] -->
var str='01';
console.log(str.match(/0?/));
<!-- // ["0", index: 0, input: "01"] -->
console.log(str.match(/1?/));
<!-- // ["", index: 0, input: "01"] -->
注：尽可能少的匹配{0,1}
console.log(str.match(/0*/));
<!-- // ["0", index: 0, input: "01"] -->
console.log(str.match(/1*/));
<!-- // ["", index: 0, input: "01"] -->
注：{0,}
console.log(str.match(/1+/));
<!-- // ["1", index: 1, input: "01"] -->
注：{1,}
```

### 非贪婪重复

> 尽可能少的匹配：??、+?、*?、{1,4}?

```bash
var str='0111'
console.log(str.match(/00?/))
<!-- ["0", index: 0, input: "011"] -->
console.log(str.match(/01?/))
<!-- ["01", index: 0, input: "011"] -->
console.log(str.match(/11?/))
<!-- ["11", index: 1, input: "011"] -->
console.log(str.match(/01+/))
<!-- ["0111", index: 0, input: "011"] -->
console.log(str.match(/01+?/))
<!-- ["01", index: 0, input: "011"] -->
注：{1}
var str='0111'
console.log(str.match(/11??/))
<!-- ["1", index: 1, input: "011"] -->
console.log(str.match(/01??/))
<!-- ["0", index: 0, input: "011"] -->
console.log(str.match(/01*/))
<!-- ["0111", index: 0, input: "0111"] -->
console.log(str.match(/01*?/))
<!-- ["0", index: 0, input: "0111"] -->
注：?? = *? ==》 {0}
var str='0111'
console.log(str.match(/1{1,4}?/))
<!-- ["1", index: 1, input: "0111"] -->
var regex = /\d{2,5}?/g;
var string = "123 1234 12345 123456";
console.log(string.match(regex));
// => ["12", "12", "34", "12", "34", "12", "34", "56"]

```

### 锚字符

字符	|描述
:----:|:----
^	|匹配字符串开头(用正则表达式处理多行时匹配行的开始)
$	|匹配字符串结尾(处理多行时匹配行尾)
\b	|匹配单词边界
\B	|匹配非单词边界
(?=p)	|零宽正向先行断言，要求接下来的字符都与p匹配，但不能包括匹配p的那些字符 (?=p) => p
(?!p)	|零宽正向先行断言，要求接下来的字符不与p匹配 (?!p) => [^p]


```bash
var str='orllld'
console.log(str.match(/^o/))
<!-- // ["o", index: 0, input: "orllld"] -->
console.log(str.match(/d$/))
<!-- // ["d", index: 5, input: "orllld"] -->
var str='orllld'
<!-- 0o1r2l3l4l5d6 -->
console.log(str.replace(/(?=d)/, ','))
<!-- // ["", index: 5, input: "orllld"] -->
<!-- // orlll,d -->
var str='orllld '
console.log(str.match(/d$/))
<!-- // null -->
console.log(str.match(/l(?=d)/))
<!-- // ["l", index: 4, input: "orllld "] -->
console.log(str.match(/l(?!d)/))
<!-- // ["l", index: 2, input: "orllld "] -->
var str='JavaScript'
console.log(str.match(/Java(Script)([A-Z]\w*)/))
<!-- // null -->
console.log(str.match(/Java(?=Script)([A-Z]\w*)/))
<!-- // ["JavaScript", "Script", index: 0, input: "JavaScript"] -->
console.log(str.match(/Java(?=Bcript)([A-Z]\w*)/))
<!-- // null -->
console.log(str.match(/Java(?!Script)([A-Z]\w*)/))
<!-- // null -->
console.log(str.match(/Java(?!Bcript)([A-Z]\w*)/))
<!-- // ["JavaScript", "Bcript", index: 0, input: "JavaScript"] -->
var str='JavaScriptS'
console.log(str.match(/Java(Script)([A-Z]\w*)/))
<!-- // null -->
```

```bash
var str='JavaScriptS'
console.log(str.replace(/Java(?!Script)([A-Z]\w*)/, function($0, $1, $2) {
		return $0 + ',' + $1 + ',' + $2
	}))
<!-- // JavaScriptS -->
var str='JavaSs'
console.log(str.match(/Java(?!Script)([A-Z]\w*)/))
<!-- // ["JavaSs", "Ss", index: 0, input: "JavaSs"] -->
console.log(str.replace(/Java(?!Script)([A-Z]\w*)/, function($0, $1, $2) {
		return $0 + ',' + $1 + ',' + $2
	}))
<!-- // JavaSs,Ss,0 -->
var str='JavaType'
console.log(str.match(/Java(?!Script)([A-Z]\w*)/))
<!-- // ["JavaType", "Type", index: 0, input: "JavaType"] -->
```


[算法结构一：简书](https://www.jianshu.com/p/1b4068ccd505)

[算法结构二：简书](https://www.jianshu.com/p/0f56afd5122e?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

[算法结构三：简书](https://www.jianshu.com/p/e02ff2afd300?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

[出处](https://luuman.github.io/2018/02/27/Induce/JavaScript/Base/1.10-RegExpObjects/#more)
