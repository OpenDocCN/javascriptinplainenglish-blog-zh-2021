# JavaScript 中移除/过滤数组(和对象数组)中的项目的 13 种方法

> 原文：<https://javascript.plainenglish.io/13-methods-to-remove-filter-an-item-in-an-array-and-array-of-objects-in-javascript-f02b71206d9d?source=collection_archive---------0----------------------->

## 最新 JavaScript 编码面试问答 2021

![](img/13c7682cbdd33a466f09d6daa34ff536.png)

Photo by [Daphné Be Frenchie](https://unsplash.com/@daphne_befrenchie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我创建了日常前端开发的技巧。

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

> 我知道小石头没什么区别，但如果我们有成千上万的石头，就有区别了，为此我明天会带新石头来。敬请期待😉

我们可能总会遇到这样或那样的方法，根据一个属性或多个属性值从一个或多个对象数组中删除项目。让我们看看基于属性值从数组中移除或过滤一个项的不同方法。

# 1.流行音乐

“`**pop()**`方法从数组中移除最后一个元素并返回该元素。此方法更改数组的长度。(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

**数组:**

```
let arraypoptest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testpop = arraypoptest.pop();console.log("array pop", testpop,"-", arraypoptest);
//10 - [2, 1, 2, 5, 6, 7, 8, 9, 9];
```

**对象数组:**

```
let users1 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testpop1 = users1.pop();console.log(
    "array of objects pop",
    JSON.stringify(testpop1),"-"
    JSON.stringify(users1)
);
//{"id":4,"name":"sara"} - [{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

# 2.变化

"`**shift()**`方法从数组中移除第**个**元素并返回移除的元素。此方法更改数组的长度。(来源: [MDN](https://developer.mozilla.org/en-US/docs)

**数组:**

```
let arrayshifttest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testshift = arrayshifttest.shift();console.log("array shift", testshift,"-", arrayshifttest);
//2 - [1, 2, 5, 6, 7, 8, 9, 9, 10]
```

**对象数组:**

```
let users2 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testshift1 = users2.shift();console.log("array of objects shift", JSON.stringify(testshift1),"-", JSON.stringify(users2));
//{"id":1,"name":"ted"} - [{"id":2,"name":"mike"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

# 3.薄片

“`**slice()**`方法将数组的一部分的浅表副本返回到从`start`到`end` ( `end`不包括在内)中选择的新数组对象中，其中`start`和`end`表示该数组中项目的索引。原始数组不会被修改。(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

**数组:**

```
let arrayslicetest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testslice = arrayslicetest.slice(0, 3);console.log("array slice", testslice, arrayslicetest); 
//not changed original array
//[2, 1, 2] - [2, 1, 2, 5, 6, 7, 8, 9, 9, 10]
```

**对象数组:**

```
let users3 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testslice1 = users3.slice(0, 3);console.log("array of objects slice", JSON.stringify(testslice1));
//not changed original array
//[{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

# 4.接合

"`**splice()**`方法通过移除或替换现有元素和/或在位置添加新元素[来更改数组的内容。"(来源:](https://en.wikipedia.org/wiki/In-place_algorithm) [MDN](https://developer.mozilla.org/en-US/docs) )

**数组:**

```
let arraysplicetest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testsplice = arrayslicetest.splice(0, 3);
```

**对象数组:**

```
let users4 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testspice1 = users3.splice(0, 3);console.log("array of objects splice", JSON.stringify(testsplice));
//[{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

# 5.使用拼接删除特定值

**数组:**

```
let arr = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];for (var i = 0; i < arr.length; i++) {
    if (arr[i] === 5) {
        arr.splice(i, 1);
    }
}console.log("splice with specific value", arr);*//[2, 1, 2, 6, 7, 8, 9, 9, 10]*
```

**对象数组:**

```
let users5 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];for (var i = 0; i < users5.length; i++) {
    if (users5[i].name === "ted") {
        users5.splice(i, 1);
    }
}console.log("splice with specific value array of objects",JSON.stringify( users5));//[{"id":2,"name":"mike"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

# 6.使用拼接-速记删除特定值

"`**splice()**`方法通过移除或替换现有元素和/或在位置添加新元素[来改变数组的内容。"(来源:](https://en.wikipedia.org/wiki/In-place_algorithm) [MDN](https://developer.mozilla.org/en-US/docs) )

`**indexOf()**`方法返回给定元素在数组中的第一个索引，如果不存在则返回-1(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

**数组:**

```
let arrShorthand = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0];let val = arr.indexOf(5);arrShorthand.splice(val, 1);console.log("splice shorthand specific value", arrShorthand);//*[1, 2, 3, 4, 5, 6, 7, 8, 9]*
```

**对象数组:**

```
let users6 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];var removeIndex = users6.map(item => item.id).indexOf(1);users6.splice(removeIndex, 1);console.log("splice shorthand specific value array of objects", JSON.stringify(users6));//[{"id":2,"name":"mike"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

# 7.过滤器

"`**filter()**`方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。"(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

**数组:**

```
let testarr = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testarr2 = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let filtered = testarr.filter(function(value, index, arr) {
    return value > 5;
});let filtered2 = testarr2.filter(item => item !== 2);console.log("filter example 1", filtered);//[6, 7, 8, 9, 9, 10]console.log("filter example 2", filtered2);//[1, 5, 6, 7, 8, 9, 9, 10]
```

**移除多个值的过滤器:**

```
let forDeletion = [2, 3, 5];let mularr = [1, 2, 3, 4, 5, 3];mularr = mularr.filter(item => !forDeletion.includes(item));console.log("multiple value deletion with filter", mularr);//[1, 4]
```

**对象数组:**

```
let users7 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let filterObj = users7.filter(item => item.id !== 2);console.log("filter example array of objects", filterObj);//[{"id":1,"name":"ted"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

# 8.删除运算符

JavaScript `**delete**`操作符从对象中删除属性；如果不再持有对同一属性的引用，它最终会自动释放。(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

```
let ar = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
delete ar[4]; // delete element with index 4console.log(ar);
//[2, 1, 2, 5, undefined, 7, 8, 9, 9, 10]
```

# 9.去除碘

`_remove`"从`array`中移除`predicate`返回 the 的所有元素，并返回移除元素的数组。谓词通过三个参数调用:*(值，索引，数组)*。(来源:[洛达什](https://lodash.com/docs/4.17.15))

**数组:**

```
let arrlodashtest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let evens = _.remove(arrlodashtest, function(n) {
    return n % 2 == 0;
});console.log("lodash remove array", arrlodashtest);//[1, 5, 7, 9, 9]
```

**对象数组:**

```
let users8 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let evensObj = _.remove(users8, function(n) {
    return n.id % 2 == 0;
});console.log("lodash remove array of object", JSON.stringify(evensObj));//[{"id":2,"name":"mike"},{"id":4,"name":"sara"}]
```

# 10.对象实用程序

方法返回一个给定对象自己的可枚举的字符串键属性对的数组，其顺序与 T2 循环提供的顺序相同(来源: [MDN](https://developer.mozilla.org/en-US/docs) )

```
const object = [1, 2, 3, 4];const valueToRemove = 3;const arrObj = Object.values(
    Object.fromEntries(
        Object.entries(object).filter(([key, val]) => val !== valueToRemove)
    )
);console.log("object utilites", arrObj); // [1,2,4]
```

# 11.洛达什过滤器

`_filter`"迭代`collection`的元素，返回所有元素的数组`predicate`返回 true。谓词由三个参数调用:*(值，索引|键，集合)*。(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let users10 = [{ id: 1, name: “ted” },{ id: 2, name: “mike” },{ id: 3, name: “bob” },{ id: 4, name: “sara” }];const lodashFilter = _.filter(users10, { id: 1 });console.log(“lodash filter”, JSON.stringify(lodashFilter));
//[{"id":1,"name":"ted"}]
```

# 12.无 lodash

`_without` "返回新的过滤值数组。"(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let lodashWithout = [2, 1, 2, 3];let lodashwithoutTest = _.without(lodashWithout, 1, 2);console.log(lodashwithoutTest);
//*[3]*
```

# 13.lodash 拒绝

`_reject`"与`[_.filter](https://lodash.com/docs/4.17.15#filter)`相反，这个方法返回`collection`的元素，而`predicate`不返回返回的真值。"(来源:[洛达什](https://lodash.com/docs/4.17.15))

```
let users9 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];const result = _.reject(users9, { id: 1 });console.log("lodash reject", result);
//[{"id":2,"name":"mike"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

你可以在这里玩 stackblitz。

[https://stackblitz.com/edit/array-remove-item](https://stackblitz.com/edit/array-remove-item)

# 你可以在这里查看我以前的文章:

*更多内容请看*[***plain English . io***](http://plainenglish.io/)