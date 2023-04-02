# 在 JavaScript 中查找数组(和对象数组)中的项目的 12 种方法

> 原文：<https://javascript.plainenglish.io/12-methods-for-finding-an-item-in-an-array-and-array-of-objects-in-javascript-84c7d46d85bd?source=collection_archive---------18----------------------->

我一直喜欢像报纸这样能在短时间内提供足够信息的东西。在这里，我为日常的前端开发创建了一些技巧，也有类似的目标。

![](img/7047c0a00c5381ded0a7cccb626f1b44.png)

Photo by [Edi Libedinsky](https://unsplash.com/@supernov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是一篇新文章，介绍了从数组和对象数组中删除重复项的一些方法。这些技巧可以成为你在 2021 年成功渡过 JavaScript 编码面试这条河的一个小石头。

> 我知道小石头没多大作用，但如果我们收集成千上万块这样的石头，它们就会有所不同。为此，我明天会带来新的石头。敬请关注。😉

我们可能总会遇到从数组或对象数组中查找、过滤和搜索项目的方法。下面是我们可以从中找到、过滤和搜索的五种不同方式。

*让我们创建将在文章中使用的测试数据。*

**测试数据:**

```
var users = [{ id: 1, name: "ted" },{ id: 1, name: "ted" },{ id: 1, name: "bob" },{ id: 3, name: "sara" },{ id: 4, name: "test" },{ id: 4, name: "test" },{ id: 5, name: "abc" },{ id: 6, name: "abc" },{ id: 7, name: "test2" },{ id: 8, name: "test1" },{ id: 8, name: "test1" }];var array = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
```

# 布尔结果

1.  **包括**

该方法确定一个数组的条目中是否包含某个值，根据情况返回`true`或`false`(来源: [MDN](https://developer.mozilla.org/)

```
console.log(array.includes(2)); // returns true
```

2.**每隔**

`**every()**`该方法测试数组中的所有元素是否都通过了由提供的函数实现的测试。它返回一个布尔值。(来源: [MDN](https://developer.mozilla.org/) )

```
let testevery1 = array.every(val=> val>3);let testevery2 = users.every(val=> val.id>3);console.log("array every",testevery1);console.log("array of objects every",testevery1);
```

3.**有的**

`**some()**`该方法测试数组中是否至少有一个元素通过了由提供的函数实现的测试。它返回一个布尔值。(来源: [MDN](https://developer.mozilla.org/) )

```
let testsome1 = array.some(val=> val>3);let testsome2 = users.some(val=> val.id>3);console.log("array some",testsome1);console.log("array of objects some",testsome2);
```

4.**lodash**

`**_includes**`检查`value`是否在`collection`中。如果找到`value`则返回`true`，否则返回`false`。(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let lodashtest9 =_.includes(array, 1);console.log("lodash includes 1 ",lodashtest9)let lodashtest10 =_.includes(array, 3, 2);console.log("lodash includes 2 ",lodashtest10);let lodashtest11 =_.includes({ 'a': 1, 'b': 2 }, 1);console.log("lodash includes 3 ",lodashtest11);let lodashtest12 =_.includes('abcd', 'bc');console.log("lodash includes 4 ",lodashtest12);
```

# 索引结果

6. **findIndex**

该方法返回数组**中满足所提供的测试函数**的第一个元素的**索引**。否则返回`-1`，表示没有元素通过测试。”(来源: [MDN](https://developer.mozilla.org/) )

```
let  testindex = array.findIndex(val => val > 1);console.log("array  findindex",testindex);let  testindex2 = users.findIndex(val => val.id > 1);console.log("array of objects findindex",testindex2);
```

7.**索引之**

`**indexOf()**`该方法返回给定元素在数组中的第一个索引，如果不存在则返回-1(来源: [MDN](https://developer.mozilla.org/) )

```
let testindexOf = array.indexOf(2);console.log("array index of",testindexOf);
```

8. **lastIndexOf**

`**lastIndexOf()**`该方法返回指定值最后一次出现的调用`[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)`对象内的索引，从`fromIndex`开始向后搜索。如果找不到该值，则返回`-1`。(来源: [MDN](https://developer.mozilla.org/) )

```
let testLastindexOf = array.lastIndexOf(2);console.log("array last index of",testLastindexOf);
```

9.**lodash**

“`**_.indexOf the**` 方法获取在`array`中第一次出现`value`的索引。如果`fromIndex`为负，则作为从`array`末端的偏移量。(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let lodashtest13 = _.findIndex(users, function(o) { return o.name == 'ted'; });console.log("find index lodash 1",lodashtest13);let lodashtest14 =_.findIndex(users, { 'name': 'ted', 'id': 1 });console.log("find index lodash 2",lodashtest14);let lodashtest15 =_.findIndex(users, ['id', 1]);console.log("find index lodash 3",lodashtest15);let lodashtest16 =_.findIndex(users, 'id');console.log("find index lodash 4",lodashtest16);let lodashtest17 =_.findIndex(array, (e) => {return e > 1;}, 0);console.log("find index lodash array",lodashtest17);
```

## 价值结果

10.**找到**

该方法返回所提供的数组中满足所提供的测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`(来源: [MDN](https://developer.mozilla.org/) )

```
let testfind = array.find(el => (el > 2));console.log("array find",testfind)let testfind2 = users.find(el => (el.id > 2));console.log("array of objects find",testfind2);let filterValue = (users, key, value)=> users.find(v => v[name] === 'name');console.log("find elements",filterValue)
```

11.**过滤器**

"方法**的`**filter()**`创建一个新的数组**，其中所有通过测试的元素都由提供的函数实现。"(来源: [MDN](https://developer.mozilla.org/) )

```
let testfilter1 = array.filter(val=> val>3);let testfilter2 = users.filter(val=> val.id>3);array.filter((item, index, array) => {console.log("index item array",index,item,array);})console.log("array filter",testfilter1);console.log("array of objects filter",testfilter2);
```

12.**地图**

"`**map()**`方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。"(来源: [MDN](https://developer.mozilla.org/) )

```
let val = [];let val2 = [];array.map(item => { if(item >= 3) val.push(item); });users.map(item => { if(item.id >= 3) val2.push(item); });console.log("map array",val);console.log("map  of objects",val2);
```

12.**洛达什**

“`**_.find**` 方法迭代`collection`的元素，返回第一个元素`predicate`返回 true。谓词由三个参数调用:*(值，索引|键，集合)*。(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let lodashtest1 = _.find(users, function(o) { return o.id < 2; });console.log("loadsh find 1 ",lodashtest1)let lodashtest2 =_.find(users, { 'id': 1, 'name': 'ted' });console.log("loadsh find 2 ",lodashtest2)let lodashtest3 = _.find(users, ['name', 'sara']);console.log("loadsh find 3 ",lodashtest3)let lodashtest4 =_.find(users, 'name');console.log("loadsh find 4 ",lodashtest4)
```

12.**罗达什**

该方法迭代`collection`的元素，返回所有元素的数组`predicate`返回 true。谓词由三个参数调用:*(值，索引|键，集合)*。(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let lodashtest5 = _.filter(users, function(o) { return o.id === 1; });console.log("loadsh filter 1 ",lodashtest5)let lodashtest6 = _.filter(users, { 'id': 1, 'name': 'ted' });console.log("loadsh filter 2 ",lodashtest6)let lodashtest7 =_.filter(users, ['name', 'ted']);console.log("loadsh filter 3 ",lodashtest7)let lodashtest8 = _.filter(users, 'name');console.log("loadsh filter 4 ",lodashtest8)
```

# 你可以在这里查看我以前的文章:

*更多内容请看*[***plain English . io***](http://plainenglish.io/)