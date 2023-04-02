# 使用 React 和 TypeScript 进行密码验证

> 原文：<https://javascript.plainenglish.io/password-validation-using-react-and-typescript-5230079dff89?source=collection_archive---------3----------------------->

## 了解如何使用 React 挂钩和 TypeScript 验证密码

![](img/15cb0d50878aedd763dffff39694d00d.png)

Photo by [Edgar Chaparro](https://unsplash.com/@echaparro?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 内容

*   介绍
*   以打字打的文件
*   入门指南
*   捕获数据
*   添加验证
*   解决办法

# 介绍

在本文中，我将向您介绍我的思考过程，并解释我如何以及为什么使用 React、React 钩子和 TypeScript 来创建健壮的密码验证。

我将介绍以下类型的验证:

*   有效长度
*   大写字母
*   小写字母
*   数字
*   特殊字符
*   密码匹配

# 以打字打的文件

> 什么是 TypeScript？

TypeScript 是添加了类型、类和模块的 JavaScript。经常被描述为，“类型脚本就像 JavaScript，但是没有什么惊喜。”TypeScript 语言在大多数文本编辑器中提供了附加的类型注释和类型检查选项。甚至在编译之前。

> 我们为什么要用它？

**及早发现漏洞**:我敢肯定你想知道它是如何及早发现漏洞的。TypeScript 通过类型检查在早期捕捉常见的错误。

**可预测性:**当你写代码的时候，TypeScript 会阻止对最初定义的任何东西进行修改。例如，如果一个变量被声明为布尔值，它将始终是布尔值。在代码的后面，这个变量不会变成一个字符串。这增加了函数按照最初的意图工作的机会。

**可读性:**添加严格类型和定义元素增加了必要的“语法糖”来理解代码在做什么。

如果你有兴趣了解更多关于 TypeScript 的知识，请查看官方 TypeScript [网站](https://www.typescriptlang.org/)。

# 入门指南

我假设如果你正在阅读这篇文章，你熟悉如何在本地启动和运行 react typescript 项目。如果没有，这里有一个快速演练，介绍如何开始运行。(我用的是 mac，所以很抱歉 windows 用户我帮不了你)

1.  创建一个目录并导航到其中。

```
mkdir typescript-medium-validation && cd typescript-medium-validation
```

2.使用以下命令安装 TypeScript React 项目。

*注意:您需要在您的计算机上安装节点来运行这个命令*

```
npx create-react-app react-typescript-password-validation --template typescript
```

3.导航到项目中。

```
cd react-typescript-password-validation
```

4.在您喜欢的代码编辑器中打开项目，并运行 start 命令。

```
npm start or yarn start
```

完美工程蓄势待发！

要在`App.tsx`中快速启动并运行，复制并粘贴这个启动代码。

在代码中，我们给我们的应用程序函数赋予了`ReactElement.`类型

关于 TypeScript 需要注意的一件重要事情是，在下面的用例中，我们创建了一系列 React 的 useState 挂钩，TypeScript 实际上是自动为它们提供类型。我们不需要这么做。

# 捕获数据

为了开始验证密码，我们需要从输入中获取值。现在有了 React 中的 TypeScript，这可能会感觉有点过于复杂和棘手。

为了真正利用 TypeScript 的好处，我们需要给我们的函数一个类型。在这种情况下，使用的类型是 **React。change event<HTMLInputElement>**

代码块中发生的事情是，我们创建了一个从`event.target`析构`value`和`name`的函数，然后我们将这些变量传递给我们的`setPassword`分派函数，以根据输入的名称和用户输入的值来更新值

现在我们有了这个函数，我们可以把它添加到输入的`onChange={ inputChange }` 处理程序中。

如果你想更深入地研究 React Events，可以看看我的另一篇文章“在 TypeScript 中反应事件”。我的文章和指南将更深入地理解 TypeScript 中的 React 事件，并将通过代码示例介绍最常用的 React 事件。

[](https://medium.com/@steven_creates/react-events-in-typescript-665a6a4c5b83) [## 在 TypeScript 中反应事件

### 在本指南+文章中，我们将使用 TypeScript 处理 React 功能组件中的事件。

medium.com](https://medium.com/@steven_creates/react-events-in-typescript-665a6a4c5b83) 

# 添加验证

让我们开始在代码中添加验证，并更新布尔值，以显示密码是否满足这些条件。

我将使用 useEffect React 钩子来完成我们所有的验证。实际上，我们只需要对第一个密码进行验证，唯一需要验证第二个密码输入的时候是我们将它与第一个密码进行比较，看它们是否匹配。

**使用效果:**

在 useEffect 中，如果满足密码字符串的条件，我们将添加所有的 useState 调度。

```
useEffect(() => {}, [password, requiredLength]);
```

**有效长度:**

在我们的起始代码中，我们将一个`requiredLength`初始状态设置为 8。现在，这不需要在 state 中设置，我们可以很容易地将一个变量设置为 8，并进行相同的比较。我们在这里做的是获取密码的长度，然后进行比较，如果它等于或大于所需的长度，如果在三元组中等于真，我们将返回真，否则返回假。

如果你不熟悉三元语法，我强烈推荐你去看看。对三元组的快速解释如下:首先提供一个评估或比较，如果等于真，则返回下一个，如果不等于真，则返回 else `evaluation ? return : else`。希望这能让事情变得更清楚。

```
setValidLength(password.firstPassword.length >= requiredLength ? true : false);
```

**大写:**

这里我们将使用逻辑运算符`!==`,其计算结果为不等值或不等类型。如果我们将字符串转换为小写，然后将它与第一个密码进行比较，我们将能够确定它们在字符串中是否为大写。

```
setUpperCase(password.firstPassword.toLowerCase() !== password.firstPassword);
```

**小写:**

我们可以用我们现在从大写字母例子中知道的东西，把字符串转换成大写字母，然后做一个比较。

```
setLowerCase(password.firstPassword.toUpperCase() !== password.firstPassword);
```

**编号:**

当我们查看字符串是否有数字时，我们将需要利用一些好的旧式正则表达式来完成这项工作。这将测试字符串中是否有数字，如果有，将返回 true。

```
setHasNumber(/\d/.test(password.firstPassword));
```

**特殊字符:**

非常类似于检查我们的密码，看看我们是否有一个号码，但只寻找这些具体的特殊字符。您可以看到如何将它定制为某些特殊字符。

```
setSpecialChar(/[ `!@#$%^&*()_+\-=\]{};':"\\|,.<>?~]/.test(password.firstPassword));
```

**密码匹配:**

最后，我们需要比较两个密码是否匹配！首先，在进行比较之前，我们需要确保我们的第一个密码确实存在。通过添加`!!`,我们强制一个布尔表达式。如果我们的第一个密码存在，并且我们的第一个密码等于我们的第二个密码。我们将评估它为真。

```
setMatch(!!password.firstPassword && password.firstPassword === password.secondPassword)
```

# 解决办法

哇，你成功了！感谢您跟随我使用 React 和 TypeScript 进行密码验证。

下面是最终代码的样子。

请随意复制并将其作为您自己的使用，并感谢您花时间阅读我的文章。我真的很喜欢为社区提供这些文章和指南。如果您有任何反馈，请在评论中提出。

如果你想看看我的其他指南和文章，看看我的媒体页面。

[](https://medium.com/@steven_creates) [## 史蒂文创造-中等

### 阅读史蒂文在媒体上创作的作品。具有 6 年以上实际设计经验的软件工程师…

medium.com](https://medium.com/@steven_creates) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)