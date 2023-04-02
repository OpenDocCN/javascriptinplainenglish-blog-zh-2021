# 我希望我知道的事情… JavaScript 函数

> 原文：<https://javascript.plainenglish.io/things-i-wish-i-knew-about-javascript-functions-40fbc8f37bf6?source=collection_archive---------11----------------------->

![](img/fda19fa9e9bafd60120e376dc1de9758.png)

尤其是从 C/Python/酏剂的背景来看，有一些关于 JavaScript 函数的事情我真的没有开始。我想我会把它们写下来，希望它们能在旅途中帮助别人。

我应该注意，这可能是第一部分——随着我继续使用 JavaScript，我肯定会学到更多关于 JavaScript 函数的东西。

# 当一个是异步时，所有的都是异步的

当我开始使用 JavaScript 时，我并不真正理解它是如何异步的，所以我花了相当多的时间试图弄清楚一个函数是如何从异步调用中得到一个结果并返回它，而函数调用方本身不必是异步的。

如果你的目标是一样的，我就不麻烦你了——你做不到。我最初对下面的建筑抱有很高的期望。

```
async function iAmAsync(num) {
  return num * 2;
}

function iUseThen(num) {
  return iAmAsync(num).then(res => res + 1);
}

console.log("iUseThen(3) =>", iUseThen(3));
```

我没有意识到的是`iAmAsync(3).then(...)`会隐含地返回一个[承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，也就是说整个`iUseThen`都会返回一个承诺。

```
iUseThen(3) => Promise { <pending> }
```

我确实发现在简短脚本中使用异步函数的一种方法是声明一个匿名异步函数并立即调用它:

```
(async function() {
	const result = await somethingNetwork();
	console.log("Result", result);
}) ()
```

## `function`和`=>`有什么区别？

`=>`在 JavaScript 中被称为“肥胖的箭头”。胖箭头是创建函数的一种简写方式(有如下限制):

```
function (name) {
  console.log("Hello", name);
}
```

您可以使用:

```
name => console.log("Hello", name);
```

## `=>`的局限性

虽然这很方便，但胖箭头的形式有一些局限性。

## 否**本**

用`=>`定义的函数没有`this`可参照。一个(有点做作的)例子- [这个作品](https://codepen.io/arafel/pen/VwpeXQx):

```
withFunction = {
  answer: 42,
  ask: function () {
    console.log("The answer is:", this.answer);
  }
};
withFunction.ask();
```

生产:

```
The answer is: 42
```

[本不](https://codepen.io/arafel/pen/gOmPzgO):

```
withArrow = {
  answer: 42,
  ask: () => {
    console.log("The answer is:", this.answer)
  }
}
withArrow.ask();The answer is: undefined
```

一个更真实的例子可以在 Vuex 中看到——如果你定义了一个突变或者一个动作，并且你使用了一个胖箭头函数，它可能不会像你预期的那样工作。

这意味着——因为没有`this`，你也不能使用`super`。

## 不能用作构造函数。

如果要定义一个类，必须使用完整的`function foo(bar) {}`形式。

## 不能用**屈服**

我必须承认，这对我来说不是问题，我还没有理由使用发电机。

## 何时使用`(foo) =>`、何时使用`foo =>`？

`foo => ...`表单只接受一个*和一个*参数，即使是简单表单也是如此。

```
foo => console.log("I'm a valid construction if foo is simple");
```

如果需要指明没有参数，括号是必需的。

```
() => console.log("I'm not listening to you");
```

如果你需要传递两个，`(foo, bar) => ...`那么它需要括号。

```
(foo, bar) => console.log("You gave me", foo, "and", bar);
```

## 重要说明

如果你需要用这个参数做任何事情，你需要括号。例如—需要添加一个 TypeScript 类型？括号。想要提供默认参数吗？括号。诸如此类。

```
(foo: string) => console.log("Printing the string", foo);
(foo = 'hello world') => console.log(foo);
```

这可以归结为——仅仅因为你*可以*做某事，并不意味着你*应该*做某事。参考见[凯尔·辛普森精彩流程图](https://raw.githubusercontent.com/getify/You-Dont-Know-JS/1st-ed/es6%20%26%20beyond/fig1.png)。

## 什么时候用`foo => { bar; return baz }`，什么时候用`foo => bar`？

如果函数体是一条语句，可以省略大括号。否则，大括号是必需的。

如果省略了大括号，那么`return`就是隐含的，也必须省略。

一句话，带暗示`return`:

```
foo => foo + 1
```

多条语句，带有明确的`return`:

```
foo => {
	console.log("You gave me", foo);
	return foo + 1;
}
```

## 关闭

有点像混合体——一部分是数据，一部分是功能。我以前遇到过闭包，但是 JavaScript 使它们比我花了很多时间使用的其他语言更容易使用。

一个闭包本质上是一个函数以及它被创建时的环境。

```
function makeClosure(outerArgument) {
  // Return a function which adds 'outerArgument' to
  // whatever argument it's given.
  return function(innerArgument) {
    return outerArgument + innerArgument;
  }
}

addOne = makeClosure(1)
console.log("Created addOne", addOne);
console.log("Two plus one is", addOne(2));
```

哪些输出:

```
$ node closure.js
Created addOne [Function (anonymous)]
Two plus one is 3
```

注意，返回的函数是匿名的，仅仅是因为我们没有在`makeClosure`中命名它。给它命名是很有可能的，虽然我还没发现它有多大用处(到目前为止)。

这是一个关于闭包的小例子——更有用的例子见[我的另一篇关于使用 Axios 的博文](https://www.solarwinter.net/using-closures-with-axios/)。

# 结论

我希望这对某些人来说是有用的介绍——希望我在开始学习 JavaScript 时就知道这些！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)