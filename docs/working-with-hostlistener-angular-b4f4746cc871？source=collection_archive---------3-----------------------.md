# 如何在 Angular 中使用@hostListener

> 原文：<https://javascript.plainenglish.io/working-with-hostlistener-angular-b4f4746cc871?source=collection_archive---------3----------------------->

## 使用 Angular 中的@hostListener 实现更多功能

在这篇文章中，我们将讨论 Angular 中的 **@hostListener 装饰器，并寻找由 **@hostListener** 提供的特性。这是一种跟踪用户事件并对这些事件做出响应的简单方法。**

![](img/172e99fca1fa8f9149b047ac95da1990.png)

@hostListener in Angular for Event Handling

# Angular 中的@hostListener 是什么？

*   它是一个**装饰器，指定要捕获的 DOM 事件**
*   **指定需要在事件调用中调用**的事件处理程序****
*   **@hostListener 接收事件名称**和相关的回调函数
*   **@hostListner 可以捕获用户触发的事件信息**

# 如何在角度组件中使用@hostListener？

**@hostListener** 也可以在组件内部使用**。这个装饰器可以添加到组件中，以添加需要捕获的事件。**

[https://gist.github.com/Mayankgupta688/d351adf1978df20c2c5fe1aa77e2e0a2](https://gist.github.com/Mayankgupta688/d351adf1978df20c2c5fe1aa77e2e0a2)

在上面的例子中，我们使用 **@hostListener** 在组件中附加了“click”事件。只要有人点击组件，附属于 **@hostListener 的函数就会被调用**。用户在组件中可以有多个@ **hostListener** 。下面给出了一个工作示例:

How to use @hostListener in Angular Component ?

# 用@hostListener 捕获窗口事件

还可以使用@hostListener 来捕获组件外部发生的事件。在下面的例子中，我们需要跟踪在“窗口”元素中调用的事件。为了捕获窗口事件，我们附加了**@ host listener(" window:click ")**，它指定需要处理“窗口”内的任何点击。

[https://gist.github.com/Mayankgupta688/d351adf1978df20c2c5fe1aa77e2e0a2](https://gist.github.com/Mayankgupta688/d351adf1978df20c2c5fe1aa77e2e0a2)

Capturing Window Events with @hostListener

# 我们如何在 Angular 中使用@hostListener？

创建自定义指令时，也可以使用@hostListener 。当我们创建自定义指令时，我们可以添加@hostListener 来附加对某些事件的行为，这些事件可以由应用该指令的组件引发。

How do we use @hostListener in Angular?

在上面的代码中，我们可以看到我们将一个@hostListener 附加到创建的自定义指令上。我们已经应用@hostListener 来捕获组件可以触发的“onclick”事件。

在上面的代码中，创建的指令被附加到一个“div”上。指令定义的功能将应用于组件。我们在“div”组件上附加了“click”处理，所以如果任何人访问“div”组件并“单击”它，就会调用与@hostListener 关联的代码。

How do we use @hostListener in Angular?

# 在@hostListener 中捕获事件

当一个事件被引发时，它会生成一个“事件”对象，我们可以在@hostListener 中捕获这个“事件”对象，并可以使用这个事件对象来修改目标元素或获取关于被触发事件的更多信息。

[https://gist.github.com/Mayankgupta688/66fc4f356611cc940bea9c65b9b15048](https://gist.github.com/Mayankgupta688/66fc4f356611cc940bea9c65b9b15048)

在上面的代码中，我们通过向@hostListener decorator 提供一个额外的参数来捕获“事件”细节。它捕获事件，并使该事件可用于与回调关联的函数。

Capturing Events in @hostListener

# 关闭:

如有疑问和顾虑，请对故事进行评论。我们会尽快回复您。

*更多内容看*[***plain English . io***](http://plainenglish.io/)