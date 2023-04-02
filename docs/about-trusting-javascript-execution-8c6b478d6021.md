# 应该信任 JavaScript 执行吗？

> 原文：<https://javascript.plainenglish.io/about-trusting-javascript-execution-8c6b478d6021?source=collection_archive---------2----------------------->

## JavaScript 是最动态的脚本编程语言之一。本文强调了与 JS 相关的安全问题。

![](img/2a7f0ae9a1d5672880cfc0a5cf8f4af8.png)

Photo by [Cytonn Photography](https://unsplash.com/@cytonn_photography?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/trust?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在脚本编程语言中， *JS* 无疑是最有活力的语言之一，或者更好地说，是一种可以定义、截取、覆盖几乎所有东西的语言，包括用于通过秘密/密码加密和解密任何东西的[crypto . precious](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto)命名空间。

这一事实通常被低估了，除非我们从事的项目希望确保用户不会泄露数据，不会被采集指纹，不会在网上冲浪时受到间谍软件的攻击，等等。

虽然肯定的是，“人们必须信任登陆在网站上的脚本”，或者你的后端项目，但现实是，广告行业，几乎没有人直接控制，从 *JS 框架*开发者开始，会尽一切可能使我们的网上冲浪有利可图，它需要跟踪，cookies，或类似的变通办法，指纹，并不时地使用极其邪恶的代码(顺便说一句，我在这个领域工作，与邪恶的代码作斗争，我们每天也试图保护用户免受这些类型的利用)。

通过 *npm* 或类似方式添加常规黑客尝试，我们就在这里了！

## 有多糟糕？

每个人都认为污染本地/内置原型应该被禁止，但这并不意味着不能这样做。此外，我们可以拥有这个世界上所有的林挺规则，但那只是关于我们的项目，而不是关于我们的软件将由 T21 执行的地方，我们能看出区别吗？

```
const {[Symbol.iterator]: iterator} = Array.prototype;Object.defineProperty(
  Array.prototype,
  Symbol.iterator,
  {
    value() {
      console.log('MitM', this);
      return iterator.call(this);
      //             ^^^^^ keep reading
    }
  }
);
```

这一小段代码将允许任何人设置它:

*   读取任何被调用的函数、方法或`new Class(...args)`可能做的每个`...spread`操作
*   阅读每一篇`Array.from`操作
*   在每一个`for/of`循环开始之前，或者在它发生的时候阅读它
*   读取通过条目数组创建的每个`Set`或`Map`
*   拦截每一次`const [value, update] = useState(init)`的使用，因为析构数组显然也会受到影响
*   …等等…在使用 web 应用程序时，允许访问几乎所有类型的共享数据

现在，让我们添加一个`typeof`检查来过滤字符串，定义一些常见的(历史上丑陋的、无意义的、破碎的、愚蠢的……)`/^[a-z0-9#$_+!?.-]{8,}$/i`reg exp，连同一个经典的`/^[^@]+@\S+$/`，等瞧:**如果认证数据被传播，没有登录是安全的。**🤯

这些类型的邪恶覆盖也可以写在代码后面，使其几乎不可能被检测到，通过污染`Function.prototype.toString`和任何其他我们用来检测`[native code]`是否存在的方法，所以基本上，先有邪恶，后有邪恶。

# ⚠️不仅阵

这个`Array.prototype`把戏已经很有趣了，但是人们也可以同样容易地毒害每一个原型(请不要这样做🙏):

```
for (const key of Reflect.ownKeys(self)) {
  // ignore non-classes maybe, typeof next!
  if (!/^[A-Z]/.test(key))
    continue; const Builtin = self[key];
  if (
    typeof Builtin === 'function' &&
    // ignore Proxy or others
    'prototype' in Builtin &&
    // filter by iterator presence
    Builtin.prototype.hasOwnProperty(Symbol.iterator)
  ) {
    // trap it
    const {[Symbol.iterator]: iterator} = Builtin.prototype;
    // override
    Object.defineProperty(
      Builtin.prototype,
      Symbol.iterator,
      {
        value() {
          // win 🥳
          console.log('MitM', this);
          return iterator.call(this);
          //             ^^^^^ keep reading
        }
      }
    );
  }
}// tadaaaaaa 🎉
[...new Set([1, 2, 3])]
// two MitM logs for you
```

所以，是的，几乎每一个已知的事物都有可能被毒害，除了少数好人。🤠

```
function noProblem() {
  console.log(...arguments);
}// 1, 2, 3
noProblem(1, 2, 3);const alsoNoProblem = (...args) => {
  console.log.apply(console, args);
  //         ^^^^^^ keep reading
};// 4, 5, 6
alsoNoProblem(4, 5, 6);
```

*   对象不是一个数组，[它有自己的迭代器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments#browser_compatibility)已经有一段时间了，所以散布它是非常安全的🦄
*   `...rest`参数只是引擎的语法提示，但在接收时不会被迭代，它们只是一个数组。然而，如果我们将它们展开，它们会通过`Array.prototype`，因此如果我们将它们展开，不会发生任何变化；它仍然是不安全的，因此我们需要*申请*(然而，继续阅读)

# ⚠️不仅是可写的

如果我们还在跟踪到底发生了什么，那么显而易见的是，毒害任何根原型都会提供极其强大的攻击，我相信 99%的网站都不会想到这一点。让我们看另一个例子:

```
class User {
  constructor(name) {
    this.name = name;
  }
  auth(password) {
    return fetch(
      '/authenticate',
      {
        headers: {
          Authorization: `Basic ${
            btoa(`${this.name}:${password}`
          )}`
        }
      }
    );
  }
}
```

让我们快速列出这几行代码中所有可能出错的地方，好吗？

*   `Object.defineProperties(Object.prototype, {name, {get(){}, set(){}}, password: {get(){}, set(){}}, email: {get(){}, set(){}}})`可以在任何时候用来拦截所有愚蠢的类(包括 mines ),这些类只是在构造函数中附加属性，根本不需要到达`User`原型
*   `fetch`全局函数可以被毒化以拦截任何类型的头，包括那些带有 *OAuth* 凭证的头，或者更糟
*   `btoa`全局函数也会中毒，并拦截凭证

简而言之，我很抱歉以这种方式把事情搞成这样，但基本上，我们注定要失败。💣

# ⚠️不仅仅是 JavaScript

如果我们明白每一种针对 JS 的编程语言都会给我们无法控制的代码增加一个额外的间接层，从而使问题变得更大并且不容易解决，那么这一段就不需要了，但是因为我知道通常情况不是这样，所以让我们展示一些实际的例子。👍

## 以打字打的文件

生产中会有各种各样的变化，一旦发生变化，就会有**零额外信任** *TS* 带到桌面上，实际上完全相反:

```
//TS
class User {
  public name = '';
  private pass = '';
}// becomes this JS: busted
class User {
    constructor() {
        this.name = '';
        this.pass = '';
    }
}
```

公共和私有字段都成为`constructor`潜在的设置者，因此任何拦截这些属性的恶意代码都可以在运行时毒害实例，以便随时检索名称和密码。

“*很公平*”，我听到有人在喊，“*那我就用真的私处吧！*“，确定！

```
// TS
class User {
  name = '';
  #pass = '';
  constructor(name: string) {
    this.name = name;
  }
}// becomes this JS: busted
var _User_pass;
class User {
    constructor(name) {
        this.name = '';
        _User_pass.set(this, '');
        this.name = name;
    }
}
_User_pass = new WeakMap();
```

这是今天 TS 在其最新的游戏中提供给我的默认设置，目标是 ES2017，这是一个非常明智的目标。(阅读:请不要把重点放在“*但 ESNext 目标是纯粹的*”废话，谢谢！)

这意味着任何在任何时间点污染了`WeakMap.prototype.set`方法的邪恶代码，将能够准确地拦截所有那些我们不想暴露的私有变量或实例…这有多"*伟大*"啊？😢

我可以继续说一段时间:

```
// TS
function merge(a:object, b:object) {
  return {...a, ...b};
}// becomes this JS: busted
function merge(a, b) {
    return Object.assign(Object.assign({}, a), b);
}
```

在这里，如果任何邪恶的代码会毒害`Object.assign`，那么所有的 *TS* 实例都将被轻易地暴露出来，因此其他所有成为`Global.utility(...args)`调用的事情也是如此。

## 镖

老实说，我不知道 Dart 的生态系统，也不知道疯狂的 JS 脚本是否会不被注意地进入 100%的 Dart 项目，但毫无疑问，它的运行时充满了潜在的攻击。

例如，如果我们美化我能找到的最基本的示例输出:

```
void main() {
  for (int i = 0; i < 5; i++) {
    print('hello ${i + 1}');
  }
}
```

我们会注意到，整个 JS Dart 的运行时重复访问每个全局`Object`实用程序，包括`defineProperty`和其他。

不过有趣的是，Dart 的运行时似乎没有遇到我们之前讨论的`Symbol.iterator`问题，主要是因为它的代码似乎也针对旧浏览器，但它也做诸如`Array.prototype.push.apply(target, arguments)`的操作，退回到“*一切容易暴露的*类别，就像 *TypeScript* 。

"*等等……为什么呼叫或申请不安全？“谢谢你的关心。😎*

```
const {call} = Function.prototype;
Object.defineProperty(
  Function.prototype,
  'call',
  {
    value(context, ...args) {
      console.log(context, args);
      return call.apply(this, [context, ...args]);
    }
  }
);
```

我想强调的是，通过 JS 原语传递的所有东西都可能以这样或那样的方式中毒:这清楚吗？

## Node.js & Deno

是的伙计们，**是的**！我所说的一切都源于 ECMAScript 规范，并不局限于浏览器，它只是关于 JavaScript 是如何定义的，以及它如何工作了 20 多年！

## …甚至巴贝尔？

哦，看在上帝的份上，是的！

## 好吧…那么，外面有什么安全的地方吗？

可能有，但是因为没有人足够重视这个被最广泛部署的编程语言低估的安全问题，简短的答案是**不**，但是我们可以做得更好，更安全地保护我们的环境，只要多信任我们的代码一点点，它只需要 4 行代码，至少作为起点。🌈

# 功能陷阱缓解

我已经在 10 多年前提到过这种技术[，要点是](https://webreflection.blogspot.com/2011/10/bind-apply-and-call-trap.html)[我们可以捕获最原始的实用程序来调用任何东西，这样在运行时就不会有任何干扰:](https://github.com/WebReflection/proxy-pants/blob/main/esm/function.js#L3-L6)

```
const {apply: a, bind: b, call: c} = Function;
const apply = c.bind(a);
const bind = c.bind(b);
const call = c.bind(c);
```

例如，我们现在可以捕获我们喜欢的每个类的`Symbol.iterator`生成器，以便我们可以直接调用它来迭代:

```
const {[Symbol.iterator]: iterator} = Array.prototype;
const iterate = arr => call(iterator, arr);// example
for (const safe of iterate([1, 2, 3]));
```

我们现在可以`iterate([literally, any, array, value])`并且 100%确定没有任何东西可以拦截传递的参数，只要我们的陷阱在任何可能的恶意代码之前**就存在。幸运的是，基于广告的脚本笨重，因此，很少作为第一个阻止脚本加载，特别是由于搜索引擎的排名，这是一个惩罚这种笨重，缓慢和阻止脚本的指标。**

然而，实际上不能保证我们的代码在任何其他代码之前运行，特别是在这个世界上，每个人都迫不及待地使用最新的工具/捆绑器，而且一旦整个事情产生了一个输出，几乎没有人知道什么会进入生产中…我们做得很好！🤝

## 保护任何东西

如果我们理解了`iterate(array)`是如何工作的，我们也可以探索`bind`的用法，通过它的所有者来保护任何方法:

```
// defining literals is always safe 🍻
// and so is the access to own properties
const obj = {
  name: 'safe',
  method() {
    console.log(this.name);
  }
};const method = bind(obj.method, obj);
method(); // "safe"
```

同样的事情也可以一劳永逸地发生在公共事业上:

```
const assign = bind(Object.assign, Object);
const entries = bind(Object.entries, Object);
```

虽然，我们可以想象为我们需要的每一个该死的全局实用程序这样做可能会非常耗时，这就是为什么我创建了 [**proxy-pants**](https://github.com/WebReflection/proxy-pants#readme) ，这是一个友好的树摇动模块，充满了罕见的常见用例，以一种安全的方式一次性绑定方法或访问器。

```
import {bound} from 'proxy-pants';const {
  assign,
  entries,
  defineProperty,
  getPrototypeOf
} = bound(Object);
```

清楚了吗？我们传递任何实例或全局实用程序，从现在开始，我们需要做的就是直接使用`assign({}, a, b)`或`entries(ref)`，而不必担心恶意代码。😇

等等，你是在问*访问者*吗？好吧，这里有一个例子:

```
import {accessor} from 'proxy-pants';

const {textContent} = accessor(document.body);

// get the current body text
textContent();

// set the new one
textContent('proxy pants!');
```

*调用方*还是*应用方*？没问题！

```
import {applier, caller} from 'proxy-pants';

const {hasOwnProperty, toString} = caller(Object.prototype);

hasOwnProperty({any: 'object'}, 'any'); // true
toString(null); // [object Null]

const {fromCharCode} = applier(String);
const charCodes = (...args) => fromCharCode(String, args);charCodes(60, 61, 62); // <=>
```

*TL；DR* 我已经写了各种库和助手，围绕这个“*安全和可信执行*”和 [proxy-pants](https://github.com/WebReflection/proxy-pants#readme) 包括这些技术，因为我们已经测试过这些技术在野外工作，我们的用户可以睡得更好，肯定更安全，所以如果你想至少保护你的代码的最关键部分，请随意使用这个库😉

# 🎯行动建议

我真的希望没有人应该编写像`[...call(iterator, arr)]`这样的*颠倒的代码*，或者甚至`[...iterate(arr)]`，而不是自然的`[...arr]`操作，好的一面是**没有人需要重构任何东西**或者改变他们的代码基础，或者删除*类型脚本*，或者 *Dart* ，以便能够控制他们的应用程序的安全级别，除了之外的**可能是核心库作者，或者关于安全、密码、安全的库已经了解并关注我的人，不应该对我从头开始编写几乎所有类型的模块这一事实感到惊讶，在这篇文章中，你可以找到我这样做的几个原因:Web 开发人员很少把安全问题看得非常严重，但是尽管许多人经常欺负仍然编写普通 JS 的人，而不是使用我们现在拥有的任何间接方式， 我想提醒你的是，那些为你的超级酷的安全的 JS 代码创建 transpilers 的人，通常也不会对这些细节给予足够的关注，所以你在那里运行的任何代码，都可能容易受到我在这篇文章中描述的所有攻击。**

## 最后但同样重要的是:性能！

当涉及到增加安全性时，关键路径上稍微慢一点的代码不应该是决定性因素，但是也就是说，很难衡量`[...call(iterator, arr)]`和`[...arr]`之间的差异，后者需要解析其原型和迭代器，而前者是作用域中众所周知的引用，不需要原型解析。🤘

## …但也…

你可以完全否认我在这里写的一切，特别是因为我敢于触及 *TypeScript* 或 *Dart* 最令人痛苦的一点，即缺乏对翻译目标的控制，但这篇文章的整个目标是让**你**意识到这些类型的攻击是存在的，尤其是对翻译的代码，所以你更好地理解如何减轻这些，你可能已经用 ts 或 dart🥂做到了这一点

## 作为总结

只需编写您喜欢的代码，做您喜欢的事情，但是如果安全性是一个问题，请注意有一些模式可以防止运行时库破坏您的产品，并且记住我已经写了很多解决方案，我非常乐意帮助您保护更多您关心的*特定部分，如果有意义的话，希望其余部分不会泄漏或不安全。👋*

感谢您的阅读。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里报名参加我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*