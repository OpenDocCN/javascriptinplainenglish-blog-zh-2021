# 添加验证以反应挂钩形式

> 原文：<https://javascript.plainenglish.io/adding-validations-to-react-hook-form-647da6bcc650?source=collection_archive---------15----------------------->

## 如何添加验证以反应钩子形式

![](img/92e81a1ea582f02260ff261df02b3909.png)

Photo by [Esther Jiao](https://unsplash.com/@estherrj?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好，最近我经常使用 React Hook Form 来管理我的表单状态。虽然它非常有用，但我听到的一个问题是— *“我如何在那里验证东西？”*

在这篇博文中，我将通过使用 Yup 向您展示如何向使用 React Hook Form 创建的表单添加验证。

# 验证我们的表单

这里我们有一个非常简单的表单，其中一个不受控制的输入组件被一个控制器包装起来，并通过名称 prop 分配给`username`值。由于 defaultValues 被传递给了`useForm`钩子，这个表单应该显示`danieljcafonso`作为输入的预填充值。

首先，我们需要安装`@hookforms/resolvers`来集成外部验证库，比如 yup、zod、joi、superstruct、vest 等等。

```
npm install @hookforms/resolvers
```

然后，我们安装我们的验证库，在这种情况下，我将使用 Yup。

```
npm install yup
```

现在我们已经安装了 Yup，我们可以使用它来创建我们的模式。在这个场景中，我们将创建一个对象，其中包含一个作为必需字符串的用户名。

在我们有了模式之后，我们需要将它传递给 React Hook Form `useForm` hook。为此，我们将它包装成 yupResolver 函数作为解析器进行传递。此外，我们可以定义我们的验证模式。

这是这些变化的最终结果。

# 验证字段数组

当处理可能有多个值的字段时，字段数组非常有用。虽然这非常有用，但我过去一直在努力验证这一点。

首先，让我们从向 defaultValues 添加一个用户数组开始

然后，在我们的组件中，让我们使用`useFieldArray`来提取表单当前值的用户数组的值。

然后，让我们使用这些字段向 DOM 添加一个新的输入来表示值。确保该名称包含相关用户的位置，以便正确绑定这些值。

现在，更改我们的模式以添加用户字段，并将其表示为一个对象数组，其中每个对象都有一个 firstName 和 lastName 必需的字符串。

之后，一切都应该正常工作，这里是我们的代码的完整版本。

# 包扎

如你所见，向 React Hook Form 添加验证非常简单，在我看来，大部分挑战来自于处理你选择使用的验证库。这里有一个到 codesandbox 的[链接，你可以在这里试用这段代码。](https://codesandbox.io/s/summer-butterfly-yhn6r)

我希望这篇博文对你有用。

敬请关注，下次再见！

*最初发表于*[*【https://www.danieljcafonso.com】*](https://www.danieljcafonso.com/add_validations_to_rhf)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)