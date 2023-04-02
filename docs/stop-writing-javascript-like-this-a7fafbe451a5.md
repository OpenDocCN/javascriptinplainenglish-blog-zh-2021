# 不要再这样写 JavaScript 了

> 原文：<https://javascript.plainenglish.io/stop-writing-javascript-like-this-a7fafbe451a5?source=collection_archive---------0----------------------->

## 写出更好的 JavaScript 代码的 10 种方法

![](img/1c8c91af685d00ed1f3ea1de0dc7783b.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们大多数人都习惯长时间编写 JavaScript 代码。但是我们可能没有更新我们自己的新功能，这些新功能可以用最少的代码解决您的问题。这些技术可以帮助您编写干净和优化的 JavaScript 代码。今天，我将总结一些优化的 JavaScript 代码片段，它们可以帮助你提高技能。

# 1.多||条件 if 的简写

```
if (fruit === 'apple' || fruit === 'orange' || fruit === 'banana' || fruit ==='grapes') {
    //code
}
```

除了使用多个`||` (OR)条件之外，我们可以使用一个带有值的数组，并使用`includes()`方法。

```
if (['apple', 'orange', 'banana', 'grapes'].includes(fruit)) {
   //code
}
```

# 2.带有多个&&条件的 if 的简写

```
if(obj && obj.address && obj.address.postalCode) {
    console.log(obj.address.postalCode)
}
```

使用可选链接(`?.`)来替换此代码片段。

```
console.log(obj?.address?.postalCode);
```

# 3.null、undefined 和 empty if 检查的简写

```
if (first !== null || first !== undefined || first !== '') {
    let second = first;
}
```

与其写这么多检查，我们可以用`||`
(OR)运算符这样写更好。

```
const second = first || '';
```

# 4.开关盒的简写

```
switch (number) {
  case 1:
     return 'one'; case 2:
     return 'two'; default:
     return;
}
```

使用贴图/对象，以更简洁的方式书写。

```
const data = {
  1: 'one',
  2: 'two'
};//Access it using
data[num]
```

# 5.单行函数的简写

```
function doubleOf(value) {
  return 2 * value;
}
```

使用箭头功能将其缩短。

```
const doubleOf = (value) => 2 * value
```

# 6.有条件调用函数的简写

```
function area() {
    console.log('area');
}
function volume() {
    console.log('volume');
}if(type === 'square') {
    area();
} else {
    volume();
}
```

您可以这样写，而不是使用 if 来有条件地调用函数。

```
(type === 'square' ? area : volume)()
```

# 7.使用 if 设置默认值的简写

```
if(amount === null) {
    amount = 0;
}if(value === undefined) {
    value = 0;
}console.log(amount); //0
console.log(value); //0
```

您可以使用`||` (OR)运算符简单地编写相同的内容。

```
console.log(amount || 0); //0
console.log(value || 0); //0
```

# 8.if…else 的简写

```
let value;
if (num > 0) {
    value = 'positive';
} else {
    value = 'negative';
}
```

如果`if` … `else`条件不是那么复杂，那么我们可以用一个三元运算符来代替它。

```
const value = num > 0 ? 'positive' : 'negative';
```

# 9.在数组中循环时传统 for 循环的简写

```
const arr = [11, 22, 33];
for(let i=0; i<arr.length; i++) {
    console.log(arr[i]);
}
```

用`forEach`替换这个正常的`for`。

```
const arr = [11, 22, 33];
arr.forEach((val) => console.log(val));
```

# 10.将字符串数字转换为数字的简写方式

```
const num1 = parseInt("100");
const num2 =  parseFloat("11.11");
```

我们可以使用一个简单的`+`操作符，而不是使用`parseInt`和`parseFloat`以及其他类似的方法。

```
const num1 = +"100";
const num2 =  +"11.11";
```

# 结论

这些是我最喜欢的 JavaScript 速记技术。这些确实有助于开发者提高代码标准，所以如果你知道类似的速记技巧，请留下评论。感谢您的阅读，希望您发现这是有帮助的！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)