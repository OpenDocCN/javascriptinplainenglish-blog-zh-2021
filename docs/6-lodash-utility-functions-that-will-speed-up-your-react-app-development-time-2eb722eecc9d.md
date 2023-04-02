# 6 个 Lodash 实用程序函数，可加快 React 应用程序的开发速度

> 原文：<https://javascript.plainenglish.io/6-lodash-utility-functions-that-will-speed-up-your-react-app-development-time-2eb722eecc9d?source=collection_archive---------6----------------------->

## 有具体的用例以及使用 Lodash 的例子。

![](img/ecc53668b6290bbe034280b0782d01f0.png)

Photo by [Nicolas Hoizey](https://unsplash.com/@nhoizey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先:**什么是 Lodash？**我会很简短，以防你已经知道了。

Lodash 是一个方便的[实用程序库](https://lodash.com/)。它提供了一些函数来轻松处理数据类型，如对象、数组、数字或字符串。在 Lodash 的帮助下，您可以在一行简单的代码中执行各种任务。您不必自己实现逻辑，也不必维护这些功能。

**但是，所有这些贴心的助手功能在现实世界中有哪些用例呢？**

这正是我想在这篇文章中回答的。我搜索了我参与的几个 React 项目，并提取了 Lodash 的常见用例。

# _.isEqual

这是迄今为止使用最多的函数。它比较两个值是否相同。同样，我不是指引用，而是指价值。

如文档中所述，支持许多数据类型:

> 该方法支持比较数组、数组缓冲区、布尔值、日期对象、错误对象、映射、数字、`Object`对象、正则表达式、集合、字符串、符号和类型化数组。

这个功能有大量的用例。您可以确定是否应该更新组件，或者是否应该进行昂贵的计算。

在提供的示例中，您可以看到 SearchInput 的基本实现。它呈现一个 TextField，并接受一个 searchValue 和一个 onChange 函数。

因为您希望确保 SearchInput 仅在 searchValue 已更改时调用 onChange 方法，所以检查事件值是否不同于 searchValue 属性是有意义的。如果是这样，就可以调用传递的 onChange 方法，例如，它可以用新的 searchValue 作为参数来触发 API 请求。如果不是这样，就没有必要触发 onChange 函数。

我知道你可能会说实现 TextField 组件的库应该确保它只在值改变时才改变。但是安全总比后悔好。

# _.去抖

去除函数的抖动可以极大地提高应用程序的性能。该实用程序的最佳用例是搜索字段。在这里，用户可以输入一个值，一些复杂的操作将会发生。例如 API 请求。如果没有去抖，每次击键都会调用这个函数，这会导致很多不必要的请求。

在上面的例子中，您可以看到 TextFields onChange 方法做了两件事。它更新文本字段本身的值，并执行 **callApi** 函数。该功能在每次击键时执行。但是多亏了 useCallback 钩子和 Lodash 的去抖动功能的帮助，只有在 400 毫秒内没有出现新的 **callApi** 调用时，这个函数才会被执行。

我还有一篇更详细的文章，是关于用一个自我实现的 useDebounce 钩子去抖动一个搜索字段，这个钩子去抖动值的变化。但是您也可以对函数调用本身进行去抖，以实现类似的行为。

[](https://bootcamp.uxdesign.cc/how-to-reduce-the-amount-of-expensive-operations-in-text-fields-e8f39a649487) [## 如何减少文本字段中昂贵的操作量

### React 组件去抖动值的实用程序

bootcamp.uxdesign.cc](https://bootcamp.uxdesign.cc/how-to-reduce-the-amount-of-expensive-operations-in-text-fields-e8f39a649487) 

# _.设置

使用 set 函数，您可以将对象的属性设置为新值。到目前为止，这听起来不是很特别，但是 set 函数会自动为您创建不存在的对象和数组，而不会抛出错误。

让我们来看看它的运行情况。如果我想给用户添加一个新的复杂属性，我可以这样做，如下所示。

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: true, read: true },
};
_.set(user, "articles[0].views", "over 9000");
```

有了这个，物体现在看起来像:

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: true, read: true },
  articles: [{ views: "over 9000" }],
};
```

如果您目前不确定属性 **articles** 是否已经存在，并且想要添加一些信息，这是一个不错的选择。

# _.得到

get 实用程序提供了从对象获取值的方法。它基本上是 set 函数的反过来，所以我认为它是不言自明的。

记住这个例子，下面将把超过 9000 的**返回。如果属性尚未定义，它将返回 undefined。**

```
_.get(user, "articles[0].views")
```

# _.isEmpty

isEmpty 函数检查传递的值是空对象还是空数组。听起来很简单，但在某些情况下，有一个快速的方法来检查这一点真的很有帮助。

在下面的示例中，您可以看到一个按钮，单击该按钮会将一个项目添加到列表中。基于这个列表的状态，应该呈现不同的布局。如果项目数组为空，应显示文本“无显示”，如果数组不为空，可生成不同的组件。

为了实现这种区分，我使用了 Lodashs isEmtpy 函数，如第 9 行所示。这是实现这种行为的一种简单易读的方法。

# _.克隆深度睡眠

这个函数深度克隆一个对象。这意味着创建了一个新的完整的新引用。让我们看看可以用这个功能做些什么。

假设我有一个用户对象，我想改变用户的一些属性。例如，名称和写权限已更改。但是我还想保留原始数据(也许以后会重置)，因此直接更改这些值是不可行的。所以我应该创建一个基于旧对象的新用户对象。

在下面的代码示例中，我用 spread 操作符(…)创建了一个 newUser 对象，之后，我更改了 newUser 的名称和权限。

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: true, read: true },
};
const newUser = { ...user };
newUser.firstname = "Not Joi";
newUser.mediumPermissions.write = false;
```

这将导致以下结果:

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: false, read: true },
};const newUser = {
  firstname: "Not Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: false, read: true },
};
```

如您所见，名字按预期更新。旧用户名为“Joi”，新用户名为“Not Joi”。但是，当我们看一看嵌套很深的介质权限的变化时，就出现了问题。旧用户和新用户都没有写权限，即使我们只想更新新用户的权限。

所以我们可以假设我们没有为深度嵌套的值创建新的引用。他们仍然指的是老用户。为了克服这个问题，可以使用 cloneDeep 函数。

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: true, read: true },
};
const newUser = _.cloneDeep(user);
newUser.firstname = "Not Joi";
newUser.mediumPermissions.write = false;
```

尝试完全相同的逻辑，但是用 Lodash 函数替换 spread 运算符，结果如下:

```
const user = {
  firstname: "Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: true, read: true },
};const user = {
  firstname: "Not Joi",
  lastname: "Schünemann",
  mediumPermissions: { write: false, read: true },
};
```

新老用户看起来完全符合预期。

# 结论

请随意使用提供的示例进行实验。但是请记住，使用实用程序库的函数并不总是有用或必要的。在使用大量 Lodash 函数来实现您的结果之前，请考虑您的用例的确切实现。如果您最终一个接一个地用多个 Lodash 函数操作数据，可能会有更简单的解决方案。

我希望你喜欢我最喜欢的 6 个 Lodash 函数和具体的用例。如果您有什么问题，或者您认为我错过了 Lodash 函数的一个很好的用例，请问我。

## 进一步阅读

[](https://bit.cloud/blog/sharing-javascript-utility-functions-across-projects-l557lr9k) [## 跨项目共享 JavaScript 实用函数

### 所以，你已经建立了这个令人敬畏的效用函数，并花了几个小时在上面。几个月后，你意识到你需要…

比特云](https://bit.cloud/blog/sharing-javascript-utility-functions-across-projects-l557lr9k) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***