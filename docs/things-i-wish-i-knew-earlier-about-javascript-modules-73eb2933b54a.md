# 关于 JavaScript 模块，我希望早点知道的事情

> 原文：<https://javascript.plainenglish.io/things-i-wish-i-knew-earlier-about-javascript-modules-73eb2933b54a?source=collection_archive---------15----------------------->

![](img/80afaf66e117e5ec69a6a6b7bf12fa40.png)

我不得不承认，我花了一段时间来理解 JavaScript 模块。这至少部分是因为有两种不同的流行模块系统， [CommonJS](http://www.commonjs.org/) 和 [ECMAScript 2015](https://en.wikipedia.org/wiki/ECMAScript) (通常简称为 ES2015)。

ECMAScript 2015 标准比 CommonJS 新。就我个人而言，我觉得它更简单，我会尽可能优先使用它。然而, [NPM](https://www.npmjs.com/) 上相当多的模块仍然使用旧的风格。

一个重要注意事项—浏览器仅支持 ES2015，不支持 CommonJS。

# CommonJS

CommonJS 由 Mozilla 团队的一名成员于 2009 年发起，试图统一 JavaScript 功能。 [CommonJS](http://www.commonjs.org/) 涵盖的不仅仅是模块——查看网站。

## 出口

在 CommonJS 模块中，符号是在一个对象中导出的(可以理解命名为`exports`)。对象的每个特性都是一个导出的符号。

通常的对象分配规则适用。这意味着您可以很容易地导出一个与文件内部名称不同的符号。

```
function sayHello(name) {
  console.log("Hello", name);
}module.exports = {
  sayHello,
  anotherSayHello: sayHello
};
```

## 需要

然后，您可以`require`整个模块或该模块中的一些符号。

```
const testModule = require("./module_name");
const { sayHello } = require("./module_name");testModule.sayHello("world");
sayHello("second world");
```

**注意**:从 CJS 风格的模块中导入命名符号只在 Node 14 中引入，并不完美——它依赖于 Node 中的一些试探法。

# ES2015

## 出口

ES2015 中导出更容易；一个项目(函数、常量、变量等)可以简单地通过添加`export`关键字导出。

```
export function sayHello(name) { console.log("Hello", name); } export const myName = "Rumpelstiltskin";
```

或者，您可以在文件末尾一次性导出项目。

```
export { sayHello, myName };
```

## 导入

像许多其他语言一样——Java、Python——然后导入想要使用的模块部分。

```
import { sayHello } from "./moduleName";
sayHello("world");
```

或者，如果您想让它们保持命名空间:

```
import * as moduleStuff from "./moduleName";moduleStuff.sayHello(moduleStuff.myName);
```

# 默认导出

在上面的大多数例子中，我们从模块中导入了一个特别命名的符号:

```
import { sayHello } from "./module_name";
```

一个模块也可以有一个默认的导出，如果你没有指定你想从模块中导入什么，你就会得到这个默认的导出。

## CommonJS

CJS 模块实际上只导出一个单项——从这个意义上说，它们只有一个默认的导出。这就是为什么我们想要导出的项目需要是对象的属性。

## ES2015

有了这个系统，你就有了更多的灵活性。可以导出多个内容，并且您可以标记您想要的默认内容。

```
export default const theAnswer = 42;
```

## 用户小心

这并不总是一件好事；您永远无法完全确定您要导入的是什么，它可能会以与原始文件完全不同(并且容易让人误解)的名称导入。

例如，以普通模块`basicMaths`为例:

```
export default sum(x, y) {
  return x + y;
}
```

该默认导出可以作为任何内容导入。

```
// This will not do what you expect.
import divide from "./basicMaths";divide(2, 4);
```

命名出口的好处是你进口的正是你想要的，没有惊喜。

```
import { divide } from "./basicMaths";// divide is empty, so this crashes (or doesn't build, depending on
// how good your tools are). Either way it's better than using the
// wrong function. 
divide(2, 4);
```

*原载于 2021 年 11 月 10 日【https://www.solarwinter.net】[](https://www.solarwinter.net/things-i-wish-i-knew-about-javascript-part-2/)**。***

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*