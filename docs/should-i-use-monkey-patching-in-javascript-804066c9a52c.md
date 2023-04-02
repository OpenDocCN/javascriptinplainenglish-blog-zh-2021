# JavaScript 中应该用猴子打补丁吗？

> 原文：<https://javascript.plainenglish.io/should-i-use-monkey-patching-in-javascript-804066c9a52c?source=collection_archive---------5----------------------->

## 猴子补丁展示了 JavaScript 的灵活性以及它的一些危险

![](img/ca56129c148cfc9799495e259b220637.png)

Photograph from Jamie Haughton at Unsplash, Illustration by David Fekke

Monkey Patching 是 JavaScript 中用自己的函数替换 JavaScript 对象中的函数的功能。这可以派上用场，但也很危险。JavaScript 的优势之一是它能够轻松地修改对象和模块。这也使得引入新的错误变得相当容易。

这种功能也可以在 Objective-C 和 Swift 等语言中找到，在这些语言中，开发人员可以使用一种称为“方法切换”的运行时功能来交换他们类中方法的功能。

为了演示这个功能，我们可以创建一个具有简单 add 函数的对象。

然后我们可以实例化这个对象，并在我们的对象上调用`add`函数。

```
const MathObject = new SimpleMathObject();
const result = MathObject.add(1, 2);
console.log(`Result of 1 + 2 = ${result}`);
// Output: Result of 1 + 2 = 3
```

# 添加猴子补丁

要给我们的对象添加一个猴子补丁，我们只需要给实例化对象上的`add`函数分配一个新函数。我们需要得到一个对原始函数的引用，这样我们就可以在我们的新函数中继续使用它，或者可能在我们完成修补后将它重新分配给对象。

我们现在可以添加我们自己版本的`add`功能，而不必改变`SimpleMathObject`的原始版本。如果我们需要给这个对象注入一些新的功能，这可能是有用的。

使用`class` [关键字](https://fek.io/blog/why-you-should-not-use-classes-in-java-script/)或[对象原型](https://fek.io/blog/crockford-objects-in-java-script/)的一个问题是会让你的对象对这种类型的操作敞开大门。如果你不希望你的函数被猴子打补丁，有一些方法可以防止这种类型的执行发生在你的代码中。实现这一点的一种方法是在返回对象时使用工厂函数和`Object.freeze`。

现在，如果您试图用自己的函数替换`add`函数，就像下面的例子，JavaScript 引擎将抛出一个 TypeError

尝试执行这段代码时出现的错误应该类似于下面的错误。

```
TypeError: Cannot assign to read only property 'add' of object '#<Object>' at file:///Users/davidfekke/Documents/monkeypatch/monkey.js:39:23
```

# 结论

猴子补丁是 JavaScript 中一个非常强大的概念。您可以使用向现有的库或模块中添加方面或注入新功能。它也可能是危险的。但是如果你不希望你的代码被猴子修补，你可以使用 Object.freeze 使你的对象只读。

您当然可以在您的 JavaScript 应用程序中使用这个特性，但是要注意，如果您忘记了这个更改，那么当您更改一个对象的默认功能时，可能会产生意想不到的行为。或者更糟的是，下一个开发您的代码的开发人员没有意识到这种变化。

*最初发布于*[*https://fek . io*](https://fek.io/blog/should-i-use-monkey-patching-in-java-script/)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io)