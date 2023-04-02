# JavaScript:如何深度克隆一个对象？

> 原文：<https://javascript.plainenglish.io/javascript-how-to-deep-clone-an-object-daa1ec29d216?source=collection_archive---------1----------------------->

## JavaScript 中对象的浅层克隆和深层克隆。此外，学习如何用 JavaScript 为 Object.assign 特征编写聚合填充。

```
**newObject = JSON.parse(JSON.stringify(oldObject));** 
```

这是 JavaScript 中克隆对象的唯一方法吗？

让我们来看看…

![](img/129a3609514dc99c5a69ef7e93135978.png)

Clone an object in Javascript

用 JavaScript 克隆对象总是一件棘手的事情。主要是因为对象通常由用户定制，具有任意集合。这使得任何人都很难想出一个现成的克隆对象的解决方案。

还有，JSON 的使用并不是在任何地方都是可取的。为什么？JSON 往往会丢失代码中使用的 JavaScript 数据类型。这意味着，在 JSON 中没有与 null/NaN/undefined or 函数等价的函数。

因此，

```
JSON.parse(JSON.stringify({a:null,b:NaN,c:Infinity,d:undefined,e:function(){},f:Number,g:false}))
```

最终会回来，

```
{a: null, b: null, c: null, g: false}
```

虽然使用 JSON.parse 和 JSON.stringify 是最快的克隆方式，但它会丢失数据。只有在不使用类型化数组、稀疏数组、blobs、set、map、regExps、FileLists、ImageDatas、undefined、NULL、Infinity 或 Date 函数的情况下，才可以使用它。

作为一名开发人员，您需要始终关注那些不会重复发明轮子的方法。而且，许多库确实考虑到对象必须被克隆的事实。这意味着，你需要好好看看你正在使用的库。看看您是否有克隆对象的简单方法——首先！

在 JavaScript 中，克隆可以分为两种类型:浅层克隆和深层克隆。让我们试着去理解每一个类别。

# 浅层克隆

**Object.assign** 用于创建 JavaScript 中任何对象的浅层克隆。根据定义，Object.assign()方法用于将所有可枚举的自身属性的值从一个或多个源对象复制到目标对象。

例如，如果您有一个对象，如下所示:

```
var parent = {a:1,b:{c:1,d:1}}
var shallow_clone = Object.assign({}, parent);//console shallow_clone
{a:1,b:{c:1,d:1}}
```

以上是父对象的浅层克隆。浅层克隆表示父对象的按位副本。子对象中的任何字段都是对父对象的引用。这意味着，子对象和父对象将共享相同的内存地址。因此，更改浅层克隆的值将会更改父克隆的值。

让我们试试下面的方法:

```
shallow_clone.d = 5
//executing the above line would change parent.d as well.
```

这就是为什么 Object.assign 被认为是创建对象浅层副本的一行程序。

# Object.assign 的聚合填充

以防您的浏览器不支持对象。赋值，您可以使用下面的代码片段来帮助您在代码中重新创建该功能。

```
Object.defineProperty(Object, '**assign**', {
    enumerable: false,
    configurable: true,
    writable: true,
    value: function(target) {
      'use strict';
      if (target === undefined || target === null) {
        throw new TypeError('First argument is empty');
      }

      var to = Object(target);
      for (var i = 1; i < arguments.length; i++) {
        var nextSource = arguments[i];
        if (nextSource === undefined || nextSource === null) {
          continue;
        }
        nextSource = Object(nextSource);

        var keysArray = Object.keys(nextSource);
        for (var nextIndex = 0, len = keysArray.length; nextIndex < len; nextIndex++) {
          var nextKey = keysArray[nextIndex];
          var desc = Object.getOwnPropertyDescriptor(nextSource, nextKey);
          if (desc !== undefined && desc.enumerable) {
            to[nextKey] = nextSource[nextKey];
          }
        }
      }
      return to;
    }
  });
```

## 传播算子

如果您使用的是最新版本的 JavaScript 库，可以使用 spread 运算符进行深度克隆。spread operator 刚推出的时候，很神奇。它似乎解决了 JavaScript 开发人员面临的许多问题。然而，随着时间的推移，使用 spread 操作符的缺陷逐渐显现。如果对象不是嵌套的，则展开操作符会创建一个深度克隆。但是，当您有嵌套对象时，spread 运算符会创建第一个级别的深层克隆，以及更深层别的浅层克隆。让我们用一个例子来理解这一点:

```
var parent =  [1,2,[3,[4,5]]]
var lets_clone = [...parent]
lets_clone[0] = 3 //works fine
lets_clone[2][1] = 3 //here the spread operator fails
```

# 深层克隆

接下来是深度克隆。**深度克隆的工作原理是为对象中的每个元素创建新的内存地址。**这意味着，新元素将独立于父元素。并且，改变一个不会影响另一个。

## 自定义功能

下面是我用 JavaScript 深度克隆一个对象的版本。

```
var object_create = Object.create;
if (typeof object_create !== 'function') {
    object_create = function(o) {
        function F() {}
        F.prototype = o;
        return new F();
    };
}function **deepClone**(src) {
    if(src === null || typeof(src) !== 'object'){
        return src;
    }

    //Honor native/custom clone methods
    if(typeof src.clone == 'function'){
        return src.clone(true);
    }

    //Special cases:
    //Date
    if(src instanceof Date){
        return new Date(src.getTime());
    }
    //RegExp
    if(src instanceof RegExp){
        return new RegExp(src);
    }
    //DOM Element
    if(src.nodeType && typeof src.cloneNode == 'function'){
        return src.cloneNode(true);
    }

    //Array
    if (Object.prototype.toString.call(src) == '[object Array]') {
        //[].slice() by itself would soft clone
        var ret = src.slice();

        var i = ret.length;
        while (i--) {
            ret[i] = deepCopy(ret[i]);
        }
        return ret;
    }

    //If we've reached here, we have a regular objectvar proto = (Object.getPrototypeOf ? Object.getPrototypeOf(src): src.__proto__);    
var dest = object_create(proto);
    for (var key in src) {
        //Note: this does NOT preserve ES5 property attributes like 'writable', 'enumerable', etc.
        dest[key] = deepCopy(src[key]);
    }
    return dest;
} 
```

在上面的`deepClone`函数中，我们支持多个场景。

1.  我们确保库的定制克隆功能不会被省略。
2.  我们首先检查要克隆的父对象是否是一个对象。
3.  我们检查功能。
4.  我们也检查数组。
5.  我们还会处理像“约会”这样的特殊情况。

与递归解决方案(在 JavaScript 中通常很昂贵)相比，上述函数被证明更平滑、更简洁。

# 结论

不管是不是 JavaScript——在任何编程语言中，开发人员都需要对变量的处理方式有信心。在克隆的情况下，这是程序员常用的功能，确保每个变量都存储在唯一的内存位置是很重要的。这时，创建副本和保持数据完整变得简单多了。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)