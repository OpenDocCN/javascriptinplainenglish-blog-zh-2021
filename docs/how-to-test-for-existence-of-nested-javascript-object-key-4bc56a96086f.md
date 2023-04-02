# 如何测试嵌套 JavaScript 对象键的存在？

> 原文：<https://javascript.plainenglish.io/how-to-test-for-existence-of-nested-javascript-object-key-4bc56a96086f?source=collection_archive---------2----------------------->

![](img/071442205d3b0fcdfd0a36ab372565ee.png)

Photo by [Samantha Lam](https://unsplash.com/@contradirony?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 对象通常嵌套在其他对象中。

此外，它们是动态的。

因此，我们可能需要检查对象中是否存在嵌套属性。

在本文中，我们将看看如何检查一个嵌套属性是否存在于一个对象中。

# 编写我们自己的函数

我们可以编写自己的 JavaScript 函数来检查对象中是否存在深度嵌套的属性。

例如，我们可以写:

```
const checkNested = (obj, ...props) => {
  for (const prop of props) {
    if (!obj || !Object.prototype.hasOwnProperty.call(obj, prop)) {
      return false;
    }
    obj = obj[prop];
  }
  return true;
}const obj = {
  level1: {
    level2: {
      level3: 'level3'
    }
  }
};console.log(checkNested(obj, 'level1', 'level2', 'level3'));
console.log(checkNested(obj, 'level1', 'level2', 'bar'));
```

我们用`obj`参数和`props` rest 参数创建了`checkNested`函数。

`obj`是我们正在检查的对象。

`props`有一个属性数组，它构成了我们要寻找的嵌套属性的路径。

在函数中，我们循环通过`props`数组来遍历`obj`以找到嵌套的属性。

为此，我们检查`obj`是否为 falsy 或者`hasOwnProperty`是否返回`false`。

如果其中任何一个是`true`，那么我们知道该属性不存在。

所以我们返回`false`。

我们用`Object.prototype.hasOwnProperty.call`而不是`obj.hasOwnProperty`调用`hasOwnProperty`，因为`obj.hasOwnProperty`可以被覆盖。

`call`取`hasOwnProperty`的`this`值。

`prop`是属性名字符串值。

如果我们通过了`if`模块，那么我们将`obj`分配给`obj[prop]`来更深入地查看。

我们可以这样做，因为属性是一个对象。

如果整个循环迭代成功，那么我们返回`true`,因为路径指向我们正在寻找的属性。

我们用`obj`对象测试这个函数，我们可以看到第一个控制台返回`true`。

而第二个果然返回`false`。

# 递归检查给定的属性

我们也可以用递归函数来做检查。

例如，我们可以写:

```
const checkNested = (obj, prop, ...restProps) => {
  if (obj === undefined) {
    return false;
  }
  if (
    restProps.length === 0 &&
    Object.prototype.hasOwnProperty.call(obj, prop)
  ) {
    return true;
  }
  return checkNested(obj[prop], ...restProps);
};const obj = {
  level1: {
    level2: {
      level3: "level3"
    }
  }
};console.log(checkNested(obj, "level1", "level2", "level3"));
console.log(checkNested(obj, "level1", "level2", "foo"));
```

这个`checkNested`功能和我们之前的那个差不多。

不同之处在于，我们从寻找的路径中获取第一个属性。

其余的留在数组中。

我们检查`restProp.length`是否为 0，以及`obj`是否具有`prop`属性。

如果它们都是`true`，那么我们返回`true`，因为我们遍历了整个路径并找到了属性。

如果在`restProps`中还剩下什么，那么我们调用`checkNested`向下钻一层。

我们应该得到和以前一样的结果。

# 可选链接运算符

检查嵌套属性路径是否存在的另一种方法是使用可选的链接操作符，它是用`?.`添加的。

该运算符是 ES2020 的新功能。

例如，我们可以写:

```
const obj = {
  level1: {
    level2: {
      level3: "level3"
    }
  }
};const value1 = obj?.level1?.level2?.level3;
const value2 = obj?.level1?.level2?.foo;
console.log(value1);
console.log(value2);
```

我们应该看到`value1`是`'level3'`并且`value2`是`undefined`，因为如果属性存在，操作符返回属性值，否则返回`undefined`。

这让我们减少了安全遍历深度嵌套属性所需的工作量。

# 结论

我们可以用自己的代码或可选的链接操作符来测试是否存在深度嵌套的 JavaScript 对象属性。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*