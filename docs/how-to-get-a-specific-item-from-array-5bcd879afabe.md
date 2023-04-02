# 如何从数组中获取特定的项

> 原文：<https://javascript.plainenglish.io/how-to-get-a-specific-item-from-array-5bcd879afabe?source=collection_archive---------7----------------------->

## JavaScript 备忘单 2021

## 每日 JavaScript 优化提示、技巧和最佳实践 2021

![](img/d73f1eb8e2368feb14dbcf6920df4917.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

我知道小石头没什么区别，但是如果我们有成千上万的石头，就有区别了..为此，我明天会带来新的石头。敬请关注。

开始今天的话题吧。

# 下面是一些在数组中查找项目的方法

1.  **includes:** 该方法确定数组的条目中是否包含某个值，根据情况返回`true`或`false`。

```
console.log(array.includes(2)); // returns true
```

2. **every:** 该方法测试数组中的所有元素是否通过了由提供的函数实现的测试。它返回一个布尔值。

```
let testevery1 = array.every(val=> val>3); //false
```

3. **some:** 该方法测试数组中是否至少有一个元素通过了所提供函数实现的测试。它返回一个布尔值。

```
let testsome1 = array.some(val=> val>3); //true
```

4. **lodash 包括:**检查`value`是否在`collection`中。如果找到了`value`，则返回`true`，否则返回`false`。

```
let lodashtest9 =_.includes(array, 1); // truelet lodashtest10 =_.includes(array, 3, 2); // false
```

5. **findIndex:** 该方法返回满足提供的测试函数的数组**中第一个元素的**索引**。否则返回`-1`，表示没有元素通过测试。**

```
let  testindex = array.findIndex(val => val > 1);
//0
```

6. **find:** 该方法返回所提供数组中满足所提供测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`。

```
let testfind = array.find(el => (el > 2));
//5
```

7。filter: 这个方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。

```
let testfilter1 = array.filter(val=> val>3);
//*[5, 6, 7, 8, 9, 9, 10]*
```

8.**映射:**这个方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。

```
let val = [];
array.map(item => { if(item >= 3) val.push(item); });
//*[5, 6, 7, 8, 9, 9, 10]*
```

你可以在这里查看 stackblitz。

[https://stackblitz.com/edit/find-item-array](https://stackblitz.com/edit/find-item-array)

# 在对象数组中查找项目

*   这些是可用于在对象数组中查找项目的方法。

1. **every:** 该方法测试数组中的所有元素是否通过了由提供的函数实现的测试。它返回一个布尔值。

```
let testevery2 = users.every(val=> val.id>3);
//false
```

2. **some:** 该方法测试数组中是否至少有一个元素通过了所提供函数实现的测试。它返回一个布尔值。

```
let testsome2 = users.some(val=> val.id>3); //true
```

3. **lodash 包括:**检查`value`是否在`collection`中。如果找到了`value`，则返回`true`，否则返回`false`。

```
let lodashtest11 =_.includes({ 'a': 1, 'b': 2 }, 1);
//true
let lodashtest12 =_.includes('abcd', 'bc');
//true
```

4. **findIndex:** 该方法返回满足提供的测试函数的数组**中第一个元素的**索引**。否则返回`-1`，表示没有元素通过测试。**

```
let  testindex2 = users.findIndex(val => val.id > 1);
//3
```

5. **find:** 该方法返回所提供数组中满足所提供测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`。

```
let testfind2 = users.find(el => (el.id > 2));
//{"id":3,"name":"sara"}
```

6。filter: 这个方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。

```
let testfilter2 = users.filter(val=> val.id>3);
```

7. **map:** 这个方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。

```
let val2 = [];users.map(item => { if(item.id >= 3) val2.push(item); });
```

## 进一步阅读

*更多内容请看*[***plain English . io***](http://plainenglish.io)