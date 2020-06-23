---
title: ArrayNot
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:02:09
tags: [数组,去重]
---

![text image](array.jpg)

> 分享一些数组去重的方法

<!--more-->

> 思路：创建一个新数组，遍历原数组，若遍历元素在新数组不存在就添加到数组中，反正则忽略

```bash
function uniqeArray(arr){
  var res = [];
  for(var i = 0;i < arr.length;i++){
      var repeat = false;
      for(var j = 0;j < res.length ; j++){
          if(arr[i] === res[j]){
              repeat = true;
              break;
          }
      }
      if(!repeat){
          res.push(arr[i]);
      }
  }
  return res;
}

```


<h3>先排序再去重</h3>

> 思路：先对数组排序，再定义一个新的数组，遍历排序后的数组，
> 若排序后的数组元素不等于新数组的最后一个元素，则添加。

```bash
function uniqeArray(arr){
  function sortNumber(a , b){
      return a - b;
  }
  var newArr = arr.sort(sortNumber);
  var res = [];
  for(var i = 0;i < newArr.length;i++){
      if(newArr[i] !== res[res.length - 1]){
          res.push(newArr[i]);
      }
  }
  return res;
}
```



<h3>对象去重</h3>

> 思路：利用对象的属性。遍历数组，若该数组元素不是对象的属性，则添加。

```bash
function uniqeArray(arr) {
   var res = [];
   var temp = {};
   for(var i = 0; i< arr.length; i++){
       if(!temp[arr[i]]){
           res.push(arr[i]);
           temp[arr[i]] = 1;
       }
   }
   return res;
}
```



<h3>filter，indexOf方法</h3>

> 思路：通过filter筛选出去重后的数组。若indexOf方法在该元素之后再查不到该元素的位置，表示该元素不存在，符合要求。

```bash
function uniqeArray(arr) {
   return arr.filter(function (item, index, array) {
       return array.indexOf(item, index+1) === -1;
   })
}
```


<h3>ES6 Set</h3>


> 思路：利用ES6中Set不包含重复元素的思想，为数组创建set对象，再将set对象转换为数组。


```bash
function uniqeArray(arr) {
   return Array.from(new Set(arr));
}
```
