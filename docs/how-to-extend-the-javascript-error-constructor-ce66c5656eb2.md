# 如何扩展 JavaScript 错误构造函数？

> 原文：<https://javascript.plainenglish.io/how-to-extend-the-javascript-error-constructor-ce66c5656eb2?source=collection_archive---------17----------------------->

![](img/de0baa471c391aed78e90b2b0322d1ad.png)

Photo by [Ivan Bandura](https://unsplash.com/@unstable_affliction?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了在我们的 JavaScript 应用程序中抛出错误，我们通常通过一个对象，它是`Error`构造函数的实例。

在本文中，我们将看看如何用我们自己的构造函数扩展 JavaScript `Error`构造函数。

# 创建我们自己的构造函数

扩展内置`Error`构造函数的一种方法是创建我们自己的构造函数，从`Error`构造函数获取数据。

例如，我们可以写:

```
function MyError(message) {
  this.name = 'MyError';
  this.message = message;
  this.stack = (new Error()).stack;
}
MyError.prototype = new Error();
throw new MyError('error occurred')
```

我们创建了接受`message`参数的`MyError`构造函数。

我们将`message`设置为`message`属性的值。

我们从`Error`实例的`stack`属性中获得堆栈跟踪。

我们将`MyError.prototype`设置为新的`Error`实例，这样`MyError`实例也是`Error`实例。

在构造函数中，我们设置了`name`,当一个错误被抛出时，它将被记录。

然后我们抛出一个带有关键字`throw`的`MyError`实例。

一旦抛出错误，我们应该在日志中看到它。

如果我们记录 `myError instanceof Error` 和`myError instanceof MyError`，我们应该会看到两者都是`true`，因为我们将`MyError.prototype`设置为一个新的`Error`实例。

# 使用 Class 语法和 extends 关键字扩展错误构造函数

ES6 中增加了 class 语法，这样我们就可以轻松地创建继承构造函数的构造函数。

然而，在语法糖的下面，原型继承仍然像我们在前面的例子中一样被使用。

为了扩展`Error`构造函数，我们编写:

```
class MyError extends Error {
  constructor(message) {
    super(message);
    this.name = 'MyError';
  }
}const myError = new MyError('error occurred')
console.log(myError instanceof Error)
console.log(myError instanceof MyError)
throw myError
```

我们用关键字`extends`创建了`MyError`类，从而创建了`Error`类的子类。

`constructor`接受`message`参数，我们通过调用`super`将其传递给`Error`构造函数。

我们还在构造函数中设置了自己的`name`属性。

然后我们用和以前一样的方法实例化`MyError`类。

如果我们在`Error`和`MyError`上使用`instanceof`操作符，我们会看到它们都是`true`。

当我们抛出一个错误时，我们看到的消息和以前一样。

# 结论

我们可以使用常规的原型继承或类语法来创建我们自己的构造函数，它从`Error`构造函数继承数据。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)