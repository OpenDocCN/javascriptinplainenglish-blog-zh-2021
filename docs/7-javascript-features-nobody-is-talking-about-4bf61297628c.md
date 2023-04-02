# 你可能不知道的 7 个 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/7-javascript-features-nobody-is-talking-about-4bf61297628c?source=collection_archive---------10----------------------->

## 大多数人不知道 JavaScript 的这些不可思议的特性。

![](img/ef391b01e63f6382b06661d17636e5f4.png)

Photo by [Kristina Flour](https://unsplash.com/@tinaflour?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你认为你知道所有隐藏的、珍贵的 JavaScript 特性和技巧吗？

嗯，我以前也是这么想的，直到最近我开始特别留意那些很少被提及的有用的特性和技巧。

事实上，JavaScript 每年都在发展，引入了用几行代码完成复杂或繁琐的任务，但该语言的某些方面已经融入其中很多年了，然而，人们很少谈论它们。

尽管如此，这些特性可以帮助您克服我们在使用这种语言时遇到的一些最常见的问题。

以下是 7 个不太受欢迎的 JavaScript 特性:

## 1.动态导入

我们大多数人都习惯于导入模块的标准方式。从技术上讲，它是导入模块的静态方法。

```
import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
```

然而，没有多少人知道存在一种动态的导入模块的方法，也就是说，您可以根据自己的需求有条件地导入模块。

要动态导入，使用关键字`import`作为函数，并传入模块名。它将返回一个承诺，解析成一个模块对象。

```
import('some-module')
     .then(obj => ...)
     .catch(err => console.log(err))
```

尽管静态导入仍然是加载初始和重要模块的首选方式，但是动态导入提供了一些好处:

1.  静态导入会增加代码的加载时间，还会导致未使用的模块。
2.  静态导入说明符字符串不能动态生成。
3.  静态导入会导致不必要的内存使用。

## 2.模板文字

除非您知道并使用 React，否则您很可能不知道或不使用模板文字。

在 ES6 中引入的模板文字本质上让你的字符串文字表现得像类固醇一样。

下面是模板文字的一个例子。

```
let a = `Hello World! This is a template literal`;
```

请注意，我们使用了反斜线代替单引号或双引号来换行。

模板文字具有以下优点:

1.  将变量直接代入字符串的能力，即字符串插值。
2.  字符串可以有多行。

3.将它包含在 HTML 中是安全的。

普通字符串也可以跨越 multiline，其语法如下:

```
console.log('string text line 1\n' +
'string text line 2');
```

然而，使用模板文字，它变得更容易理解，看起来也更干净。

```
console.log(`string text line 1
string text line 2`);
```

这两个代码都记录多行字符串，但毫无疑问，模板文本看起来更简单。

当正确使用时，它可以产生更干净、更短和更简单的字符串。

## 3.零融合算子

一个逻辑运算符，无效合并运算符(？？)可以将您从不可预见的错误和日志中拯救出来。

使用这个操作符，您可以快速检查变量是否为空，如果是，就设置默认值。

```
const foo = null ?? 'John Smith';
console.log(foo);
//output: 'John Smith'const bar = undefined?? 75;
console.log(bar);
```

换句话说，当左侧操作数为`undefined`(或`null`)时，该运算符返回右侧操作数。

您可以立即看到该运营商提供的巨大优势。

这不仅会使代码更加无错，还能帮助避免可能导致崩溃的意外行为。

值得注意的是，OR 运算符(||)也可以实现同样的功能。

```
let firstName = null; 
let lastName = null; 
let nickName = "Guest";  // shows the first truthy value: alert(firstName || lastName || nickName || "Anonymous"); //Guest
```

OR(||)和 nullish 合并运算符(？？)也就是说，||运算符返回第一个真值，而？？运算符返回第一个定义的值。

## 4.可选链接

可选的链接运算符(？。)提供了一种安全快速的方法来访问嵌套的对象属性。

使用它，您可以轻松地读取位于连接对象链深处的属性值，而不必明确验证链中的每个引用是否有效。

```
const user= {
  name: 'John',
  security:{
    password:'somepass',
  }
};const mpassword = user.security?.password;
console.log(mpassword); //"somepass"const mpassword = user.address?.street;
console.log(mpassword); //undefined
```

在执行任何操作之前，您也可以使用这个操作符来检查属性是否存在，但是更好的方法将在下面讨论。

## 5.`in` 操作员

`in`操作符用于验证一个指定的属性存在于一个对象或者它的原型链中。

```
const car = { make: 'Honda', model: 'Accord', year: 1998 };console.log('make' in car);
// expected output: truedelete car.make;
if ('make' in car === false) {
  car.make = 'Suzuki';
}console.log(car.make);
// expected output: "Suzuki"
```

正如您所注意到的，`in`操作符根据指定的属性存在返回`true`或`false`。

在进行 DOM 操作时，这个属性非常有用。

```
var q= "onrender" in  document.createElement("div");
if(q){
  ...
}
else{
  ...
} 
```

你可以在这里阅读更多关于这个操作符[的内容。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)

## 6.JSON 对象

我知道 JSON 对象，尤其是`JSON.stringify()`，即使初学者也知道并使用，尤其是在调试时。

但是这比看起来要复杂得多。

首先，`stringify`函数可以有多个参数。

第二个参数可以是一个数组，包含我们打算记录到控制台的值的键，允许我们只打印我们感兴趣的值。

您甚至可以传递一个函数作为第二个参数，它将检查每个键/值对。

```
JSON.stringify(someObject, (key, value) => {
  if (value === 0) {
    return undefined;
  }
  return value;
});
```

你可以在这里找到这个神奇功能[更多这样的鲜为人知的方面。](https://dev.to/blacksonic/the-secret-power-of-json-stringify-393b)

## 7.数组方法

这个听起来并不新鲜，也没有上面讨论的那些令人兴奋，但是最近围绕数组的发展带来了一些令人难以置信的数组方法。

例如，如果您将员工的工资存储在一个数组中，并希望从所有工资中扣除一定的百分比，使用`map`方法可以很容易地做到这一点。

```
var numbers = [400, 800, 300, 1000];
var x = numbers.map(*v*=> v*0.75) //reducing 25% of the salaryconsole.log(x)
console.log(numbers)
```

类似地，您有`every`方法来检查整个数组，看它是否满足特定的标准。

```
var data = [
{name:'Science', results:'passed'},
{name:'Maths',results:'failed'},
{name:'Computer',results:'passed'},
];
var finalResult=data.every(*v* => v.results=='passed')
```

我在最近的一篇文章中讨论了这些函数以及其他函数。

[](/8-modern-array-methods-that-every-developer-should-know-416855e01757) [## 每个开发人员都应该知道的 8 种现代数组方法

### 非常有用的方法让你的生活更轻松

javascript.plainenglish.io](/8-modern-array-methods-that-every-developer-should-know-416855e01757) 

## 最后的想法

JavaScript 和生活中的大多数事情一样，不是你能完全掌握的。

JavaScript 有很多隐藏的特性，我在本文中精选了一些最有用的特性。

您可以精通并胜任 JavaScript，但是无论您做什么，很有可能有些特性或技巧仍然超出了您的范围。

编码是一个终生的旅程，会遇到和学习新事物，因此你必须享受这个旅程。

然而，旅程不一定要单调乏味。

在我最近的博客中，我讨论了一些有趣的游戏，它们可以提高你的编码技能。

[](/7-fun-games-you-should-play-to-up-your-coding-skills-ec051a55faaa) [## 你应该玩的 7 个有趣的游戏来提高你的编码技能

### 掌握各种网络技术的非典型方法。

javascript.plainenglish.io](/7-fun-games-you-should-play-to-up-your-coding-skills-ec051a55faaa) 

我希望你喜欢阅读这篇文章！