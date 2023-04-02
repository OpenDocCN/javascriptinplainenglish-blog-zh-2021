# JavaScript:如何检查是否为空(字符串、对象和数组)

> 原文：<https://javascript.plainenglish.io/javascript-how-to-check-if-empty-strings-objects-and-arrays-5fef2087a1cb?source=collection_archive---------10----------------------->

你是否正在寻找一个内置的方法，可以返回**真**或**假**，检查**字符串。空()**？我们可能没有内置的方法，但是有几种方法可以实现这个功能。在这篇文章中，你将读到如何检查一个**字符串、对象**和**数组**是否为空。

![](img/8ca7c998ca1074f63b7b68108419e816.png)

Image from [Pixabay](https://pixabay.com/photos/paper-brush-color-palette-painting-3204064/).

那么，我们开始吧。

# 一根绳子

你会很感兴趣地知道，有这么多不同的方法可以用来检查一个字符串是否为空。关于编码的一件事是，你永远不应该做假设。千万不要假设变量有长度，而且是字符串。为了构建健壮的东西，您需要编写基于所有决策的方法，并且不做任何假设。

在 JavaScript 的例子中，你可以在字符串的原型中写一个方法来决定它是否为空。在我们的例子中，我将把这个方法命名为 isEmpty。而且，根据我们的需要，这个函数可以用下面的任何一个函数来填充。

```
String.prototype.**isEmpty** = function(){ 
  **to be filled**
}
```

这是检查字符串是否为空的最快的方法。您将使用求反运算符。

```
function A(str) {
  let r=1;
  if (!str)
    r=0;
  return r;
}
```

在下面的函数中，您将把字符串转换为原始的**布尔**数据类型。在这个转换过程中，结果要么是真，要么是假。**布尔值** (null)将为假。并且，**布尔值**(有效字符串)将为真。

```
function F(str) {
  let r=1;
  if(!Boolean(str))
    r=0;
  return r;
}
```

如果你确定变量是一个字符串，你可以使用 inbuild 方法 **length。**

```
function J(str) {
  let r=1;
  if(str.length <= 0)
    r=0;
  return r;
}function D(str) {
  let r=1;
  if(!str || 0 === str.length)
    r=0;
  return r;
}
```

我最老的一个帖子谈到了使用**“= =”**和**“= = =”**，如果你看过，你会意识到正确使用它们。然而，这里我们使用， **"== "和" ==="** 来检查字符串是否为空。很多时候，您会想知道输入是 null、未定义还是空的。如果变量应该有多种数据类型，你应该在 **"== "和" === "，**之间小心选择。

帖子链接:[https://JavaScript . plain English . io/vs-in-JavaScript-2977631 d00db](/vs-in-javascript-2977631d00db)

```
function B(str) {
  let r=1;
  if (str == "")
    r=0;
  return r;
}function C(str) {
  let r=1;
  if (str === "")
    r=0;
  return r;
}
```

下面的策略是检查字符串是否为空的最罕见的方法之一。而且，它确实有效。它既不是最快的也不是最慢的。

```
function G(str) {
  let r=1;
  if(! ((**typeof** str != '**undefined**') && str) )
    r=0;
  return r;
}
```

“trim”函数被证明是有用的，当你有一个多空格的字符串时，尤其是在两端。它将帮助你去掉空格，当输入仅仅是一个 **" <空格> "** 时，它也将帮助你得到正确的答案。这里再次需要注意的是。不能对 null 或未定义的变量使用“trim()”。您必须确定输入是一个字符串。否则，您最终会得到一个严重的错误。同样，在 **isEmpty** 原型中，你有很多使用 trim 的方法。这里，有几个让你开始。

```
function K(str) {
  let r=1;
  if(str.**length** === 0 || !str.**trim**())
    r=0;
  return r;
}function N(str) {
  let r=1;
  if(!str || !str.**trim**().**length**)
    r=0;
  return r;
}function O(str) {
  let r=1;
  if(!str || !str.**trim**())
    r=0;
  return r;
}function Q(str) {
  let r=1;
  if(!str || (str.**trim**()==''))
    r=0;
  return r;
}
```

最后，我们可以利用正则表达式来检查字符串是否为空。这些绝对是执行这项检查最慢的方法。当在 Chrome、Safari 和 Firefox 中测试时，正则表达式的使用大大增加了完成操作的时间。

```
function E(str) {
  let r=1;
  if(!str || /^\s*$/.test(str))
    r=0;
  return r;
}function H(str) {
  let r=1;
  if(!/\S/.test(str))
    r=0;
  return r;
}function M(str) {
  let r=1;
  if((/^\s*$/).test(str))
    r=0;
  return r;
}function L(str) {
  let r=1;
  if ( str.replace(/\s/g,"") == "")
    r=0;
  return r;
}
```

# 一个物体

我们下一个关注的领域是物体。如何判断一个对象是空的、空的还是未定义的？

判断一个对象是否为空的最快方法是使用 **for-in** 组合。

```
for(var i in object)
return false;
return true;
```

在 object 中使用方法总是很有趣。有几种方法可以帮助你检查对象是否为空。这些方法中的大多数比 **for-in** 循环慢 40%到 50%。以下集合按照从快到慢的顺序排序。

```
return Object.keys(obj).length === 0;return Object.entries(obj).length === 0;return Object.getOwnPropertyNames(obj).length === 0;return Object.keys(obj).length === 0 && obj.constructor === Object;
```

在某些情况下，我们选择将 for-in 循环与对象中的方法结合起来，以决定它是否为空。同样，这些不是最慢也不是最快的检查方式。这里有几种检查方法，在这个特定的集合中从最快到最慢。

```
{for(var prop in obj){
if(obj.hasOwnProperty(prop)){return false}
}}{for(var prop in obj){
if(obj.hasOwnProperty(prop)){return false}
}
return true;}{
for(const key in obj){
if(hasOwnproperty.call(obj,key)){
return false;}}
return true;}
```

最后，检查对象是否为空的最慢方法是:

```
return JSON.stringify(obj) === '{}';
```

大多数时候，我都有一个难题，要确定对象的某个特定属性是未定义的、空的还是空的。现在，问题变得更深入了，我们有几种方法来找到正确的解决方案。这个问题可以很容易地分为三种具体情况:

1.  对象由属性组成，并且属性的值不是“未定义的”。
2.  该对象由一个属性组成，其值为“未定义”。
3.  该对象根本没有属性。

已定义的成员和未定义的值之间有明显的区别。和一个未定义的成员。

使用**类型的<对象>。<属性>** 不会完全帮你找到答案。但是，你可以把它与**<对象>** 中的【属性】结合起来。

```
typeof obj.x === 'undefined' && !("x" in obj)**// {x:1} returns false****// { x: (function(){})() } returns false****// {} returns true**
```

检查属性是否未定义的另一种方法是使用 **void** 操作符。

```
let obj = {};
if(obj['x'] === **void** 0){}
```

# 阵列

在数组的情况下，在检查它是否为空之前，你需要做一个未定义的检查。如果数组未定义，并且如果使用。方法，将会产生错误。检查数组的简单方法是:

```
if(!Array.isArray(array) && !array.length)
```

在上面的行中，我们使用 Array.isArray()来检查参数是否是数组。这剔除了像 undefined、null 和任何不是数组的值。这也消除了看起来像数组的对象，例如，DOM 的 arguments 对象和 NodeList 对象。

接下来， **array.length** 将检查该值是否为真。因为前面的条件确保了它是一个数组，所以你不需要担心插入更多的严格比较，比如 **array.length！== 0 或 array.length！= 0**

# 结论

现在，我们已经想出了几种方法来决定一个**字符串**、**对象**或**数组**是否为空。如果你喜欢这篇文章，请分享，别忘了关注。

**延伸阅读:**

[](https://differ.plainenglish.io/p/how-to-check-for-an-empty-object-in-javascript-dvjxdkyal) [## 如何在 JavaScript 中检查空对象

### 在 JavaScript 中，空对象是没有属性或方法的对象。检查空对象是一种常见的…

different . plain English . io](https://differ.plainenglish.io/p/how-to-check-for-an-empty-object-in-javascript-dvjxdkyal) 

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****