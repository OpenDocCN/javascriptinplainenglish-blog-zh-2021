# 是的，JavaScript 类是真正的类

> 原文：<https://javascript.plainenglish.io/yes-javascript-classes-are-real-classes-a87906b6b512?source=collection_archive---------14----------------------->

![](img/7bea1ba7c7300b4c12c5e3f7791f8c99.png)

你听说过像这样的争论吗？

JavaScript 中没有所谓的“类”, JavaScript 也不支持经典继承。JavaScript 被迫以各种方式偏离现代 OOP 的类概念(即 Java 类)，因为它的类语法是建立在原型继承之上的。这可能会导致新手和经验丰富的开发人员出现奇怪和混乱的行为。最好不要使用类语法，而是接受 JavaScript 的原型性质。

这种听起来令人费解的论点的变体经常被传来传去，但只要稍加挖掘，你很快就会发现这种论点没有任何分量。所以让我们拿起铁锹开始工作吧！

# JavaScript 类是不是充满了古怪？

**原论点:***“JavaScript 被迫以多种方式偏离现代 OOP 的类概念(意为 Java 类)，由于其类语法建立在原型继承之上的事实。这可能会给新手和经验丰富的开发人员带来奇怪和困惑的行为。”*

实际上，这些偏差大部分与原型继承无关，而与 JavaScript 的动态本质有关。python 语言提供了一个很好的有效性检测工具来对付这些类型的“奇怪的类行为”参数——如果一个反对 JavaScript 类的特定参数也适用于 python 类，那么这个参数一定没有太大的分量，否则，我们会看到 python 社区中的人拿着干草叉和尖桩到处跑，高呼“Python 类去死吧！”。所以，让我们列出一些经常被引用的论点，看看它们与我们的有效性检测工具相比如何。

**注意:**我打算让这个部分成为一个“活的”部分。我会继续更新它，以解决人们将来可能提出的问题。

## 实例可以在运行时改变类

在 JavaScript 中，可以使用 [Object.setPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf) 在运行时切换原型。在 Python 中，通过修改 __class__ 字段也可以做到这一点。如果不是 Python 中的问题，那就不可能是 JavaScript 中的“真正问题”。

```
class Square:
    width = 1
    height = 1class Circle:
    r = 1my_square = Square()
my_square.__class__ = Circleprint(isinstance(my_square, Square)) # False
print(isinstance(my_square, Circle)) # True
print(my_square.r) # 1
```

## 一个类的方法可以在声明后动态改变

Python 是一种非常动态的语言，所以它也支持这种行为。

```
class Square:
    width = 1
    height = 1
    def area():
        return width * heightmy_square = Square()
Square.area = lambda self: 5
print(my_square.area()) # 5
```

## 您可以实例化一个 JavaScript 类并接收一个完全不相关的实例

这是在讨论一个事实，即 JavaScript 构造函数能够返回一个不是构造类的实例的值。

```
class Square {
  constructor() {
    return { x: 2 }
  }
}const mySquare = new Square()
console.log(mySquare) // { x: 2 }
console.log(mySquare instanceof Square) // false
```

这也可以在 Python 中完成。

```
class Square:
    def __new__(*args):
        return {'x': 2}my_square = Square()
print(my_square) # {'x': 2}
print(isinstance(my_square, Square)) # False
```

# JavaScript 有类和经典继承吗？

**原论点:**“*JavaScript 中没有所谓的“类”，JavaScript 也不支持古典继承。”*

虽然类语法的确主要是原型的语法糖，但这本身并不能成为 JavaScript 没有类的令人信服的理由。毕竟，C++整体上不就是汇编/二进制的语法糖吗？有人可能会说，C++没有真正的函数，因为它只是标签和 gotos 的糖衣——你甚至可以在运行时做一些花哨的内存把戏，拉开窗帘，揭示函数如何运行的真相，因为，嗯，它是 C++，它可以让你做任何事情。也可以说 Python 类不是真实的，它们只是内置 type()函数的语法糖(尽管没人这么说)。用 Python 的类语法可以做的任何事情也可以用 type 函数动态地完成，然而，我们说 Python 有类。

那么 JavaScript 有类吗？JavaScript 支持经典继承吗？答案是绝对的**是的！只需要一点糖就能赋予一种语言特色。**

# 应该避免 JavaScript 类吗？

**原始论点:** *“最好不要使用类语法，而是拥抱 JavaScript 的原型本质。”*

是否要使用类语法取决于您。人们有正当的理由希望避免它。例如，您可能会发现继承已经是一个足够复杂的主题，拥有一种具有两种继承形式(经典和原型)的语言实在是太多了——最好保持简单，将一切都视为原型。或者，也许你不知道为什么你不喜欢类的语法，或者为什么你喜欢原型——很难精确地指出偏好背后的确切原因。如果这种“类是奇怪的，因为它们是建立在原型继承基础上的”理论一直被搁置，我不会感到惊讶，因为人们不确定他们不喜欢类语法的什么，这是一个容易指责的目标。

如果说我学到了什么的话，学习和发展你自己观点的最好方法是就这些事情进行对话，特别是与那些持相反观点的人，所以请随意在评论中开始讨论(只是，请尊重)。

不说这些:如果我收到一些评论，谈论如何简单地添加类语法以使 JavaScript 成为一种“成熟”的语言，或者因为它想看起来更面向对象，我不会感到惊讶。我将非常严厉地反对这个理论。这个论点是“反对团体只是盲目地遵循教条”论点的变体。这是一种非常有害的思想，它以伤害性的标签针对特定人群，比如“他们只是随大流”，或者“他们没有一个好的信仰理由”。这真的就像一个孩子感到沮丧，大喊“你就是不明白”，然后走开——这种行为永远不会帮助任何人学到任何东西。如果你不认为类语法是一个好的补充，那很好，告诉我为什么它不适合 JavaScript，给我实际的论据！不要只是说语言设计者不知道他们在做什么——这不是反对功能本身，而是反对功能背后的原因，这是一个非常无用的、破坏性的论点(也是一个逻辑谬误)。

**延伸阅读**

*   [反对的观点](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/this%20%26%20object%20prototypes/ch4.md#javascript-classes)。他们的结论恰恰相反:“但是这意味着 JavaScript 实际上有类吗？简单明了:没有。”
*   一个(有点过时)[关于“JavaScript 有类吗”的 StackOverflow 问题](https://stackoverflow.com/questions/2752868/does-javascript-have-classes)。
*   我有一个[类似的观点](http://stupidpythonideas.blogspot.com/2015/12/prototype-inheritance-is-inheritance.html#:~:text=The%20only%20difference%20is%20that,but%20let's%20ignore%20that%20here.)，也比较了 Python 类和 Javascript 类。
*   道格拉斯·克洛克福特—“精彩部分”[谈到](https://youtu.be/PSGEjv3Tqo0?t=1090)他完全否定了 JavaScript 类语法。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)