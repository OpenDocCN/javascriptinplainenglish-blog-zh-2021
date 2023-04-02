# 如何在 Angular 的组件和指令中获取属性值

> 原文：<https://javascript.plainenglish.io/how-to-get-an-attribute-value-in-angulars-components-and-directives-adf77a5da939?source=collection_archive---------6----------------------->

在本教程中，我们将探索读取组件或指令中传递的 HTML 属性值的所有方法。

![](img/2c0fd51656d5ee37d053bad3e2074c8e.png)

# 读取 HTML 属性

*HTML 中的元素有* ***属性****；这些是附加的值，它们以各种方式配置元素或调整它们的行为，以满足用户想要的标准。—* [*MDN 文档*](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)

例如:

`type`和`colspan`是 HTML 属性的一些例子。

在某些情况下，您需要根据为 HTML 属性设置的值来处理组件或指令的行为。

例如，有一个组件叫做`smart-input`。您希望为作为值传递给 HTML 属性的不同的`type`呈现不同的布局。

# `ElementRef`阶级

读取这些属性值的一种方法是通过`[ElementRef](https://angular.io/api/core/ElementRef)`:

以上是好的，并按预期工作。但是，有一个更短的方法可用于上述角度。

# `@Attribute()`参数装饰器

可以使用参数 decorator 通过依赖注入将 HTML 属性的值传递给组件或指令构造函数。

因此，对于前面的例子，为了读取`type`属性，我们将做如下所示的事情:

有了上面的代码，`smart-input`就会呈现

`@Attribute()` decorator 也可以用在制作`[FactoryProvider](https://angular.io/api/core/FactoryProvider)`的时候。

所以，对于`smart-input`，我们也可以编写如下代码:

这个装饰器也被一些内置指令使用:

以下是使用`@Attribute()`装饰器的两个限制:

1.  它只适用于静态 HTML 属性值。不支持[属性绑定](https://angular.io/guide/attribute-binding#binding-to-an-attribute)和[属性绑定](https://angular.io/guide/property-binding)。
2.  由于它仅适用于静态值，因此仅支持`string`类型。

为了克服上述限制，我们可以使用`@Input()`装饰器。

# `@Input()`物业装修工

是一个属性装饰器，用在子组件或指令中，表示属性可以从父组件接收它的值。

所以，对于上面的例子，我们可以重写如下:

以上工作正常。与`@Attribute()`不同，它支持所有数据类型，如果您使用[属性绑定](https://angular.io/guide/property-binding)或[文本插值](https://angular.io/guide/interpolation#text-interpolation)，它还会跟踪值的变化。

还要注意，`@Input()`支持静态和动态两种绑定。

许多内置指令也使用这个装饰器。下面是几个例子:

使用`@Input()` decorator 的唯一限制是，它的值只有在组件或指令初始化后才可用，即在生命周期钩子中。

我们学习了三种读取`smart-input`组件的`type`值的方法，以及如何在一些内置指令和限制中使用它们。让我们再来看看主要的区别:

**可用性**

1.  `ElementRef`和`@Attribute()`通过依赖注入使属性的值在`constructor`中可用
2.  `@Input()`使值在组件/指令初始化后可用，即在`ngOnInit`生命周期挂钩中。

**型支架**

1.  `ElementRef`和`@Attribute()`仅支持`string`
2.  `@Input()`支持所有类型

**值更新**

1.  `ElementRef`和`@Attribute()`不跟踪值更新
2.  `@Input()`如果使用了属性绑定或文本插值，则跟踪值更新

**一般用法**

1.  由于`ElementRef`和`@Attribute()`只支持`string`类型，它们通常用于读取静态 HTML 属性的值
2.  由于`@Input()`支持所有类型，并且它还跟踪更新，所以它通常用于读取传递给组件/指令的 DOM 属性或自定义数据

# 结论

我们学习了如何使用`ElementRef`类、`@Attribute()`和`@Input()`装饰器读取组件或指令中的 HTML 属性值。我们还学习了它们的用法，如何在一些内置指令和限制中使用它们。

我已经为上面的所有代码创建了一个 [stackblitz](https://stackblitz.com/edit/angular-ivy-8cyazj?file=src/app/app.component.ts) 。

*原发布于* [https://indepth.dev](https://indepth.dev/tutorials/angular/get-attribute-value) 。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)