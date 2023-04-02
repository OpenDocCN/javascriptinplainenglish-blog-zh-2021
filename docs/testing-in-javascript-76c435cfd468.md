# 用 JavaScript 测试代码的简单技术

> 原文：<https://javascript.plainenglish.io/testing-in-javascript-76c435cfd468?source=collection_archive---------12----------------------->

能够测试你写的代码是编码的一个重要部分。对于我参与的几个项目，在为应用程序编写了一些代码之后，我会进入应用程序来测试代码，检查是否一切都按预期运行，以及我没有破坏任何东西。

然而，有另一种方法可以测试我们的代码，而不用进入我们的应用程序。这是通过编写一些我们可以用命令运行的测试代码来实现的。这个测试代码将让我们知道是否一切都正常工作(假设我们正确地编写了测试)。

![](img/92b2afddf477bc10f7a6e1627e40950e.png)

Photo by [Nguyen Dang Hoang Nhu](https://unsplash.com/@nguyendhn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这很有帮助，因为当我们对应用程序进行更改时，我们可以运行一个测试命令，看看我们的代码是否正常工作。对于测试，您可以使用几个框架。但是为了演示测试是如何工作和运行的，我将浏览一些不需要框架的代码，并测试 Node.js 中的简单函数。

我将使用的例子是**地图**函数。这显然是不实际的，因为 map 函数是内置在 JavaScript 中的，我们永远也不需要创建这个函数。然而，这是一个基本的功能，大多数人都知道它的作用和工作原理。因此，将更容易看到为什么测试工作或失败。

因此，在一个 JavaScript 文件中，我们可以编写我们的`forEach()`函数，然后将它作为一个模块导出，这样我们以后可以在项目的其他地方导入和使用它(我们也应该能够在我们的测试文件中导入它)。该映射将被定义如下:

```
map(arr, fn) {
  const result = [];
  for(let i = 0; i < arr.length; i++){
    result.push(fn(arr[i], i));
  }
  return result;
}
```

目的是通过我们的数组运行一个循环，并通过一个函数运行它，该函数将结果从函数推送到一个新的数组，然后返回该数组。现在我们已经创建了我们的地图，我们可以创建我们的测试来看看它是否正常工作。在测试中，我们可以使用任何你可以在数组中使用的通用语句。

你如何测试并不重要。您可以测试映射字符串，在每个字符串的末尾连接一些东西，或者使用数字并对数字执行一些数学运算。重要的是你知道你想要的预期输出是什么。

因此，对于这个测试，我将使用一个简短的数字数组，并将数组中的每个数字减 1(这样我就可以简单地计算出结果数组应该是什么)。

首先，我们需要创建一个文件来编写测试，并确保文件名以 **.test.js** 结尾(例如 **index.test.js** )。在这个文件中，我们测试我们的地图。你可以看到下面的测试:

```
const result = map([1,2,3], value =>{
  return value - 1;
});
if(result[0] !== 0) {
  throw new Error(`Expected to find 0, but found ${result[0]}`)
}
if(result[1] !== 1) {
  throw new Error(`Expected to find 1, but found ${result[1]}`)
}
if(result[2] !== 2) {
  throw new Error(`Expected to find 2, but found ${result[2]}`)
}
```

如您所见，我们只是在[1，2，3]的数组上测试 map 函数，并列出我们期望每个索引的结果的条件语句。如果结果不符合预期，代码会抛出一个错误，指出结果应该是什么以及它实际上是什么。如果我们在终端中使用以下命令运行该文件:

```
node index.test.js
```

我们不会看到任何好事发生，因为如果我们没有出错，我们的测试已经通过了。如果我们在地图上犯了一个错误，就可能会导致错误，就像我们从 1 而不是 0 开始循环一样。这将导致我们的测试失败，代码将抛出一个错误。

就这样！我希望本文能派上用场，帮助您成功测试代码。

*多内容于* [***浅显易懂***](https://plainenglish.io/)