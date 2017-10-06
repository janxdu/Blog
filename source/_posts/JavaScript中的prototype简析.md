---
title: JavaScript中的prototype简析
date: 2017-01-15 01:16:00
categories: Front End
tags: [JavaScript] 
---
### prototype定义

一个对象内部对原型的引用称为 [[Prototype]]。对象的原型是没有公开的属性名去访问的。由于浏览器实现以`__proto__`来访问对象的[[prototype]]，ES6出于兼容性考虑将其纳入规范，但是一般不推荐使用。
一个对象有原型，其原型对象又有自己的原型，直到某个对象的原型是null为止，这种一级一级的链式结构称为原型链。
![JavaScriptObjectLayout](http://ojs1n6jlb.bkt.clouddn.com/JavaScriptObjectLayout.png)

上图由`Foo`生成的对象的[[prototype]]是`Foo.prototype`，`Foo.prototype`的[[prototype]]是`Object.prototype`，`Object.prototype`是null，至此就是一条完整的原型链。可以总结为如下表格：

| Object| [[prototype]] | prototype |
| --- | --- | --- |
| Foo Instances | Foo.prototype | undefined |
| Foo constructor |  Function.prototype| Foo.prototype |
|Function constructor|Function.prototype|Function.prototype|
|Function.prototype|Object.prototype|undefined|
|Object.prototype|null|undefined|
### 用途
JavaScript 是基于原型的语言，原型链的设定就是少数能够让多个对象共享属性和方法，甚至模拟继承的方式。

### 注意
- `null` 对象不是`Object`的实例，但是
```javascript
typeof null;//"object"
null instance of Object;//false
```
- 使用`new`关键字创建一个对象的实例时，其原型对象的`constructor`属性默认指向其构造函数，可以重写为其他值。
- 在通过原型链实现继承时，不能使用对象字面量创建原型方法。



引用：
[mozilla ` __proto__`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto)
[mozilla prototype chain](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
[JavaScript 原型系统的变迁，以及 ES6 class](https://segmentfault.com/a/1190000003798438)

