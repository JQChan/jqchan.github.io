---
title: delete操作符
date: 2018-09-05 21:32:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [JS]
categories: 前端开发
subtitle: delete操作符
---
这篇文章主要介绍一下[delete](https://devdocs.io/javascript/operators/delete)操作符。delete操作符主要用于从对象中删除属性，结果是对象不再保留对此属性的引用，最终自动释放，所以之后在查询此属性的话会返回undefined。如
``` javascript
var Employee = {
  firstname: "Mohammed",
  lastname: "Haddad"
}

console.log(Employee.firstname);
// "Mohammed"

delete Employee.firstname;

console.log(Employee.firstname);
// undefined
console.log(Employee)
// Object { lastname: "Haddad" }
```
### 语法：
```
delete object.property
delete object['property']
```
### 返回值：
``` javascript
true / false
```
**非严格模式下，删除对象的不可配置属性的情况会返回false，其他情况都会返回true，包括删除一个不存在的属性也会返回true**

严格模式下，删除对象的不可配置属性会报**SyntaxError**语法错误

如下：
``` javascript
var Employee = {
  age: 28,
  name: 'abc',
  designation: 'developer'
}

console.log(delete Employee.name);   // 返回true
console.log(delete Employee.age);    // 返回true

// 尝试删除一个不存在的属性，结果会返回true
console.log(delete Employee.salary); // 返回true
// 定义一个属性是不可配置的
Object.defineProperty(Employee, 'height', {configurable: false});
console.log(delete Employee.height) // 返回false
```

**无论在全局作用域中还是函数作用域中，通过var、let、const声明的变量的configurable都为false，所以采用delete操作符是无法删除的，但直接声明的全局变量却可以采用delete操作符直接删除**
``` javascript
var nameOther = 'XYZ';

// 直接在全局作用域生命一个变量adminName
adminName = 'xyz';   

// 通过以下方法获取全局属性
Object.getOwnPropertyDescriptor(window, 'nameOther'); 
// Object {value: "XYZ", 
//                  writable: true, 
//                  enumerable: true,
//                  configurable: false}

// 因为nameOther是通过var去声明的，所以它是不可配置的

delete nameOther;   // 返回false

delete adminName;       // 返回true
```
**delete操作符只会删除对象自己的属性，但如果此对象的原型链上存在删除的属性，则对象会继续使用原型链上的那个属性**
``` javascript
function Foo() {
  this.bar = 10;
}

Foo.prototype.bar = 42;

var foo = new Foo();

// 删除自身的属性，返回true
delete foo.bar;           

// foo.bar还是可用的，因为它的原型链上还存在bar属性
console.log(foo.bar);

delete Foo.prototype.bar; 

// 原型链上的bar属性已删除，所以输出undefined
console.log(foo.bar);   
```
**delete操作符不能删除全局作用域中的function函数，但如果函数作为对象的方法，则可以删除**

**delete操作符也不能删除浏览器内置的静态属性或方法**
``` javascript
delete Math.PI; // 返回false
```

### 删除数组元素
**采用delete操作符删除任何数组的元素，都不会影响数组的长度（即length），但这个元素将不再存在在数组中，所以删除数组元素建议采用直接将数组的元素直接赋值为undefined或者采用splice方法去删除某个元素**
``` javascript
var trees = ['redwood', 'bay', 'cedar', 'oak', 'maple'];
delete trees[3];
if (3 in trees) {
    // 这里的代码将不会执行到
}
```