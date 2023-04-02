# 零化合并运算符与逻辑 or 运算符

> 原文：<https://javascript.plainenglish.io/nullish-coalescing-vs-logical-or-63c4720667b8?source=collection_archive---------18----------------------->

## 找出 JavaScript 的区别？？(无效合并)和||(逻辑或)运算符。

![](img/2fa561d636ef7aa84db72603b369820b.png)

## [无效合并](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

JavaScript 提供了一个`??`操作符，可以用来在处理`undefined`和`null`时设置默认值。例如:

```
let v = undefined ?? "value"
console.log(v) //value
```

上面代码片段中`v`的值将是“value”。

## [逻辑 OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)

在处理`undefined`或`null`值时，`||`操作符也可用于设置默认值。例如:

```
let v = undefined || "value"
console.log(v) //value
```

上面代码片段中`v`的值将是“value”。

## 差异

逻辑“或”的一个“弱点”是它将像`0`、`NaN`、`""`这样的值解释为假值，从而返回其右边的操作数。

```
//Incorrect result
let calculatedChange = 0
let changeToGive = calculatedChange || 0.5
console.log(changeToGive) // 0.5
```

`changeToGive`实际上应该是`0`，但是`||`运算符将`0`解释为错误值，因此默认为`0.5`。

```
//Correct result
let calculatedChange = 0
let changeToGive = calculatedChange || 0.5
console.log(changeToGive) // 0
```

`??`避免了前述示例中`||`的意外行为。

希望您已经牢牢掌握了零化合并运算符和逻辑 or 之间的区别。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)