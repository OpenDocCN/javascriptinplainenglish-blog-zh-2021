# JavaScript:这是什么？

> 原文：<https://javascript.plainenglish.io/javascript-what-is-this-3bd177378b66?source=collection_archive---------12----------------------->

## 理解 JavaScript 中“this”关键字的范围和上下文。

![](img/56daf0dde11006e485568f7201422b01.png)

Photo by [Emil Priver](https://unsplash.com/@emilpriver?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@emilpriver?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在编写 JavaScript 代码时，有一件事会让我们感到困惑，那就是关键字`**this**`。这是一个特殊的关键字，用来标识定义函数范围的自动性。在 JavaScript 中，每个函数在运行时都有一个对当前执行上下文的特殊引用，称为`**this**`，它从不引用原始类型，而是引用一个对象。

关于“this”关键字如何与执行上下文相关联，有四个基本规则，它们都取决于 JavaScript 函数的代码在哪里执行。在本文中，我们将分析这些规则，从与关键字`**this**`密切相关的 JavaScript 语言的一些关键概念开始，例如**范围**和**上下文**。

# 有些困惑

当谈到 JavaScript 中的`**this**`关键字时，不要认为它指的是类、对象、实例和面向对象编程世界中的所有其他东西。此外，不要将`**this**`关键字与其他编程语言进行比较。另一个需要澄清的重要事情是，功能的“上下文”和“范围”不是一回事。许多开发人员混淆了这些术语，将一个错误地描述为另一个。所以在继续之前，让我们先澄清这两个概念的含义。

## 范围和背景

**范围是指变量的可见性**。在 JavaScript 中，这是通过使用函数来实现的。当我们在函数内部使用`**var**`关键字时，你正在初始化的变量是函数私有的，在函数外部是看不到的。但是，如果我们在其中声明了其他函数，那么这些“内部”函数就可以访问该变量，因为它们在同一个范围内。函数还可以访问在内部和外部声明的变量，但不能访问嵌套函数内部声明的变量。这在 JavaScript 中称为范围。

**上下文**，另一方面**与对象**相关。它指的是函数所属的对象。当使用 JavaScript 'this '关键字时，它指的是函数所属的对象。执行上下文，其中`**this**`关键字被评估，只不过是位置**，其中**和**如何**一个特定的函数被调用。

# 全球范围

为了更好地理解这一基本规则，让我们从下面的代码片段开始:

```
function print () {
  console.log(`My name is ${this.name}`)
}print()
```

在前三行代码中，我们声明了一个`**print**`函数，它引用了`**this**`关键字，尤其是`**name**`属性。在我们调用函数之后。在这种情况下，`**this**`并不指向任何对象，而是指向浏览器全局范围`**Window**`，实际上试图通过以下方式修改我们的`**console.log**`:

```
function print () {
  console.log(this)
}print()
```

我们将获得类似这样的东西:

```
Window {window: Window, self: Window, document: document, name: "", location: Location, …}
```

全局范围没有一个名为`**name**`的属性，所以从前面的脚本返回的结果是:

```
My name is
```

当代码不在“严格模式”下运行时，会发生这种情况。事实上，如果我们试图通过在脚本开头添加`**'strict mode'**`来修改代码:

```
'use strict'function print () {
  console.log(`My name is ${this.name}`)
}print()
```

我们将获得一个`TypeError`:

```
Uncaught TypeError: Cannot read property 'name' of undefined
    at print (<anonymous>:4:34)
    at <anonymous>:7:1
```

如果你不知道什么是“严格模式”，看看[官方文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)。

# 隐式结合

为了更好地理解第二条规则，让我们回到上一个例子中定义的漂亮的`**print**`函数，并创建两个引用它的对象。请记住，我们的目标是能够使用`**this**`关键字查看函数的定义，并理解它所引用的内容。这个规律 80%的时候能够让我们明白`**this**`指的是什么。现在考虑下面的代码:

```
'use strict'function print () {
  console.log(`My name is ${this.name}`)
}const person1 = { name: 'Paul', print: print }
const person2 = { name: 'Steve', print: print }
```

在代码示例中，我们有两个对象，`**person1**`和`**person2**`，它们有两个属性。第一个属性是`**name**`:一个字符串，标识一个人的名字。现在，如果我们想在对象`**person1**`和`**person2**` 上调用`**print**`函数，我们必须使用“点”`.`，如下所示:

```
person1.print()
person2.print()
```

为了理解关键字`**this**`指的是什么，我们首先需要看一下函数的左边。如果有一个“点”,向点的左边看，找到由`**this**`关键字引用的对象。

在上例中，`**person1**`和`**person2**`位于*点的“左侧”，这意味着关键字`**this**`首先指向`**person1**`对象，然后指向`**person2**`对象。在`**print**`函数内部，JavaScript 解释器将`**this**`更改为`**person1**`和`**person2**`。*

*如果我们执行代码，您将获得以下结果:*

```
*Paul
Steve*
```

*现在让我们举一个类似的，但是稍微高级一点的例子:让我们在我们的`**person2**`对象中定义第三个属性`**father**`。该属性将是对`**person1**`的引用:*

```
*'use strict'function print () {
  console.log(`My name is ${this.name}`)
}const person1 = { name: 'Paul', print: print }
const person2 = { name: 'Steve', print: print, **father**: person1 }person2.print()
person2.father.print()*
```

*如上所述，在 80%的时间里我们需要看到*【点的左边】*来理解当我们调用`**print**`函数时`**this**`关键字指的是谁。第一次调用 print 时，点左边的对象是`**person2**`，所以`**this.name**`会引用字符串“Steve”。然而，当第二次调用`**print**`时，在点的左边有`**father**`属性，它是对`**person1**`的引用，所以`**this.name**`将引用字符串“保罗”。*

# *显式绑定*

*让我们重新考虑一下上一段给出的例子，但是这次不在`**print**`函数和`**person**`对象之间创建任何引用:*

```
*'use strict'function print () {
  console.log(`My name is ${this.name}`)
}const person = { name: 'Paul' }*
```

*我们知道要知道`**this**`关键字指的是什么，我们首先需要看看函数是在哪里被调用的。现在，问题是“我们如何调用`**print**`，但是用引用`**person**`对象的`**this**`关键字调用它？”不能因为`**person**`没有`**print**`功能就直接用`**person.print()**`。在 JavaScript 中，每个函数都包含一个允许我们这样做的方法，这个方法叫做`**call**`。*

*`**call**`是每个函数都有的一个方法，它允许你指定，作为第一个参数，调用函数的上下文。换句话说，您传递的第一个参数将是`**this**`关键字在该函数中引用的内容。欲了解更多信息，请查阅[文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)。*

*现在我们可以这样在`**person**`上下文中调用`**print**`:*

```
*print.**call**(person)*
```

*相比隐式绑定规则，这次我们不用看*【点的左边】*，而是只看`**call**`函数的第一个参数；这将是`**this**`将在`print`函数中引用的范围。这就是为什么这个规则被定义为显式绑定，因为我们显式地(使用`**.call**`)指定了`**this**`关键字所指的内容。*

```
*'use strict'function print () {
  console.log(`My name is ${this.name}`)
}
const person = { name: 'Paul' }
print**.call**(person)*
```

*如果我们执行下面的代码，结果将是:*

```
*Paul*
```

*现在让我们试着修改我们的`**print**`函数，增加两个参数`**gender**`和`**age**`。*

```
*function print (gender, age) {
  console.log(`My name is ${this.name}, I'm a ${gender} of ${age} years old!`)
}*
```

*现在，如果我们想向被调用的函数传递一些参数，我们必须在指定第一个参数后一次传递一个参数:*

```
*'use strict'function print (gender, age) {
  console.log(`My name is ${this.name}, I'm a ${gender} of ${age} years old!`)
}const person = { name: 'Paul' }
const arguments = ['male', 37]
print.**call**(person, **arguments[0]**, **arguments[1]**)*
```

*下面是如何将参数传递给用`**call**`函数调用的函数。然而，不得不从我们的`**arguments**`数组中一个接一个地传递参数有点烦人。如果我们可以将整个数组作为第二个参数传递，JavaScript 会为我们将它们展开，那就太好了。这正是`**apply**`功能的作用。*

*`**apply**`的工作方式与`**call**`完全一样，但是我们可以传递一个数组，apply 会负责将数组的每个元素作为参数分配给函数，而不是一个接一个地传递参数。*

*现在，使用`**apply**`、**、**我们的代码可以这样修改:*

```
*'use strict'function print (gender, age) {
  console.log(`My name is ${this.name}, I'm a ${gender} of ${age} years old!`)
}const person = { name: 'Paul' }
const arguments = ['male', 37]
print.**apply**(person, **arguments**)*
```

*到目前为止，通过我们的*“显式绑定”*规则，我们已经了解了`**call**`和`**apply**`，它们都允许您调用一个函数，指定`**this**`关键字将引用什么。我们现在需要知道的最后一个函数是`**bind**`。该函数与`**call**`相同，但它不是立即调用该函数，而是返回一个新的函数，我们可以稍后调用。因此，如果我们使用`**bind**`查看我们之前的代码，它将如下所示:*

```
*'use strict'
function print (gender, age) {
  console.log(`My name is ${this.name}, I'm a ${gender} of ${age} years old!`)
}const person = { name: 'Paul' }
const arguments = ['male', 37]const newPrint = print.**bind**(person, arguments[0], arguments[1])
newPrint()*
```

## *新操作员*

*另一种理解这是指什么的方式是新的关键字。如果你不熟悉 JavaScript 中的`**this**`关键字，那么考虑一下，每次你用`**new**`关键字调用一个函数，JavaScript 解释器都会为你创建一个新的对象，并把它命名为`**this**`。所以，当然，如果用关键字`**new**`调用一个函数，`**this**`指的是解释器创建的新对象:*

```
*function Person (name, age) {
  **this**.name = name 
 **this**.age = age
 **this**.print = function () {
    console.log(`Hello I'm ${**this**.name} and I'm ${**this**.age}!`)
  }
}const me = new Person('Davide', 37)
me.print()*
```

*如果我们使用 JavaScript 类，我们将获得相同的行为:*

```
*class Person {
  constructor(name, age) {
    **this**.name = name
    **this**.age = age
  } print () {
    console.log(`Hello I'm ${**this**.name} and I'm ${**this**.age}!`)
  }
}const me = new Person('Davide', 37)
me.print()*
```

*在这两种情况下，`**this**`将引用使用`**new**`操作符创建的对象，在这种情况下，只需查看*“点的左边”*即可了解`**this**`引用的是谁。在刚刚显示的示例中，我们将得到以下结果:*

```
*Hello I'm Davide and I'm 37*
```

# *词汇装订*

*JavaScript 中的`**this**`关键字可能比它应该的更复杂。好消息是，下一条规则是最直观的。您可能听说过并使用过“*箭头功能*”。它们从 ES6 开始引入。它们允许您以更简洁的格式编写函数:*

```
*persons.map(person => person.name)*
```

*甚至比简洁性更重要的是，当涉及到`**this**`关键字时，这些类型的函数采取了更直观的方法。与普通函数不同，箭头函数没有`**this**`。相反，`**this**`是词汇上确定的。这是一种优雅的说法，即`**this**`是根据在原型链中寻找变量的正常规则确定的。让我们用一个例子来更好地阐明这个概念，考虑下面的代码示例:*

```
*const person = {
  name: 'Davide',
  age: 37,
  gender: 'male',
  frameworks: ['Fastify', 'Angular', 'Vue'],
  print() {

    const message = `My name is ${this.name}, 
      I'm a ${this.gender} of ${this.age} years old! 
      My favourite frameworks are: `

    const frms = this.frameworks.reduce(function (str, f, i) {

      if (i === this.frameworks.length - 1) {
        return `${str} and ${f}.`
      } return `${str} ${f},`
    }, "")    console.log(message.concat(frms))
  }
}person.print()*
```

*如果我们运行这段代码，我们将获得以下错误:*

```
*if (i === this.frameworks.length - 1) {
               ^
TypeError: Cannot read property 'frameworks' of undefined*
```

*当我们调用`**person.print()**`时，我们期望看到*“我叫大卫，男性，37 岁！……”*。根据错误，`**this.frameworks**`未定义。让我们通过我们的步骤来理解`**this**`指的是什么，最重要的是试图理解为什么它不应该指`**person**`。*

*首先，我们需要看看函数是在哪里被调用的。该功能被传递给`**.reduce**`，因此`**this**`的范围与`**person**`的范围不同。事实上，我们从未见过匿名函数的调用，因为在`**.reduce**`的实现中，JavaScript 会自己调用。这是个问题。我们必须指定我们传递给`**.reduce**`的匿名函数在`**person**`上下文中被调用。这样`**this.frameworks**`将引用`**person.frameworks**`。所以，我们可以使用`**.bind**`:*

```
*const person = {
  name: 'Davide',
  age: 37,
  gender: 'male',
  frameworks: ['Fastify', 'Angular', 'Vue'],
  print() {

    const message = `My name is ${this.name}, 
      I'm a ${this.gender} of ${this.age} years old! 
      My favourite frameworks are: `

    const frms = this.frameworks.reduce(function (str, f, i) {

      if (i === this.frameworks.length - 1) {
        return `${str} and ${f}.`
      } return `${str} ${f},`
    }**.bind(this)**, "") console.log(message.concat(frms))
  }
}person.print()*
```

*现在，如果我们运行代码，结果是:*

```
*My name is Davide, I'm a male of 37 years old! My favourite frameworks are:  Fastify, Angular, and Vue.*
```

*我们已经看到了`**.bind**`如何再一次为我们解决问题，但是它与箭头函数有什么关系呢？前面我们说过，在 arrow 函数中，这是由词汇决定的，然后遵循原型链，直到找到 frameworks 变量。在上面的例子中，按照原型链，这指的是人，因此是`**this.frameworks**`。没有理由仅仅因为我们使用了`**.reduce**`函数就创建新的执行上下文。因此，通过移除`**.bind(this)**`函数并使用匿名箭头函数，代码将如下所示:*

```
*const person = {
  name: 'Davide',
  age: 37,
  gender: 'male',
  frameworks: ['Fastify', 'Angular', 'Vue'],
  print() {

    const message = `My name is ${this.name}, 
      I'm a ${this.gender} of ${this.age} years old! 
      My favourite frameworks are: `

    const frms = this.frameworks.reduce(**(str, f, i) => {**

      if (i === this.frameworks.length - 1) {
        return `${str} and ${f}.`
      } return `${str} ${f},`
    **}**, "") console.log(message.concat(frms))
  }
}person.print()*
```

*在这种情况下，结果也将是:*

```
*My name is Davide, I'm a male of 37 years old! My favourite frameworks are:  Fastify, Angular, and Vue.*
```

*这个结果表明箭头功能没有自己的`**this**`。相反，JavaScript 解释器将在父范围内搜索，以确定它引用了什么。*

# *结论*

*在本文中，我们仔细研究了`**this**`,以及它的范围是如何随着它的使用方式和位置而变化的。所以，如果你把这四个小规则应用到实践中，每次你在一个函数中找到关键字`**this**`，你就能明白它指的是什么。目前:*

```
***HAPPY, CODING!***
```

# *文献学*

*[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this?retiredLocale=it) [## this - JavaScript | MDN

### 与其他语言相比，函数的 this 关键字在 JavaScript 中的行为略有不同。它也有一些…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this?retiredLocale=it) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) [## function . prototype . bind()-JavaScript | MDN

### bind()方法创建了一个新函数，当调用该函数时，它的 this 关键字被设置为提供的值，并带有一个…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) [## function . prototype . call()-JavaScript | MDN

### 调用时用作此的值。注意:在某些情况下，可能不是该方法看到的实际值。如果…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) [## 箭头函数表达式- JavaScript | MDN

### arrow 函数表达式是传统函数表达式的一种紧凑替代形式，但它是有限的，不能…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)*