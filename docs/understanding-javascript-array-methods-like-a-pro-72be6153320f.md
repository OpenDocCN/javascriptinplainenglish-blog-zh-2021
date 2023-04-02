# 像专家一样理解 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/understanding-javascript-array-methods-like-a-pro-72be6153320f?source=collection_archive---------5----------------------->

![](img/1e61ae1c710a26b0ad16fb818431a034.png)

Photo by [Kevin Ku](https://www.pexels.com/@kevin-ku-92347?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/black-farmed-eyeglasses-in-front-of-laptop-computer-577585/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

如果你真的想成为 JavaScript 的专家，那么你必须能够完全理解数组方法的工作原理以及何时使用它们。在这个由多个部分组成的系列中，我将解释如何通过学习 JavaScript 中最常见的数组方法来提高您的 JavaScript 知识和技能，从而成为一名更好的程序员。在本系列中，我们将探索 JavaScript 必须提供的所有不同类型的数组方法，例如 **forEach、map、filter/find、reduce 和一些**。

我们开始吧！😃

# 来自过去的爆炸

For 循环已经成为过去，随着新一代编程语言中出现新的数组方法，它也开始变得过时。作为一名计算机科学专业的学生，我所学的只是如何使用 for 循环，主要是因为我们使用的都是 Java。在大学里，他们没有教我们，更不用说允许我们，使用除 for 循环之外的任何其他方法来迭代数组。傻吧？🥴

直到我开始研究 JavaScript 时，我才开始了解可以用来循环数组的替代方法的字典。我记得我第一次遇到 **forEach** 方法是在寻找一个关于堆栈溢出的问题的答案时，我心想，“真的有那么简单吗？”从那以后，我很少在应用程序中使用 for 循环。实际上，我开始回到以前定义 for 循环的其他文件中，并将它们改为使用 forEach。从那时起，我开始去除使用旧的 for 循环的习惯，开始使用更现代的方法。

闲聊够了，让我们看看如何开始将这些数组方法集成到我们的应用程序中…

# forEach()方法

我认为最好从 JavaScript 提供的最简单的数组方法开始，并从那里开始。让我们看看下面的例子:

```
const names = ['rick','morty','summer','kate','jerry','snowball']for(let i = 0; i < names.length; i++){
  console.log(names[i]);
}// output
// 'rick','morty','summer','kate','jerry','snowball'
```

上面的代码是一个非常简单的例子，说明了我们如何遍历一个名称数组，并将每个名称打印到控制台。现在，这对于这样一个简单的例子来说已经很好了，但是一旦我们开始进入更复杂的数组(比如 2D 或 3D 数组)，这就开始变得非常混乱(我们将在本系列的后面看到更复杂的例子)。

在处理 for 循环时，我们还必须考虑数组的界限。在上面的例子中，如果我们试图访问 names[i+1],这可能会导致我们的输出变得不确定，并且很可能抛出错误。对我们来说幸运的是，JavaScript 有一个方法可以处理这个问题，而无需我们去考虑它。

输入 forEach 方法。🙏

```
const names = ['rick','morty','summer','kate','jerry','snowball']names.forEach(name => console.log(name));// output
// 'rick','morty','summer','kate','jerry','snowball'
```

看一下上面的代码。在这里，我用一个 **forEach** 方法替换了我们的 for 循环，该方法给出了与前面代码相同的结果。从编程的角度来看，这看起来更干净，可读性更强，但是它是如何工作的呢？类似地，它的工作方式就像一个 for 循环，遍历数组中的元素，但不同的是 forEach 为我们跟踪数组索引，这意味着我们不必再担心访问数组边界之外的索引。

用 laments 的话来说，forEach 说，“对于数组‘names’中的每个名字，用 name 做一些事情”，在我们的例子中，这只是简单地记录我们的 name 元素的值。

如果我们需要访问数组的索引呢？我们能使用 forEach 方法做到这一点吗？当然可以！forEach 方法有一个 index 参数，它给出了我们当前所在元素的索引。看看下面的代码，看看我们如何在上面的例子中利用 index 参数:

```
const names = ['rick','morty','summer','kate','jerry','snowball']names.forEach((name,index) => console.log(`${index}: ${name}`));// output
// '0: rick','1: morty','2: summer','3: kate','4: jerry','5: snowball'
```

请注意，我们现在能够记录数组索引以及数组的每个元素，当我们需要有条件地索引数组的特定元素时，这给了我们更多的灵活性。forEach 循环的一个缺点是，当我们遇到像 for 循环那样的特定条件时，我们不能提前退出循环。对于这个用例，使用 For 循环实际上更好。

但我记得你说过 for 循环已经是过去的事了？没错，它们是，但是对我们来说幸运的是，JavaScript 已经找到了用 **find()** 方法消除这个用例中 for 循环的方法。

# 何时使用 forEach()方法

通常，forEach 方法用于代替 for 循环，使它们更具可读性。老实说，我发现自己不再经常使用 forEach 方法了，因为我主要可以使用 **map()** 和 **reduce()** 方法来完成我需要的所有事情，但是我们稍后会谈到这一点。

# find()方法

以前，当我们需要有条件地提前跳出 for 循环时，我们需要编写类似下面这样的代码:

```
const names = ['rick','morty','summer','kate','jerry','snowball']for(let i = 0; i < names.length; i++){
 if(names[i] === 'summer'){
   console.log(`${i}: ${names[i]}`)
   break;
  }
}// output
// '2: summer'
```

请注意，一旦 for 循环找到元素“summer”，它会立即停止对数组的迭代，并退出 for 循环。不幸的是，上面我们钟爱的 forEach 方法不这样做，除非我们有条件地在方法中抛出一个不建议的错误。

输入 find()方法！

让我们看看如何使用与上述 for 循环相同的条件来使用 find 方法:

```
const names = ['rick','morty','summer','kate','jerry','snowball']const result = names.find(name => name === 'summer');
console.log(result)// output
// 'summer'
```

同样，这个方法给我们留下了一个比上面的 for 循环例子更加清晰易读的解决方案。find 方法遍历我们的数组，返回我们正在寻找的元素的第一个实例，如果没有找到该元素，将返回 *undefined* 。在这种情况下，我们要搜索的元素再次是“夏季”。如果数组中有不止一个元素呢？正如我之前所说的，find 方法返回我们正在寻找的元素的第一个实例**。看看下面的例子:**

```
const names = ['rick','morty','jerry','kate','jerry','rick']const result = names.find((name,index) => {
 if(name === 'jerry'){
    console.log(`I found ${name} at index: ${index}`)
    return name;  
  }
});// output
// 'I found jerry at index: 2'
```

我们可以看到，即使“jerry”位于数组中的两个不同位置，find 方法也会返回第一个“jerry”实例，它恰好位于数组的索引 2 处。注意，我们也可以像上面的 forEach 方法一样，获取数组中元素所在的索引。

看来杰瑞并不难找到…

![](img/30e701538837a98796baeb4926aad76c.png)

memegenerator.net Sad jerry rick and morty — Caption

# 何时使用 find()方法

当我们需要在一个数组中找到一个特定的元素而不需要遍历整个数组时，find 方法是很有用的。例如，我们可能需要查找具有唯一用户 id 的特定用户或具有特定产品代码的产品。如果我要搜索的数组中有大量元素，并且不想遍历整个数组来找到我要找的确切元素，我通常会使用这种方法。

所以在一个数组中找到一个元素是很酷的事情，但是如果我们想在一个数组中找到所有符合给定条件的元素呢？JavaScript 再次想到了这一点，它被称为 filter 方法。

# filter()方法

假设我们在一个数组中有一整个星系的元素，需要找到满足特定条件的所有元素。最初我们可以准备类似这样的东西:

```
const galaxy = ['rick','morty','jerry','kate','jerry','rick']let ricks_found = [];for(let i = 0; i < galaxy.length; i++){
 if(galaxy[i] === 'rick'){
   ricks_found.push(galaxy[i]);
  }
}console.log(ricks_found);
// output
// ["rick","rick"]
```

在这个例子中，我们迭代我们的 galaxy 数组来寻找所有的“rick”元素。一旦在我们的星系中发现一个“rick”元素，我们就将结果推送到我们新定义的“ricks_found”数组中，并记录结果。如我们所见，我们能够在数组中找到仅有的两个“rick”元素。让我们看看如何利用过滤方法来获得相同的结果:

```
const galaxy = ['rick','morty','jerry','kate','jerry','rick']const ricks_found = galaxy.filter(name => name === 'rick');console.log(ricks_found);
// output
// ["rick","rick"]
```

再一次，我们发现了一个更干净的解决方案。filter 方法与 find 方法非常相似，因为一旦找到一个实例，它就不会中断循环，而是继续循环数组的其余部分，找到所有符合我们标准的元素。如果我们试图过滤数组中的元素“summer ”,我们最终会得到一个空数组。

# 何时使用 filter()方法

当我们只需要数组中的特定元素时，filter 方法非常方便。假设我们需要找到与特定客户匹配的所有发票，或者我们需要显示名字相似的所有用户，那么我们可以利用过滤方法轻松地做到这一点。当在表格中显示数据时，我倾向于经常使用这种方法，我需要过滤数据以获得更小的结果集。我会说这是所有方法中我第二常用的方法。

# 总结一下

这样，您离像专家一样理解 JavaScript 数组方法又近了一步！在本文中，我们研究了 for 循环是如何慢慢消失的，以及我们可以使用什么来使数组迭代更加灵活和可读。我们能够涵盖何时以及如何使用像 **forEach()、find()和 filter()** 这样的方法的基本用例。希望从这些更简单的数组方法开始可以帮助您更好地理解这些方法的概念，并推动您成为一名更有经验、更优秀的开发人员。

感谢您阅读我的另一篇文章。我希望你们都像我写这篇文章一样喜欢阅读它。当我发布本系列的第二部分，我们将讨论更高级的 JavaScript 数组方法时，请不要忘记关注我以获得通知。

下期再见！👋

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)