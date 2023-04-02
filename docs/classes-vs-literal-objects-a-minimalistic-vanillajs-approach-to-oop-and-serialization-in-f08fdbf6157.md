# 类与文字对象:JavaScript 中面向对象和序列化的极简“香草 JS”方法

> 原文：<https://javascript.plainenglish.io/classes-vs-literal-objects-a-minimalistic-vanillajs-approach-to-oop-and-serialization-in-f08fdbf6157?source=collection_archive---------13----------------------->

![](img/9c1cc69bc074de5d350151663c6c9c7e.png)

Photo by [Jefferson Santos](https://unsplash.com/@jefflssantos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming-language?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

面向对象编程意味着识别和隔离具有特定属性和方法或功能的“代码工作者”,这些代码工作者相互交互和交换数据。

ECMAScript 2015，也称为 ES6，引入了 JavaScript 类。JavaScript 类是 JavaScript 对象的模板。这意味着引入像*类、静态、扩展*这样的关键字。

虽然使用类对于组织代码非常有用，但是在客户机-服务器环境中编程，尤其是在“web 无服务”架构中，首先需要在不同的应用程序或页面之间交换数据(即在浏览器内部运行的 javascript 客户机应用程序和 HTTP 服务或 API)。换句话说，不同的软件组件必须能够交换组成它们的对象(或者说数据),以便相互交流。这称为对象序列化。

## 序列化

在计算中，串行化是**将数据结构或对象状态转换成可以存储**(例如，在文件或内存数据缓冲区中)或传输(例如，通过计算机网络)并在以后重建的格式的过程。(【https://en.wikipedia.org/wiki/Serialization】*)*

## *使用 Javascript 文字对象的简单序列化方法*

> *对象文字是花括号内逗号分隔的名称-值对列表。下面是一个例子。*

```
***exports var room = {** *name*: 'kitchen',
 *floor*: 1,
 *measure*: 12,
 *sayHello(){*
  console.log(`Hello, i'm the ${this.name}`)
 *}***}***
```

***通过网络共享房间对象或在单页应用程序中路由***

*我要做的是将数据从方法中分离出来，并使用一个 extends(但您可以随意称呼它)方法来设置或获取序列化的 room 对象。**这将使房间对象成为一个具有许多对象数据的静态类。***

```
*export var room = {**extends(data){**
  return {
     name: data && data.name ? data.name : undefined
     floor: data && data.floor ? data.floor : undefined
     measure: data && data.measure ? data.measure : undefined
  }**},**

 sayHello(obj){
  console.log(`Hello, i'm the ${obj.name}`)
 }}*
```

> *请注意，extends 方法返回一个新对象(记住，当您创建一个对象*时，您给出的是对它的引用，而不是一个值*)。*

## *实际例子*

```
*let room1 = room.extends({name: 'kitchen'})
let room2 = room.extends({name: 'garage'})console.log(room.sayHello(room1)) //Hello, i'am the kitchen
console.log(room.sayHello(room2)) //Hello, i'am the garage*
```

**更多内容看* [***说白了. io***](http://plainenglish.io/)*