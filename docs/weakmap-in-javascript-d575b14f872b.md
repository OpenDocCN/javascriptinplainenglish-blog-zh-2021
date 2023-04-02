# JavaScript 中的 Weakmap

> 原文：<https://javascript.plainenglish.io/weakmap-in-javascript-d575b14f872b?source=collection_archive---------14----------------------->

![](img/ea3fe0d9dcf6dd9775f623d4a355a074.png)

## 理解弱引用和强引用的区别，记住我们的垃圾收集器！

```
let obj = { name: ‘toto’ }// The object { name: ‘toto’ } can be accessed
// since obj has the reference to it// overwrite the reference
obj = null// the object will be removed from the memory
// since we have lost all reference on it
```

另一个例子，

```
let obj = { name: ‘toto’ }
let arr = [ obj ]obj = null
```

在本例中，对象`{ name: 'toto' } '不会被删除，因为数组保留了对它的引用！

## 强引用和弱引用的区别是什么？

事实上，JavaScript 中的大多数变量都保留了对一个对象的强引用。例如，上面的数组保存了一个对对象 **({ name: 'toto' })** 的**强**引用。

如果任何变量保持一个对该对象的**强引用**，该对象将不会被垃圾收集器移除。但是如果只有变量保持对对象的弱引用，它将被垃圾收集器删除。

一些变量类型对一个对象有一个弱引用，这就是 Weakmap 的情况。

## Weakmap

weakmap 是一个额外的数据存储，它可以允许我们从外部扩展一个对象(第三方库)或密封对象，而不需要推断垃圾收集器！或者聪明地创建一个缓存功能！

别慌，我会解释给你看这是什么意思！在我们比较 map 和 weakmap 之前。

## 地图对地图

使用 map，对象占用内存，可能不会被垃圾收集。映射有一个对对象的强引用。

```
let obj = { name: ‘toto’ }
let mapObj = new Map()
mapObj.set(obj, ‘any value’)obj = null
mapObj.size() // 1
```

Weakmap 完全不同，它不阻止关键对象的垃圾收集。

第一条规则: weakmap 只接受“object as key ”;**其次**，它只保留对对象的弱引用。

```
let obj = { name: ‘toto’ }
let weakmapObj = new WeakMap()
weakmapObj.set(obj, ‘any value’)obj = null
weakmapObj .size() // 0
```

该对象被垃圾收集器移除，因为 weakmap 只有一个对对象*{ name: 'toto' }*的**弱引用**，并且该对象不再有强引用(只有变量 obj 保留了对它的引用)。

## 什么时候用这个？

如你所见，Weakmap 很强(没错，是个玩笑)但不是每次都能用。只能在少数情况下使用。

**缓存功能**

```
const cache = new WeakMap()const process = function (obj) { 
 // If the input is not already cached 
 if (!cache.has(obj)) { 
 // Imagine a function that need a lot of memory/ressource 
 // We don’t want to re-execute bigOperation function
 // if the input is the same ! 
 const result = bigOperation(obj) 
 // So we execute the function one time and
 // we store the result in cache ! 
 cache.set(obj, result) 
 } 
 return cache.get(obj) 
}let obj = { /* any object */ } 
// first time we don’t have this input as cache, so we will put into 
const firstResult = process(obj) 
// second time we don’t need to execute the big function, 
// just need to exctract the result in cache 
const secondeResult = process(obj) 
// the original object will be removed from weakmap ! 
obj = null 
```

有了地图，这个缓存函数应该把 obj 保存在内存中。它会导致内存泄漏！

当我们保存一个对未使用对象的引用时，就会产生内存泄漏，所以如果你不再使用任何对象，就删除对它的任何变量引用！

⚠️我们不能用*。keys() /。values() /。因为我们不知道垃圾收集器什么时候会删除对象！*

**最后一个例子**

无内存泄漏的动态访问计数器

```
// Counter of visits
let visitsCountMap = new WeakMap()// increase the visits count
function countUser(user) {
 const count = visitsCountMap.get(user) || 0
 visitsCountMap.set(user, count + 1)
}let toto = { name: “toto” }countUser(toto) // count his visits// later toto leaves us
toto = null 
```

*注:本文灵感来自*[*https://javascript.info/weakmap-weakset*](https://javascript.info/weakmap-weakset*)

希望你喜欢这篇读物！

🎁如果你在[推特](https://twitter.com/code__oz)上关注我并给我打电话，你可以免费得到我的新书**被低估的 javascript 技能，改变现状**😁

或者得到它[这里](https://codeoz.gumroad.com/l/RXLYp)

🎁[我的简讯](https://www.getrevue.co/profile/code__oz)

☕️你可以[支持我的作品](https://www.buymeacoffee.com/CodeoZ)🙏

🏃‍♂️，你可以跟着我👇

🕊 [推特](https://twitter.com/code__oz)

👨‍💻 [Github](https://github.com/Code-Oz)

你可以标记🔖这篇文章！

*更多内容看* [***说白了. io***](http://plainenglish.io/)