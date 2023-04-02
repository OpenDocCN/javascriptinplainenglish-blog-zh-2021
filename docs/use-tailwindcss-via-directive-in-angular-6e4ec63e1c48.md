# 通过 Angular 中的指令使用 TailwindCSS

> 原文：<https://javascript.plainenglish.io/use-tailwindcss-via-directive-in-angular-6e4ec63e1c48?source=collection_archive---------6----------------------->

## 从角度模板中整理顺风类，并在应用程序中重用样式。

![](img/0092bd9848e46ad983ea20d0fd9fe4f3.png)

Photo by [Pascal Meier](https://unsplash.com/@zhpix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral). **Fun fact: Tailwind is a term heavily used in** [**Aviation**](https://en.wikipedia.org/wiki/Headwind_and_tailwind)**.**

从 v11.2 开始，Angular 对 TailwindCSS 提供了一流的支持。当在 angular 模板中使用 tailwind 时，您可能希望对一些类进行分组以便重用。例如，对于卡片样式，您可能有`bg-gray-100 rounded-md p-4 shadow hover:shadow-lg hover:bg-gray-50`。当然，你有 tailwind 的 [@apply 指令](https://tailwindcss.com/docs/functions-and-directives#apply)来创建你自己的定制类，由 tailwind 类组成。但是我将向你展示一种非常规的分组方式，并在 angular 模板中使用它们。

# 样式映射

让我们首先创建一个风格词典。键名将用于匹配和提取 tailwind 类，并将它们应用于 HTML 元素。下面给出一个例子:

Styles Map

# 该指令

创建一个名为`tailwind`的指令，并使其全局可用，例如，通过在您的`AppModule`中声明，或者如果您有一个`CoreModule`作为单例/可重用内容的全局容器模块。

Tailwind directive

发生了什么事？我们将接收一个字符串作为指令的输入。注意我们使用了选择器名称和输入两者`tailwind`。相同的选择器和输入名称允许您用一个声明附加和获取输入。

我们需要对输入进行一些处理。我们没有使用`OnChanges`生命周期挂钩，而是使用了另一种带有 getter & setter 的模式。与实现内部的`ngOnChanges`方法相比，这更干净，并且只在输入改变时运行。

指令可以访问主机，即指令应用的位置。我们使用`@HostBinding(’class’)` decorator 将类属性附加到主机上。

在 setter 中，我们获取输入字符串并-

1.  用空格分割字符串。然后我们有一个字符串元素的数组。
2.  对于每个字符串元素，查看我们是否在**样式映射**中有匹配。如果是，那么返回映射的更大的字符串(tailwind 类)。否则，返回字符串本身。因此，如果字符串元素是`layoutCenter`，那么我们得到`flex items-center justify-center`，如果是`bla`，那么我们得到`bla`。
3.  我们将所有解析后的字符串再次用空格分隔连接起来。

# 使用

我们的诡计得逞了！是时候在模板中使用它了。你像这样使用它:

Usage of Tailwind Directive

现在你甚至可以通过`tailwind="someclass"`指令直接应用 tailwind 类，而不是 HTML 类属性(`class="someclass"`)；我不是警察！可能性无穷:)

# 利弊

1.  对顺风类进行分组并在应用范围内使用要容易得多。你不需要为每个元素做单独的指令/包装组件，比如`button`、`card`，只是为了在你的应用中应用一些样式类。
2.  如果有许多样式，应用程序必须将一个大的 typescript 对象加载到内存中。没什么大不了的，但还是要记在心里。
3.  定制类的顺序很重要。最右边的自定义类包含的顺风类将覆盖左边的自定义类。这就是为什么`button buttonSecondary`会按预期工作，而`buttonSecondary button`不会。

分享你的想法和/或建议作为回应。感谢阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io)