# 如何在 JavaScript 中使用模板文字构建模板引擎

> 原文：<https://javascript.plainenglish.io/how-to-build-a-template-engine-using-template-literals-in-javascript-9ace13ae4514?source=collection_archive---------3----------------------->

![](img/434b5b80f19e9dcb615ac2dcfe21a30f.png)

Photo by [Joanna Kosinska](https://unsplash.com/@joannakosinska?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可能见过像[小胡子](https://mustache.github.io/)、[ejs.co](https://ejs.co/)这样的模板引擎。这些库用起来非常酷。然而，对于简单的用例，您可能不想包含这些库。可以增加制作 app 的代码量。JavaScript ES6 或 ES2015 引入了模板字符串或模板文字的概念。使用模板字符串，您可以构建一个模板引擎。

## 什么是模板字符串？

模板字符串是指允许创建多行字符串的分隔符。它还可以包括表达式。模板字符串可以使用反斜杠(``)来定义。

**样本:**

```
const userName = "Deepak";
let htmlStr = `<div>
  <h1>This is Template String</h1>
  <p>My name is ${userName};
</div>`;console.log(htmlStr);
/* 
<div>
  deepak is list is
  <h1>30</h1>
  yrs old
</div>
*/
```

在上面的示例中，`**htmlStr**`是一个存储使用模板字符串计算的字符串的变量。用户名将被变量`userName.`的值替换

使用占位符`**${}**`，你可以分配任何表达式。模板字符串将尝试计算表达式，并将其分配给占位符位置。

**样本:**

```
const a = 10;
const b = 5;
console.log(`The value of exp (a+b)*10= ${(a + b) * 10} `);//The value of exp (a+b)*10= 150
```

## 标记模板

模板字符串还提供了标记模板的强大功能。您可以将任何函数用作标记函数。标记函数可以解析模板字符串。第一个参数是经过解析的字符串数组，其余参数是模板字符串中使用的表达式。让我们创建一个标记函数。

```
const html = (strings, ...args) => {
  console.log(strings);
  console.log(args);
};// [ '{name:', ', age: ', ',\ngetName:', '}' ]
// [ 'Deepak', 30, [Function: getName] ]const user = {
  name: "Deepak",
  age: 30,
  getName() {
    return this.name;
  },
};const htmlString = html`{name:${user.name}, age: ${user.age}, getName:${user.getName}}`;
```

如果你运行上面的例子，你会看到一个包含`[ ‘{name:’, ‘, age: ‘, ‘,getName:’, ‘}’ ]` 的字符串数组和一个所有传递的表达式`[ ‘Deepak’, 30, [Function: getName] ].`的数组。正如你注意到的，你也可以传递一个函数作为表达式。

**CSS 构建器**

如果你曾经做过 React，你可能会熟悉 [**样式化组件**](https://styled-components.com/) 。S **tyled-components** 提供了许多实用方法来创建 React 组件。**样式化组件**最大的 USP 是标记模板函数的使用。`**css**`是效用函数之一。使用这个函数，你可以创建复杂的 CSS 字符串。让我们试着模仿这种行为。

```
// Theme token varibaleconst theme = {
  color: "#dedede",
  font_size: "20px",
};/**
 * css: tagged function, parse the string template 
 * and exec all functions theme as parameter.
 *
 * [@param](http://twitter.com/param) {*} strings
 * [@param](http://twitter.com/param)  {...any} fns
 * [@returns](http://twitter.com/returns)
 */
const css = (strings, ...fns) => {
  let str = strings[0];
  for (let i = 0; i < fns.length; i++) {
    if (typeof fns[i] === "function") {
      str += fns[i](theme);
    } else {
      str += fns[i];
    }
    str += strings[i + 1];
  }
  return str;
};const cssStr = css`
   {
    color: ${(p) => p.color};
    font-size: ${(p) => p.font_size};
  }
`;console.log(cssStr);// { color:#dedede; font-size:20px }
```

**解释**:

在上面的例子中，我们已经创建了一个**主题**变量。这个主题变量存储所有的主题标记。 **css** 函数将解析模板字符串，并将字符串与表达式的值连接起来。它执行所有以主题变量作为参数的函数表达式。

现在，既然我们对模板字符串和标记函数有了一个很好的想法，让我们试着构建一个复杂的 HTML 引擎。

**要求**:

HTML 函数的简单要求是获取一个模板字符串并对对象建模，解析它并返回 HTML 字符串。

```
function html(string template, object model) 
 -> (string html)html(
  `<div>${"person.name"} is <strong>${(m) => m.person.age}</strong>yrs old</div>`, { person: { name: "deepak", age: 30 } }
);{/* <div>deepak is <strong>30</strong>yrs old</div> */}
```

为了构建这个 HTML 解析器，我们需要一个简单的 util 函数`safeEval`。这个 **safeEval** 函数将帮助从基于键的对象中获取嵌套值。

```
const evalReg = /(\.)|(\[(\d)\])/;
const safeEval = (key, obj, def) => {
  let lastKey;
  let match;
  do {
    if (lastKey) {
      if (match && match[2]) {
        obj = obj[lastKey][match[3]];
      } else {
        obj = obj[lastKey];
      }
    }
    match = evalReg.exec(key);
    if (!match) {
      lastKey = key;
      break;
    } else {
      lastKey = key.substr(0, match.index);
      key = key.slice(!match[3] ? match.index + 1 : match.index + 3);
    }
  } while (match);
  if (lastKey) {
    obj = obj[lastKey];
  }
  return obj || def;
};const model = { person: { name: "deepak", age: 30 } }
console.log(safeEval("person.name", model));
console.log(safeEval("person.age", model));// deepak
// 30
```

一旦我们有了`safeEval`函数，剩下的逻辑就非常简单，与`css`标记函数相同。

```
/**
 * html: tagged function returns a closure function. The closure function parse the template string and bind with model data
 * 
 * [@param](http://twitter.com/param) {*} strings 
 * [@param](http://twitter.com/param)  {...any} fns 
 * [@returns](http://twitter.com/returns) 
 */
function html(strings, ...fns) {
  return (model) => {
    let str = strings[0];
    for (let i = 0; i < fns.length; i++) {
      const evl = fns[i];
      if (typeof evl === "string") str += safeEval(evl, model);
      else if (typeof evl === "function") str += evl(model);
      else res += evl;
      str += strings[i + 1];
    }
    return str;
  };
}let template = html`<div>${"person.name"} is <strong>${(m) => m.person.age}</strong>yrs old</div>`;console.log(template({ person: { name: "deepak", age: 30 } }));// <div>deepak is <strong>30</strong>yrs old</div>
```

Tada！我们最简单的 HTML 模板引擎已经可以使用了。您可以根据自己的需要定制和增强行为。

**一个复杂的例子:**使用 HTML 模板引擎构建一个秒表。

**参考:**[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Template _ literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

*更多内容看**[***说白了. io***](http://plainenglish.io/)*