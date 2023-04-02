# 9 个没人谈论的 JavaScript 黑客

> 原文：<https://javascript.plainenglish.io/9-javascript-hacks-nobody-talks-about-f15445e301ca?source=collection_archive---------4----------------------->

## 减少工作量和编写简洁代码的特性和技巧。

![](img/57d34b145b7e5b9ed45ea7c6ff3a3fd8.png)

Photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 有相当广泛的应用，从 web 开发到机器学习再到应用程序开发。

幸运的是，JavaScript 提供了一个全面的有用特性列表，但是这些特性和技巧并不流行，也很少被提及。

有了如此大量的应用程序和用例，代码的复杂性也增加了，了解技巧和窍门肯定可以节省您大量的时间。

因此，我列出了 9 个没人谈论的 JavaScript 漏洞:

## 1.快速调整大小和清空数组

在编程时，我们经常需要改变或清空数组。

最有效的方法是使用`Array.length`方法。

```
const array = [1, 2, 3, 4, 5];
console.log(array); // 5array.length--;
console.log(array); // 4array.length += 15;
console.log(array); // 19
```

代码片段的输出将是:

```
[1, 2, 3, 4, 5]
[1, 2, 3, 4]
[1, 2, 3, 4, ..15 empty]
undefined
```

还可以通过将长度设置为 0 来移除数组的所有元素。

```
let arr= ['a', 'b', 'c'];arr.length = 0;console.log(arr.length); // Ouput=> 0
console.log(arr); // Output=> []
```

## 2.条件句的快捷方式

在编程过程中，当满足某个条件时，您可能需要某段代码。

例如，您可能希望向未登录的用户显示登录页面，而当用户登录时，您希望显示主页。

这种逻辑可以使用条件语句来实现。

```
var x=1;if(x==1){
    console.log(x)
  }
else{
    console.log("Error")
  }
```

然而，使用三元运算符(`?`和`:`)可以很容易地实现这种逻辑。

它有三个操作数:一个条件，后面跟一个`?`，如果条件为真，后面跟一个要执行的表达式，再后面跟一个`:`，如果条件为假，那么必须执行的表达式。

让我们看看代码来更好地理解它。

```
var x=1;
console.log( x==1? x: "Error"); //Output: 1
```

## 3.动态导入

导入模块的标准方式很简单，但是当您需要动态导入函数的时候呢？

```
import defaultExport from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
```

只有在满足某些条件时，您才需要导入一些特定的模块，这就是动态导入发挥作用的地方。

您可以使用`import`功能来动态导入模块。

要动态导入，使用关键字`import`作为函数，并传入模块名。

```
import('some-module')
     .then(obj => ...)
     .catch(err => console.log(err))
```

如您所见，它返回一个承诺，解析成一个模块对象。

虽然静态导入可用于导入关键和必要的模块，但动态导入有几个好处:

1.  静态导入会增加代码的加载时间，还会导致未使用的模块。
2.  静态导入说明符字符串不能动态生成。
3.  静态导入会导致不必要的内存使用。

## 4.零融合算子

零化合并算子(？？)可以节省很多时间，如果你需要检查一个值是否为空，如果是，那么就指定一个默认值。

这可以防止应用程序中不可预见的错误和意外行为。

```
const name = null ?? 'Anonymous';console.log(name); // Output=> 'Anonymous'const age= undefined?? 18;
console.log(bar); // Output=> 18
```

换句话说，当左侧操作数为`undefined`(或`null`)时，该运算符返回右侧操作数。

该运营商提供的巨大优势显而易见。

这不仅会产生更多无错的代码，还会有助于避免可能导致崩溃的意外活动。

值得注意的是，OR 运算符(||)也可以实现同样的功能。

```
let firstName = null; 
let lastName = null; 
let nickName = "Guest";  // shows the first truthy value: alert(firstName || lastName || nickName || "Anonymous"); //Guest
```

OR(||)和无效合并运算符(？？)略有不同，因为||运算符返回第一个真值，而？？运算符返回第一个指定值。

## 5.合并数组

数据集越大，合并两个数组所需的计算能力就越强。

最简单也是最常见的方法是使用`Array.prototype.concat()`法。

```
const array1 = ['a', 'b', 'c'];
const array2 = ['a', 'e', 'f'];
const array3 = array1.concat(array2);console.log(array3); 
// Output=> Array ["a", "b", "c", "a", "e", "f"]
```

然而，当处理海量数据集时，`Array.prototype.concat()`并不是最有效的选择，因为它创建了一个新数组，这是一个内存密集型任务。

在这种情况下，使用`Array.push.apply(arr1, arr2)`方法是更好的选择，因为它合并了两个数组而没有创建一个新的。

```
let list1 = ['a', 'b', 'c'];
let list2 = ['a', 'e', 'f'];list1.push.apply(list1, list2);
console.log(list1);
//Output=> Array ["a", "b", "c", "a", "e", "f"]
```

## 6.最小评估

如果要将一个变量赋给另一个变量，可能需要检查所赋变量的值是否不为空。

这个操作可以通过使用一个`if`语句来简单地执行，但是，使用多个条件评估来编写`if`语句可能会很麻烦，甚至可能导致错误。

```
if (var1 !== null || var1 !== undefined || var1 !=='') {
     var2 = var1;
}
```

但是实现这一点的简单方法是 JavaScript。

```
var2 = var1 || 'Some value';
```

## 7.默认参数值

您的应用程序可能会让用户选择输入自定义值或使用默认值。

这在利息计算器应用程序中很常见，除非用户提供不同的利率，否则使用默认利率，比如 6.5%。

同样，这个逻辑可以使用`if`语句简单地实现。

```
function calculator(principle,rate,time) {
  if (principle === undefined)
    principle = 5000;
  if (rate === undefined)
    rate = 6;
  if (time===undefined)
    time = 3;
  ....
}
```

实现这一点的简单方法实际上非常简单。

```
function calculator(principle=5000, rate=6, time=3){
   ...
}
```

您基本上是在函数声明本身中分配默认值。

## 8.`in` 操作员

如果你想检查一个指定的属性是否存在于一个对象或者它的原型链中，那么`in`操作符将会帮助你。

换句话说，`in`操作符使得检查一个定义的属性是否存在于一个对象或者它的原型链中变得更加容易。

```
const car = { make: 'Honda', model: 'Accord', year: 1998 };console.log('make' in car);
// expected output: truedelete car.make;if ('make' in car === false) {
  car.make = 'Suzuki';
}
console.log(car.make);
// expected output: "Suzuki"
```

该运算符返回`true` 或`false`。

当使用 DOM(文档对象模型)时，这个属性非常有用。

```
var q= "onrender" in  document.createElement("div");
if(q){
  ...
}
else{
  ...
}
```

你可以在这里阅读更多关于这个运营商[的内容。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)

## 9.强制参数检查

有时，你需要有某些价值观来成功地完成一项任务。

例如，当登录您的电子邮件帐户时，您必须提供电子邮件地址。

同样，在注册一些社交媒体平台时，您可能需要提供您的姓名、年龄、电子邮件和电话号码。这里，平台不能提供某种默认值。

从开发人员的角度来看，检查是否提供了强制值以及是否提供了`null`可能会变得令人厌烦，如果必须多次执行检查并且涉及多个这样的强制值，情况就更是如此。

```
function submitName(name) {
  if(name=== undefined) {
    throw new Error('Missing parameter');
  }
  return name;
}
```

幸运的是，快速检查参数值是否为空的简单方法是通过在这个列表上实现我们的#7 hack，即默认参数值。

您需要创建一个简单的抛出错误的函数来解决缺少参数的问题。

一旦创建了这个函数，就需要将它指定为强制参数的默认值。

```
mandatory = () => {
  throw new Error('Missing parameter');
}

submitName= (name= mandatory()) => {
  return name;
}
```

因此，如果没有提供默认参数，在我们的例子中是“name ”,那么抛出错误的函数`mandatory()`将被返回并执行。

这种方法也促进了[干(不要重复自己)](/5-habits-that-separate-great-developers-from-good-developers-bc7187e7529f#845b:~:text=1.%20Don%E2%80%99t%20repeat%20yourself.)原则。

## 结论

JavaScript 正越来越多地被用于各种各样的场景中，并且当谈到新的 JavaScript 框架时，似乎看不到尽头。

然而，所有这些框架和库的一个共同点是，它们都是基于 JavaScript 的，当尝试这些框架时，精通 JavaScript 总是有好处的。

你可以看看我最近的博客，里面有一些节省时间的现代技巧和窍门。

[](/5-modern-javascript-tips-and-tricks-to-save-time-7773aff6be26) [## 节省时间的 5 个现代 JavaScript 技巧和窍门

### 使用这些 JavaScript 技巧减少工作量并编写干净的代码

javascript.plainenglish.io](/5-modern-javascript-tips-and-tricks-to-save-time-7773aff6be26) 

完全掌握 JavaScript 是很困难的，如果不是不可能的话。

然而，通过不断学习新的技巧和特性，你一定会变得非常精通 JavaScript。

希望你喜欢阅读这篇文章！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)