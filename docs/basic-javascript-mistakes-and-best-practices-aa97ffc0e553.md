# 常见的 JavaScript 错误和最佳实践

> 原文：<https://javascript.plainenglish.io/basic-javascript-mistakes-and-best-practices-aa97ffc0e553?source=collection_archive---------1----------------------->

![](img/40c9794f22508b57710b7d699992d342.png)

Photo by [Kenny Eliason](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文面向所有人，无论您是初学者、中级还是高级 JavaScript 开发人员。在这里，我们讨论了许多 JavaScript 开发人员正在犯的一些非常基本的错误。

关于 javascript 有一些误解。尤其是对于 JavaScript 中的迭代器。开发人员对于迭代器的选择非常模糊，并且忘记了使用它们的全部目的。

我们一会儿将研究这些错误，但是让我们谈谈循环和迭代器之间的主要区别。

等等，什么？两者不是一样的吗？

你通常不会把它们归类为不同的，但是这里有一个小问题。

# **循环与迭代器**

![](img/f7eeac9ac29e8b975eaeb3c1e8cd2962.png)

Loop Vs Iterator

在 JavaScript 中，我们有各种各样的循环和迭代器。我们有 **for，while 和 do…while 循环**，我们也有很多**迭代器，比如 for-each，map，filter，reduce** 等等。

让我们再多谈谈循环。

在一个循环中，我们可以确定循环的初始值。此外，与迭代器不同，循环允许您确定增量变量的值，这可能有助于您在使用元素时跳过它的编号。

迭代器只是一次从头到尾迭代一个数组的每个元素，并根据逻辑进行适当的操作。

# **无意义的“地图”**

听起来很奇怪？

在 JavaScript 领域，我们有多种迭代器选项，但它们都是为某种用例设计的。

实际上，我遇到过多次代码审查，在那里我看到人们在地图函数中使用`push()`。让我给你看一个例子，以便更好地理解。

```
const extraThirdArray= [];postList.map(ele => {
   const showDetails = ele.showDetails; //Resulting in boolean value
   const postData = getPost(ele.id, showDetails);
   extraThirdArray.push(postData);
});// **getPost()** will get post. If the second params showDetails is true then it will send some additional details to it otherwise it returns some basic details fot the post.
```

还有几个例子，但我希望你能理解。在这个例子中，在地图中使用`push()`是没有意义的。

Map 返回一个由从 map 返回的任何值组成的新数组。map 函数本身映射该值并将其保存在其数组中。使用 map 时，创建额外的数组并在其中推送元素是没有意义的。

地图功能会帮你完成。这是使用地图的主要目的。

```
const postData = postList.map(ele => {
   return getPost(ele.id, ele.showDetails);
});
```

或者

使用速记😍

```
const postData = postList.map(ele => getPost(ele.id, ele > 2));
```

# 最佳实践

## 1.可避免的条件语句

让我们来看看一些很容易避免的情况。

**(i)我们真的需要检查确认数组长度的条件吗？**

```
if(arr.length > 0) {
  //Some logic
}
```

我们有一个很好的方法来处理这个问题，而不是像大于 0 这样不必要的检查。

👉**更好的解决方案**

```
if(arr.length) {
  // Some logic
}
```

***为什么？*** 🧐

如果数组中存在除 0 之外的长度，它将为真，因此满足 If 条件。

**(ii)用下面的方法检查数组是否没有长度？**

```
if(arr.length <=0) {
  //Some logic
}
```

👉**更好的解决方案**

```
if(!arr.length) {
  //Some logic
}
```

***为什么？*** 🧐

JavaScript 中的数组不能有负长度。只有当它为 0 时才可能是假的，反之亦然。

**(iii)验证数组长度只是为了迭代它？**

许多开发人员使用 *if 条件*来检查数组是否有长度，然后为了不破坏代码而遍历数组。

```
let postIds = [];
if(arr.length) {
   postIds = arr.map(e => e.id)
}
```

👉**更好的解决方案**

```
const postIds = (arr || []).map(e => e.id);
```

***为什么？*** 🧐

将默认值指定为空数组将防止代码被破坏。如果有任何假值，如 undefined 或 null，它将返回到默认值。

## **2。不要不必要地使用三元运算符**

有时，在满足条件的情况下，需要将变量设置为 true，反之亦然。开发人员使用三元运算符来实现同样的目的。

```
const needPostDetails = post.created_at > date ? true : false;getPost(id, needPostDetails);
```

👉**更好的解决方案**

```
getPost(id, post.created_at > date);
```

***为什么？*** 🧐

在这种情况下，***post . created _ at>date***满足则返回 true，不满足则返回 false。您不需要特殊的条件，如使用三元运算符来实现这一点。

## **3。想要从对象中移除关键点吗？**

嗯，从对象中删除或移除键取决于具体情况。如果你想操作同一个对象，你可以像我们通常做的那样使用 *delete* 关键字。

```
const obj = {
   a:1,
   b:2,
   c:3,
   d:4,
   e:5,
   f:6,
   g:7
}delete obj.e;
delete obj.f;
delete obj.g;
delete obj.a;console.log(obj);Output:*const obj = {*
     b:2,
     c:3,
     d:4, *}*
```

👉**更好的解决方案**

```
const {e,f,g,a, ...rest} = obj;console.log(rest);Output:*const obj = {*
     b:2,
     c:3,
     d:4, *}*
```

***为什么？*** 🧐

一个更好的解决方案是使用 rest 操作符，而不是多次使用 **delete** 关键字，因为你不需要多次使用 delete 来删除你想要删除的键。使用 rest 操作符也不会操作您现有的对象；相反，它提供了它的一个浅表副本。

## **4。从数组中删除重复值**

```
const arr = [1,3,4,2,3,1,3];
const uniqueValue = arr.filter((value, index, self) => {
    return self.indexOf(value) === index;
});console.log(uniqueValue);Output:
[1, 3, 4, 2]
```

👉**更好的解决方案**

```
const uniqueValue = [...new Set([...arr])];console.log(uniqueValue);Output:
[1, 3, 4, 2]
```

***为什么？*** 🧐
更好的解决方案可以在这里使用一套。集合本身只包含唯一的值。我们可以利用它的本性来达到我们的目的。

我希望你喜欢这篇文章，并从中学到一些东西。你可以随时在社交媒体上联系我，寻求任何建议或意见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***