# 6 个 JavaScript 一行程序来转换对象和数组

> 原文：<https://javascript.plainenglish.io/6-javascript-one-liners-to-transform-objects-and-arrays-ab3b47459b9b?source=collection_archive---------11----------------------->

## 我经常用来呈现数据可视化的代码片段的编译列表。

由于我作为数据分析师的工作性质，我的大量 web 应用程序项目不可避免地涉及到**数据可视化用例**。不出所料，许多呈现的前端组件包括**图表和地图**——例如 [Choropleth 地图](https://datavizcatalogue.com/methods/choropleth.html)或交通路线，所有这些都需要数据对象和数组的前端操作。

![](img/22905ad2012d8ac6bf6c3234f31a2382.png)

Illustration by Author | An example of chart and map visualisations in 1 of my school assignments a few years ago | Currently deployed at [IS Mafia : : VA Project](http://ismafia.herokuapp.com/)

因此，用简单的方法将 JavaScript 对象和数组转换成它们想要的最终状态节省了我在数据转换过程中的大量时间和精力。希望通过分享这些代码片段，其他人也能发现它们适用于他们的用例。

## 1.深层复制对象

`**var copiedObj = JSON.parse(JSON.stringify(obj))**;`

**解释:**在 JavaScript 对象中，复制一个对象变量会导致只复制对同一个对象的引用。因此，对其嵌入的密钥对值的任何更改都会导致对原始对象变量的更改。

```
var obj = { a: 1, b: 2 };
var copiedObj = obj;
copiedObj.a = 2;

console.log(copiedObj); // {a: 2, b: 2}
console.log(obj); // {a: 2, b: 2}
```

为了防止对原始对象进行更改，考虑使用以下命令来深层复制一个对象变量*(注意，对新对象变量的更改不再改变原始对象中的元素)*:

```
var obj = { a: 1, b: 2 };
var copiedObj = JSON.parse(JSON.stringify(obj));
copiedObj.a = 2;

console.log(copiedObj); // { a: 2, b: 2 }
console.log(obj); // { a: 1, b: 2 }
```

## 2.将多个对象合并成一个

```
var mergedObj = { 
  ...obj1, 
  ...obj2 
};
```

**解释:**对于大多数 web 程序员来说，(`**...**` ) spread 运算符可以说是 ES6 中引入的最有用的运算符之一。

单个物体如`var **obj1** = { a: 1, b: 2 }`也可以表示为`var obj = { **...obj1** }`

因此，如果有另一个对象`var **obj2** = { c: 1, d: 2 }`需要与`**obj1**`合并，下面的代码将产生期望的结果:

```
var mergedObj = { 
  ...obj1, 
  ...obj2 
};
// { a: 1, b: 2, c: 1, d: 2 }
```

## 3.将多个数组合并成一个

```
var mergedArr = arr1.concat( arr2, arr3 );
```

**解释:**当您希望合并多个数组时，`**concat**`将是一种方便的方法:

```
var arr1 = [1,2,3];
var arr2 = [4,5];
var arr3 = [6];
var mergedArr = arr1.concat( arr2, arr3 ); // [1, 2, 3, 4, 5, 6]
```

## 替代方法:使用(`…`)扩展操作符来连接数组

类似于在**点 2** 中如何使用(`**...**`)，这也可以应用于数组而不是对象:

```
var arr1 = [1,2,3];
var arr2 = [4,5];
var arr3 = [6];
var mergedArr = [ ...arr1, ...arr2, ...arr3 ]; // [1, 2, 3, 4, 5, 6]
```

## 4.移除数组的第一个元素

```
arr.shift();
```

**解释:**与其遍历整个数组并将除了第**个元素**之外的所有元素转移到一个新初始化的数组(`[]`)中，不如直接使用`**shift**`:

```
var arr = ["first", "second", "third", "forth"];
arr.shift();
// result of arr is: ["second", "third", "forth"]
```

## 5.移除数组的最后一个元素

```
arr.pop();
```

**解释:**类似于**点 4** ，不需要遍历整个数组，将除**最后一个元素**之外的所有元素转移到一个新初始化的数组中(`[]`，只需使用`**pop**`:

```
var arr = ["first", "second", "third", "forth"];
arr.pop();
// result of arr is: ["first", "second", "third"]
```

## 6.移除对象键和值对

```
delete obj[keyValue];
```

**解释:**有时你想从一个对象中完全删除一个密钥对值，而不是遍历该对象并将其分配给另一个空对象(`{}`)，只需使用`**delete**`关键字:

```
var obj = { id: 1, name: "ABC Primary School", category: "school" };

// assuming keyValue = "category":
delete obj["category"] 
// obj now becomes { id: 1, name: "ABC Primary School" }
```

**这就是我列出的用于对象和数组转换的 6 个 JavaScript 一行程序的全部内容(希望这足够简单明了:P)。**

## 个人评论

类似于我以前发表的一篇文章:

[](/6-useful-javascript-code-snippets-91424efd1c55) [## 6 个有用的 JavaScript 代码片段

### 这个列表可能很主观，但我还是分享了我自己的版本。示例和代码。

javascript.plainenglish.io](/6-useful-javascript-code-snippets-91424efd1c55) 

每个作者基于他/她的用例类型都有不同的建议列表，所以没有“绝对”或“正确”的列表。只需 **应用最适合你日常项目的列表。🙃**

## 非常感谢你坚持到这篇文章的结尾！❤希望你已经发现这很有用，如果你想要更多的数据分析&网络应用相关的内容，请随时[关注我。会非常感激😀](https://medium.com/@geek-cc)

[](https://geek-cc.medium.com/membership) [## 通过我的推荐链接加入灵媒——李思欣·崔

### 获得李思欣·崔和其他作家在媒体上的所有帖子！😃您的会员费直接…

geek-cc.medium.com](https://geek-cc.medium.com/membership) 

# (可选)最后但同样重要的是，请随意给我买杯咖啡 ☕(它真的会帮我度过朝九晚六的工作，哈哈)。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)