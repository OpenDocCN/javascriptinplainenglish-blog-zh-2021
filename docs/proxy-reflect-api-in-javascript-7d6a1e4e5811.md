# JavaScript 中的代理和反射 API 简介

> 原文：<https://javascript.plainenglish.io/proxy-reflect-api-in-javascript-7d6a1e4e5811?source=collection_archive---------8----------------------->

![](img/6fcb1922d1e393d2a2d64463bae1348d.png)

代理和反射 API 出现在 ES6 中，两者配合得非常好！

首先，

## 代理人

一个**代理**是外来物体，它没有属性！它包装了对象的行为。它需要两个参数。

```
const toto = new Proxy(target, handler)
```

**目标**:代理将要代理/包装的对象。

**handler:** 是代理的配置，它会拦截目标上的操作(get、set 等。)，你会看到一个例子！

多亏了**代理**，你可以像这样创建`traps`:

```
const toto = { a: 55, b:66 }
const handler = {
   get(target, prop, receiver) {
      if (!!target[prop]) {
         return target[prop]
      }
      return `This ${prop} prop don’t exist on this object !`
   }
}const totoProxy = new Proxy (toto, handler)totoProxy.a // 55
totoProxy.c // This c prop don’t exist on this object !
```

每个内部对象`method`都有自己的*目标函数。*

下面是等同于 Target 的对象方法列表

```
| object method | target |
| — — — | — — |
| object[prop] | get |
| object[prop] = 55 | set |
| new Object() | construct |
| Object.keys | ownKeys |
```

这是完整的清单🔗[*https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Proxy/Proxy*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy*)

目标函数的参数可以根据函数而改变。

比如对于 **get** 函数，取*(目标，道具，接收者(代理本身))*但是对于 **set** 函数，取*(目标，道具，值(要设置)，接收者)。*

## 用法示例

我们可以创造一个🔓秘密财产！

```
 const toto = {
   name: ‘toto’,
   age: 25,
   _secret: ‘***’
}const handler = {
   get(target, prop) {
      if (prop.startsWith(‘_’)) {
         throw new Error(‘Access denied’)
      }
      return target[prop]
   },
   set(target, prop, value) {
      if (prop.startsWith(‘_’)) {
         throw new Error(‘Access denied’)
      }
      target[prop] = value
      // set methods return boolean,
      // in order to let us know if the value has been correctly set !
      return true
   },
   ownKeys(target, prop) {
      return Object.keys(target).filter(key => !key.startsWith(‘_’))
   },
}const totoProxy = new Proxy (toto, handler)
for (const key of Object.keys(proxy1)) {
   console.log(key) // ‘name’, ‘age’
} 
```

## 显示

反射是一个静态类，它简化了代理的创建。

每个内部对象方法都有自己反射方法:

```
| object method | Reflect|
| — — — | — — |
| object[prop] | Reflect.get|
| object[prop] = 55 | Reflect.set|
| new Object() | Reflect.construct|
| Object.keys | Reflect.ownKeys |
```

这是完整的清单🔗[*https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Reflect*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect*)

❓为什么要用它？因为它与代理配合得非常好！它接受与代理的处理程序相同的参数！

```
const toto = { a: 55, b:66 }const handler = {
   get(target, prop, receiver) {
   // Equal to target[prop]
   const value = Reflect.get(target, prop, receiver)
   if (!!value) {
      return value 
   }
   return `This ${prop} prop don’t exist on this object !` 
   },
   set(target, prop, value, receiver) {
   // Equal to target[prop] = value
   // Reflect.set return boolean, it’s perfect
   // since set handler need to return boolean
   return Reflect.set(target, prop, receiver)
   },
}const totoProxy = new Proxy (toto, handler)
```

因此，如您所见，代理和反射 API 是有用的，但您不会每天都使用它们。使用它们来制作陷阱或隐藏一些对象属性可能会很好。另一个解决方案是，比如符号。

如果你使用的是 Vue.js 框架，试着修改一个组件的 props 对象，它会触发一个来自 Vue 的警告日志，这个功能是使用代理完成的。:)

希望你喜欢这篇读物！

🎁你可以免费获得我的新书《javascript 中被低估的技能》,如果你在推特上关注我的话😁

或者在这里得到它

🎁[我的简讯](https://www.getrevue.co/profile/code__oz)

☕️你可以[支持我的作品](https://www.buymeacoffee.com/CodeoZ)🙏

🏃‍♂️，你可以跟着我👇

🕊 [推特](https://twitter.com/code__oz)

👨‍💻 [Github](https://github.com/Code-Oz)

你可以标记🔖这篇文章！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)