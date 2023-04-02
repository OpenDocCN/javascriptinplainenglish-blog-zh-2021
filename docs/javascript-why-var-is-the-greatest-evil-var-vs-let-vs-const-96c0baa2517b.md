# JavaScript:为什么“var”是最大的恶魔

> 原文：<https://javascript.plainenglish.io/javascript-why-var-is-the-greatest-evil-var-vs-let-vs-const-96c0baa2517b?source=collection_archive---------9----------------------->

## JavaScript 中“var”、“let”和“const”的区别——详细解释。

在我的 [YouTube 频道](https://www.youtube.com/watch?v=FNh2JCiFXIg)看这个教程！

为什么不用' var '？当你看到这篇文章的标题时，你可能会问这个问题。没错！关键字`var`可能是这种语言最令人头疼的特性之一。多年来，随着 ES6 中`let`和`const`关键词的引入，人们从此爱上了`let`和`const`关键词。让我们来看看为什么。

![](img/1029f85ae952cbff0a2764f7788982c2.png)

Photo by [Sammy Williams](https://unsplash.com/@sammywilliams?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 理解范围

在我们继续之前，让我们简单地看一下什么是作用域。

一般来说，作用域可以定义为包含在一对花括号`{}`内的代码块(object 除外，它也是由一对`{}`创建的)。每当我们看到一对花括号，我们就可以假设我们进入了一个新的范围。

例如:

```
*// an if statement*
if(condition){
    *//....*
}*// for loop*
for (let index = 0; index < array.length; index++) {}*// function*
function something(){}*// or just a random pair of curly braces for the sake of creating a new scope*
{
    *// some code*}
```

您可以将作用域想象成一个半隔离的房间:作用域内创建的任何东西都留在作用域内。但是，我们需要遵守一些规则:

1.  在作用域中创建的变量留在作用域内。一旦我们退出作用域，在作用域内创建的变量将会被丢弃到永恒的虚空中😛。
2.  我们可以访问父作用域中的变量，但是父作用域不能访问子作用域中的变量。
3.  `var`变量有💩不要遵守这些规则。

注意:功能作用域与标准作用域稍有不同。稍后将详细介绍。

# `var`怎么会出问题？

现代 JavaScript 有 3 种方式定义变量，即使用`var`、`let`和`const`关键字。

假设我们有以下代码:

```
let a = 'a';
var b = 'b';
const c = 'c';if(true){
    let a = 2;
    var b = 2;
    const c = 2;
}*// What are we going to see here??*
console.log(a);
console.log(b);
console.log(c);
```

您希望在控制台日志中看到什么？答案可能会让你吃惊:

```
*// ....*console.log(a); *// expect: a*
console.log(b); *// expect: 2*
console.log(c); *// expect: c*
```

## 这是怎么回事？

我们来分析一下。这又回到了规则 1:

> *在作用域中创建的变量留在作用域内。*

```
let a = 'a';
var b = 'b';
const c = 'c';*// we are creating a scope here in the if statement*
if(true){
    *// variables created using the 'let' and 'const' keywords* 
    *// stays inside the scope, and will be destroyed once we exit the scope* *// here we are redeclaring variable 'a' and 'c'. So 'a' and 'c' are not*
    *// related to their counterparts above at all!* *// However this rule does not apply to 'var' variables.* 
    *// So redeclaring variable 'b' will override the value of the variable 'b'* 
    *// above.*
    let a = 2;
    var b = 2;
    const c = 2;
}
*// Hence, variable 'a' and 'c' here are referring to the variables* 
*// declared before the if statement.* *// Variable 'b' got rewritten in the if statement*
console.log(a);
console.log(b);
console.log(c);
```

👊这演示了`var`变量最危险的行为之一:`**var**` **不是范围安全的。**

再来说说`var`的另一个危险行为:吊装。

# 提升

提升机在英语中是“升起”的意思。在 JavaScript 中，提升意味着将变量移动到代码的最开头。默认情况下，所有`var`变量都被提升。

例如，下面的代码:

```
if(true){
    var hey = "ya";
}
```

对 JavaScript 来说会是这样的:

```
var hey;if(true){
    hey = "ya"
}
```

这就是吊装的意思。实际上，将变量移到脚本的顶部。

# JavaScript 如何读取变量？

在我们继续之前，让我们了解 JavaScript 如何处理变量。

在 JavaScript 中创建变量实际上有两个步骤。**申报**和**分配**。

**声明**就是只声明一个变量，没有值。赋值意味着给变量赋值。

```
*// declaring the variable 'abc'*
let abc;
*// assigning value to variable 'abc'*
abc = 123;
*// Normally we carry out declaration and assignment in 1 go.*
let hey = 'ya';
```

现在，这里是 JavaScript 如何读取变量的值。

1.  当 JavaScript 看到一个变量时，它将首先尝试在当前范围内查找该变量。
2.  如果在当前范围内没有找到该变量，那么 JavaScript 将在父范围内查找。
3.  如果在父作用域中没有找到该变量，那么 JavaScript 将在祖父作用域中查找，等等…

一些例子:

**情景一:**

```
let abc = 123;if(true){
    *// Here, Js will try to find the declaration of 'abc' in* 
    *// the current scope.* *// There is none, so JS will proceed to the parent scope.* 
    *// In the parent scope, the variable 'abc' is declared and has a value of 123.*
    console.log(abc); *// expect: 123*
}
```

**情景二:**

```
let abc = 123;if(true){
    let abc = 456; *// Again, JS will try to find the declaration of 'abc' in the current scope.*
    *// There is a declaration, and its value is 456*
    console.log(abc); *// expect: 456*
}
*// We are now reading 'abc' on the parent scope.* 
*// So we are getting the value 123*
console.log(abc); *// expect: 123*
```

**情景三:**

```
let abc = 123;if(true){
    *// There is a declaration in the current scope, but it is declared*
    *// after JS's attempt to read it. We can't read a value before we* 
    *// declare it.* *// Therefore we see an error*
    console.log(abc);  *// expect error*
    let abc = 456;
}
```

# 那么吊装和这个有什么关系呢？把所有的放在一起

因为默认情况下`var`变量被提升，所以让我们再看一遍上面的场景，但是使用`var`。

**情景一:**

```
*// This works like before, JS will try to read the variable from the parent scope*
var abc = 123;
if(true){
    console.log(abc); *// expect: 123*
}
```

**情景二:**

```
var abc = 123;if(true){
    var abc = 456;
    console.log(abc); *// expect: 456*
}
*// We are getting 456 this time!!*
console.log(abc); *// expect: 456*
```

😦好了，冷静下来。这正是吊装提出的问题。对于 JavaScript，上面的代码看起来像:

```
var abc;
abc = 123;if(true){
    *// we are overwriting the global variable abc.*
    abc = 456;
    console.log(abc); *// expect: 456*
}
*// value of 'abc' has been changed by the if statement scope*
console.log(abc); *// expect: 456*
```

**场景 3:**

```
var abc = 123;if(true){
    console.log(abc);  *// expect: 123*
    var abc = 456;
}
```

😦😦好吧，让我们再冷静一次。这是 JavaScript 看到的:

```
var abc;
abc = 123;if(true){
    console.log(abc);  *// expect: 123*
    abc = 456;
}
```

**奖金方案:**

```
console.log(abc); *// expect: undefined*
var abc = 123;
```

好了，希望你不要再惊讶了。JavaScript 是这样看的:

```
var abc;
console.log(abc);
abc = 123;
```

# `Var`在全球范围内

在浏览器中，全局范围被称为`window`对象。这里是`var`变量的另一个奇怪行为:所有的`var`变量都被添加到了`window`对象中。

```
var abc = 123;
let heya = 123;console.log(window.abc); *// expect: 123*
console.log(window.heya); *// expect: undefined*
```

# `Var` vs `Let` vs `Const`一言以蔽之

*   Var 不是作用域安全的。
*   Var 变量被吊起来。
*   默认情况下，Var 变量被添加到全局`window`对象中。
*   一旦声明，我们不能重新分配`const`变量。

# 功能范围及`Var`吊装

函数作用域是由函数提供的作用域。与其他作用域不同，`var`在函数作用域中声明的变量不会被提升到全局作用域，而是被提升到函数的最开始。

**场景 1:**

```
var abc = 123;function print(){
    console.log(abc); *// expect: undefined*
    var abc = 567;}print();
console.log(abc); *// expect: 123*
```

JavaScript 认为这是:

```
var abc;
abc = 123;function print(){
    var abc;
    console.log(abc); *// expect: undefined*
    abc = 567;
}print();
*// abc is referred to the variable defined in the global scope.*
console.log(abc); *// expect: 123*
```

**场景二:**

```
var abc = 123;function print(){
    console.log(abc); *// expect: 123*
    abc = 567;}print();
console.log(abc); *// expect: 567*
```

这应该很简单。JavaScript 是这样看的:

```
var abc;
abc = 123;function print(){
    *// Since there is no local 'abc'*
    *// we are getting the variable from the global scope.*
    console.log(abc); *// expect: 123*
    *// changing the value of 'abc'*
    abc = 567;
}
print();
*// after running the print() function,*
*// value of abc is changed.*
console.log(abc); *// expect: 567*
```

就这样！总之，永远不要使用`var`因为它是一段(咒骂语编辑)😅。

*多内容于* [***通俗易懂***](http://plainenglish.io/)