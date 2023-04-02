# 理解 JavaScript 中的函数

> 原文：<https://javascript.plainenglish.io/understanding-functions-in-javascript-9846268cd88e?source=collection_archive---------4----------------------->

## 熟悉 JavaScript 函数的分步指南。

![](img/cc958ac1f007cfdc942b2ef3b4fa0380.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在 JavaScript 中，函数的使用频率越来越高。如果您熟悉 JavaScript 开发，那么您就知道在开发项目中这些事情有多重要。

因此，最好在使用之前清楚地了解这些功能。

# 功能

在每种编程语言中，我们可以看到使用这些函数的不同方式。在我们讨论 JavaScript 函数的例子之前，让我们试着理解什么是函数，以及为什么我们需要 JavaScript 中的函数。

函数是我们用来执行特定任务的一组语句，使用函数的重要性在于，我们可以写一次，也可以想用多少次就用多少次。

例如，您可以编写一个简单的函数，获取两个数字作为参数，并返回这两个数字的和。所以，当你需要将两个数字相加得到总的回报时，你可以在程序中的任何地方使用这个函数。请记住，您必须在需要的时候调用该函数。

在 JavaScript 中，我们可以用 3 种不同的方式编写一个函数。

# 1.常规函数—函数声明

在函数声明中，您可以使用 function 关键字，并按如下方式编写它。

```
 function welcome(name) {
console.log(‘Hello ‘, name);}
```

在这个方法中，我们使用**函数**关键字启动我们的函数，然后写下函数的名字。如果您为函数获取任何参数，如上例所示，将它们放在括号内。如果它没有得到任何参数，则将括号留空。

然后打开一个括号，在里面写下你的代码。当您需要调用该函数时，在任何需要的地方键入`welcome(‘John’)`。

# 2.函数表达式

基本上，在函数表达式中，我们所做的是将函数存储在变量中。在 JavaScript 中，我们使用`var`、`let`和`const`来声明变量。所以，当涉及到函数表达式时，我们可以把上面的函数写成下面的形式。

```
 const welcome = function(name) {
console.log(‘Hello ‘,name);}; 
```

当您调用这个函数时，使用变量名**欢迎使用**并在末尾加上括号。`welcome(‘John’)`。

通过查看这两种函数声明方法，您可能会认为它只与语法不同。但是当涉及到 JavaScript 中的提升时，这两种方法之间有相当大的差异。

如果使用函数声明的第一种方式，则可以在调用函数之前或调用函数之后声明函数。

让我们通过下面的例子来理解这一点。

```
ex 01:
welcome('John');/*

 some code here*/function welcome(name){
console.log('Hello ',name);
}
welcome(‘John');
```

在这里，这个函数调用在你把它放在函数声明之前或者声明之后的时候起作用。

但是当涉及到函数表达式时，不能在声明之前调用函数。您总是需要先声明函数，然后才能调用它。

```
ex 02:const welcome = function(name){
console.log('Hello ',name);};welcome(‘John');
```

# 3.箭头功能

这被称为函数声明的缩写形式。让我们通过下面的代码示例来理解这一点。

```
 // function expressionconst welcome = function(name){
console.log(‘Hello ‘,name);};// arrow functionconst welcome = name => {
console.log(‘Hello ‘,name);};
```

在这里，不需要**函数**关键字，您可以直接放置用于该函数的参数。如果你在上面的 ***(ex: name)*** 函数中只使用了一个参数，你就不需要用括号将参数括起来。

但是，如果你在 arrow 函数中使用两个或更多的参数,用括号把它们括起来是很重要的。

```
ex 03:// arrow function which takes two parametersconst msg = (name, time) => {
console.log(`Hey ${time}, ${name}`);};msg('John','good morning'); // note: order of the argument should be matched with the parameters.
```

同样，如果你的函数没有任何参数**,保持括号为空，如下所示。**

```
ex 04:// arrow function with no parametersconst msg_2 = () => 'hey there!';
console.log('Message is: ‘,msg_2());
```

让我们用下面的例子来试着更熟悉箭头函数。

```
ex 05:// suppose we need to find the area of a triangle by giving height and base valuesconst calcArea = (height, base) => {
return (height * base)/2;};const area = calcArea(10, 12);
console.log('Area is: ',area); // since you're returning a value in a single line, you can simplify this arrow function further as belowconst calcArea = (height, base) => (height * base)/2;
```

# 结论

在大多数场合，开发者倾向于使用**函数表达式**和**箭头函数**在 JavaScript 中声明函数。

如果你还不熟悉 JavaScript，使用常规的函数声明，一旦你逐渐习惯了，你会发现函数表达式和箭头函数比常规方法更容易使用。

感谢您的阅读。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*