# 用简单的术语解释 JavaScript 的“this”关键字

> 原文：<https://javascript.plainenglish.io/explaining-javascripts-this-keyword-in-simple-terms-238e26b1d0df?source=collection_archive---------16----------------------->

在 JavaScript 中，您必须以前使用过“this”关键字。“this”关键字在 JavaScript 中可能有不同的含义，这取决于调用它的位置。本文的目的是向您展示一种简单的方法来确定这在特定场景中是指什么。

# “这”到底是什么？

![](img/ee0da430846acd2ef2ce7159efbe0f12.png)

‘this’ can be confusing (Photo by [sydney Rae](https://unsplash.com/@srz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral))

在 JavaScript 中，“this”关键字指的是在一个范围内控制/运行一组特定代码的对象(*通常使用的技术术语是执行上下文*)。这是对所有者的约束。简单地说，‘这个’指的是它所属的对象。因此，我们知道它可以在不同的上下文中指代不同的对象。让我们来看看这些简单的问题，以确定它指的是什么对象:

1.  Node.js 或客户端 JavaScript 中使用了“this”吗？*(在 Node 中，全局上下文中的 this 是指‘global this’，而在浏览器中是指‘window’对象)*
2.  问问你提到“this”的代码块的所有者是谁？(*注意，无论何时在函数中调用这个函数，都要弄清楚谁拥有这个函数。在那种情况下，这才是真正的参考。*)
3.  它是否明确地有界于一个函数？*(使用 call()和 apply()等方法。在这两种情况下，这些函数中传递的对象成为“this”的引用。稍后我们将简要地看一下它。)*

让我们通过不同的场景来理解这一点:

# ①这就其本身而言

单独调用时，它引用全局对象。

看看下面的例子:

```
console.log(this); // This will print window object
```

让我们回答我们的问题，以总结上述代码示例中的含义:

*   在这种情况下，我们使用的是普通的 JavaScript，这应该是指窗口对象。
*   我们看到没有类或方法拥有这个对象。因此，它将使用最广泛的全局范围，即窗口对象。
*   没有显式的函数绑定。

因此，我们可以断定这里指的是窗户。

**注:** *在上面的例子中，即使我们在一个函数内编写控制台语句，也会得到同样的结果。这是因为该函数属于全局窗口。*

# 2)这在一个函数内

正如我们之前所学的，如果这是在一个函数中调用的，我们需要查看拥有函数的*来推断这个对象的引用。*

看看下面的例子:

```
function calculateTaxes(){
  console.log(this); // This will return window
}
```

让我们回答我们的问题，以总结上述代码示例中的含义:

*   我们使用普通的 JavaScript，所以对象的全局引用是 window。
*   这里，该函数由窗口对象拥有。
*   该函数未显式绑定。

因此，我们可以得出结论，这里的“this”指的是窗口对象。

让我们看另一个例子:

```
"use strict"
function calculateTaxes(){
  console.log(this); // This will return window
}
```

记住‘this’对象是绑定到所有者的。如果我们在 JavaScript 中使用严格模式，它会阻止默认绑定*(本例中我们的默认绑定是全局对象窗口)。因此，在这种特殊情况下，“这”是未定义的，这是一种例外情况。*

# 3)这在一个类内

在一个类中，它指的是该类的一个对象。因此，您可以访问它的所有属性和方法。

看看下面的例子:

```
class Animals{ var name = 'Dog';
 var species;

 function sound(){
   // Identify what sound that animal makes and return value
 }
 console.log(this.name); // This will print Dog
}
```

让我们回答我们的问题，以总结上述代码示例中的含义:

*   在这种情况下，我们使用普通的 JavaScript。所以全局上下文就是窗口对象。
*   然而，这里我们看到代码块的所有者，也就是“this”被调用的地方，是动物类。
*   没有显式的函数绑定。

因此，我们可以得出结论，这里的“this”指的是动物类的对象。

**注:** *如果我们在声音函数内编写控制台语句。我们会得到同样的结果。因此，this.sound()也有效。既然，声音功能是动物类所拥有的，动物类仍然是‘这个’的拥有者。*

# 4)这与显式函数绑定

“this”可以与 call()和 apply()函数一起使用。这两个都是内置的 JavaScript 函数。它们的用途相同，但传递参数的方式不同(Call 方法单独获取每个参数，Apply 将它们作为数组)。

这两个函数本质上都是用一个给定的“this”对象和不同的参数调用一个函数。也就是说，我们可以指定我们想要传递的“这个”对象。让我们看一个例子:

```
var mansBestFriend = {
 species: "Dog",
 name: "Scotty"
}var introduceAnimal = function(food){
  console.log("This is " + this.name + ".");
  console.log("This " + this.species + " loves " + food + ".");
}// This is Scotty. This Dog loves Steak.
introduceAnimal.call(mansBestFriend, 'Steak');
introduceAnimal.apply(mansBestFriend, ['Steak']);
```

正如我们所了解的，调用和应用函数的第一个参数是“this”对象。在这里，我们明确指定，该对象是 mansBestFriend。

让我们回答我们的问题，以总结上述代码示例中的含义:

*   在这种情况下，我们使用普通的 JavaScript。所以全局上下文就是窗口对象。
*   它是在一个函数中被调用的，所以它本身会引用窗口对象，因为函数是由窗口拥有的。
*   然而，*我们使用 call/apply 方法显式绑定‘this’对象**。这意味着，我们需要查看什么对象被传递给这些函数，以推断这里的“This”指的是什么。由于 mansBestFriend 对象被传递给 call 和 apply，所以这里的‘this’指的是 mansBestFriend 对象。*

*你可以在这篇精彩的[文章](https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb#:~:text=call()%20and%20apply(),call%20expects%20each%20param%20individually.)中了解更多关于呼叫和申请的信息。*

*使用这种简单的技术，您可以很容易地确定在特定的执行上下文中“this”指的是什么。*

*识别对象的所有者，理解异常并寻找显式绑定(如果有的话)。现在，您可以像专业人士一样在 JavaScript 中使用“this”了。*

***感谢您阅读我的文章！***

***我的名字是毗湿奴·萨西德哈兰，我写技术文章、代码和讲故事。我的目标是把复杂的概念化繁为简，用通俗易懂的语言解释。我也分享激励过我的真实生活故事。***

***如果你喜欢这篇文章，你可能也会喜欢:***

*[](/why-you-should-stop-using-loops-88a6a789106e) [## 为什么应该停止使用循环

### 如果你和我一样，你在 JavaScript 中使用 for 和 while 循环的时间最长。我是说如果它得到了…

javascript.plainenglish.io](/why-you-should-stop-using-loops-88a6a789106e) [](/promises-in-typescript-27d887a8d380) [## 打字稿中的承诺

### 想象一下，你去店主那里买糖果。你要了一颗糖，店主答应了(即给了你一颗糖)

javascript.plainenglish.io](/promises-in-typescript-27d887a8d380) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*