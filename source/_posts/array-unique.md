---
title: JavaScript 数组去重
date: 2018-09-22 13:34:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [JS]
categories: 前端开发
subtitle: JavaScript 数组去重
---
## 数组去重方法
### 1.  利用ES6 Set去重（ES6中常用）
原理：
**Set对象能存储任何类型值的唯一值，无论是原始值还是对象引用，（https://devdocs.io/javascript/global_objects/set）**
new Set只会返回一个Set对象，在这个对象中的值只能出现一次，它在Set对象中是独一无二的;

⚠️ Set对象根据值相等原则去筛选，+0和-0、0相等，NaN也等于NaN，但{}不等于{}, []不等于[](即值如果是引用类型的，如果不是同一个引用，值都不相等)

**缺点：** 所以，Set不能去掉空对象或者空数组
``` javascript
function unique(arr) {
  return Array.from(new Set(arr))
}
//  或者
var uniqueArr = [...new Set(arr)]
```

### 2.  利用for循环嵌套for循环，然后利用数组的splice方法去重（ES5中常用）
原理：
第一层从arr[0]的地方开始，第二层是从j+1的地方开始循环arr[i]后面的元素，数组是引用类型，同一个数组循环splice的话此时数组的长度减1，所以在第二层循环中找到相同的话j执行j--再从原来删掉的地方继续循环
``` javascript
function unique(arr){
  for(var i = 0; i < arr.length; i++){
    for(var j = j + 1; j < arr.length; j++){
      if(arr[i] === arr[j]){
        arr.splice(j, 1)
        j--
      }
    }
  }
  return arr
}
```
### 3.  利用Array.indexOf或者Array.includes去重
原理：新建一个array，for 循环原数组，使用Array.indexOf()或者Array.includes()查找判断结果数组array是否存在当前元素，如果查找不到，则添加，最后这个新的array就是去重后的array
``` javascript
function unique(arr){
  var array = [];
  arr.map(function(item, i){
    if(array.indexOf(item) === -1){
    // if(!array.includes(item)){
      array.push(item)
    }
  })
  return array
}
```
### 4.  利用sort()
原理：利用Array.sort()方法将原数组排序，然后判断左右相邻元素是否相等，从而去重，可以采用新建数组的方法，也可以采用splice方法
``` javascript
function unique(arr){
  arr = arr.sort() //默认由小到大排序
  for(var i = 0; i < arr.length; i++){
    if(arr[i+1] === arr[i]){
      arr.splice(i + 1, 1)
      i--
    }
  }
  return arr
}
```
### 5.  利用对象不存在相同属性方法去重
原理： 利用对象不存在相同属性方法去重，或者利用Object.hasOwnProperty()
``` javascript
function unique(arr){
  var obj = {}
  var array = []
  arr.map(function(item, i){
    obj[item] = item
  })
  for(var key in obj){
    array.push(obj[key])
  }
  return array
}
```
``` javascript
function unique(arr){
  var obj = {}
  return arr.filter(function(item, index, arr){
    return obj.hasOwnProperty(typeof item + item) ? false :
      (obj[typeof item + item] = true)
  })
}
```
### 6.  利用Array.filter()&Array.indexOf()数组去重
原理：利用Array.filter()筛选数组当前元素在数组中的indexOf索引是否等于当前索引
``` javascript
function unique(arr){
  return arr.filter(function(item, index, arr){
    return arr.indexOf(item) === index
  })
}
```
### 7.  利用Map数据结构去重
原理：Map对象包含键值对。任何值（对象和原始值）都可以用作键或值。键是唯一的

创建一个空Map数据结构，遍历需要去重的数组，把数组的每一个元素作为key存到Map中。由于Map中不会出现相同的key值，所以最终得到的就是去重后的结果
``` javascript
function unique(arr){
  let map = new Map()
  let array = []
  arr.map(function(item, i){
    if(map.has(item)){
      map.set(item, true)
    } elsee{
      map.set(item, false)
      array.push(item)
    }
  })
  return array
}
```
