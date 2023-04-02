# 如何获取 JavaScript 数组中的所有唯一值

> 原文：<https://javascript.plainenglish.io/how-to-get-all-unique-values-in-a-javascript-array-ecb120f7131b?source=collection_archive---------11----------------------->

![](img/80af9c0c40190f146e183f4ca97f90d4.png)

Photo by [Johann Siemens](https://unsplash.com/@johannsiemens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从数组中移除重复的值是我们有时在 JavaScript 应用程序中不得不做的事情。

在本文中，我们将研究如何从 JavaScript 数组中获取所有唯一的值。

# 过滤方法

我们可以使用数组实例的`filter`方法来过滤掉任何发现的重复值。

例如，我们可以写:

```
const onlyUnique = (value, index, arr) => {
  return arr.indexOf(value) === index;
}const a = ['a', 1, 'a', 2, '1'];
const unique = a.filter(onlyUnique);
```

我们有`onlyUnique`函数，用作`filter`方法的回调。

`filter`方法的回调接受我们迭代的值作为第一个参数。

第二个参数是我们正在迭代的元素的索引。

`arr`是我们正在迭代的数组。

所以我们可以调用`indexOf`或`arr`来得到`value`的第一个实例的索引。

如果它与`index`不一样，那么我们知道它是一个重复值。

我们可以把函数传递到`filter`方法中，得到唯一的值。

因此`unique`为`[“a”, 1, 2, “1”]`

# 转换为集合并返回到数组

我们可以从数组中移除重复项的另一种方法是，将数组转换为集合，然后将该集合转换回数组。

我们可以用扩展运算符将集合转换成数组，因为集合是一个可迭代的对象。

例如，我们可以写:

```
const a = ['a', 1, 'a', 2, '1'];
const unique = [...new Set(a)];
console.log(unique)
```

我们用`Set`构造函数创建一个集合。

这将创建一个集合，其中不允许有重复的值。

因此，所有重复的值都将被删除。

然后，我们使用扩展运算符将集合转换回数组。

`unique`应与前值相同。

# 洛达什

Lodash 有`uniq`方法，返回一个去掉重复值的数组。

例如，我们可以写:

```
const a = ['a', 1, 'a', 2, '1'];
const unique = _.uniq(a)
console.log(unique)
```

从`a`中删除所有重复项。

# 结论

我们可以用集合和扩展运算符从数组中移除重复的项。

同样，我们也可以通过`filter`和`indexOf`方法进行同样的操作。

我们也可以使用 Lodash 从数组中移除重复的项目。

*多内容于* [***浅显易懂***](http://plainenglish.io)