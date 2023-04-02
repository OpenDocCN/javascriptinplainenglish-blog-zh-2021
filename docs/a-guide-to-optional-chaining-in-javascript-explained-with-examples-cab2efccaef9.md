# 可选链接指南？.'用 JavaScript——用例子解释

> 原文：<https://javascript.plainenglish.io/a-guide-to-optional-chaining-in-javascript-explained-with-examples-cab2efccaef9?source=collection_archive---------13----------------------->

![](img/f94f1152be24a0ff6523692f400d7d72.png)

JavaScript 中的可选链接`?.`是访问嵌套对象属性的安全方式，即使中间属性不存在。

# “不存在的财产”问题

如果你刚开始看教程，学 JavaScript，可能问题还没接触到你，但是挺普遍的。

举个例子，假设我们有保存用户信息的`user`对象。

我们的大多数用户都有在`user.address`房产、街道`user.address.street`的地址，但有些人没有提供。

在这种情况下，当我们试图获取`user.address.street`，而用户碰巧没有地址时，我们会得到一个错误:

```
let user = {}; // a user without "address" propertyalert(user.address.street); // Error!
```

这就是预期的结果。JavaScript 是这样工作的。由于`user.address`是`undefined`，尝试获取`user.address.street`失败并出错。

在许多实际情况下，我们更希望得到`undefined`而不是这里的错误(意思是“没有街道”)。

…还有另一个例子。在 web 开发中，我们可以使用一个特殊的方法调用，比如`document.querySelector('.elem')`，得到一个对应于 web 页面元素的对象，当没有这样的元素时，它返回`null`。

```
// document.querySelector('.elem') is null if there's no element
let html = document.querySelector('.elem').innerHTML; // error if it's null
```

同样，如果元素不存在，我们将在访问`null`的`.innerHTML`时出错。在某些情况下，缺少元素是正常的，我们希望避免错误，只接受`html = null`作为结果。

我们如何做到这一点？

显而易见的解决方案是在访问其属性之前，使用`if`或条件运算符`?`检查值，如下所示:

```
let user = {};alert(user.address ? user.address.street : undefined);
```

它工作，没有错误…但它相当不雅。如您所见，`"user.address"`在代码中出现了两次。对于嵌套更深的属性，由于需要更多的重复，这就成了一个问题。

例如:让我们试试`user.address.street.name`。

我们需要检查`user.address`和`user.address.street`:

```
let user = {}; // user has no addressalert(user.address ? user.address.street ? user.address.street.name : null : null);
```

这太可怕了，人们甚至可能难以理解这样的代码。

不要在意，因为有更好的方式来编写它，使用`&&`操作符:

```
let user = {}; // user has no addressalert( user.address && user.address.street && user.address.street.name ); // undefined (no error)
```

使用属性的完整路径可以确保所有组件都存在(如果不存在，求值将会停止)，但这并不理想。

如您所见，属性名在代码中仍然是重复的。例如，在上面的代码中，`user.address`出现了三次。

这就是为什么可选的链接`?.`被添加到语言中。来一劳永逸的解决这个问题！

# 可选链接

如果`?.`之前的值为`undefined`或`null`，可选链接`?.`停止评估，并返回`undefined`。

**在本文中，为了简洁起见，我们将说某个东西“存在”，如果它不是** `**null**` **而不是** `**undefined**` **。**

换句话说，`value?.prop`:

*   作为`value.prop`工作，如果`value`存在，
*   否则(当`value`为`undefined/null`时)返回`undefined`。

以下是使用`?.`访问`user.address.street`的安全方法:

```
let user = {}; // user has no addressalert( user?.address?.street ); // undefined (no error)
```

代码简洁明了，没有任何重复。

即使`user`对象不存在，用`user?.address`读取地址也有效:

```
let user = null;alert( user?.address ); // undefined
alert( user?.address.street ); // undefined
```

请注意:`?.`语法使它前面的值成为可选的，但不再是可选的。

例如在`user?.address.street.name`中，`?.`允许`user`安全地为`null/undefined`(并在那种情况下返回`undefined`)，但那只是针对`user`。以常规方式访问更多的属性。如果我们希望其中一些是可选的，那么我们需要用`?.`替换更多的`.`。

# 短路

如前所述，如果左侧部分不存在，`?.`会立即停止(“短路”)评估。

因此，如果有任何进一步的函数调用或副作用，它们不会发生。

例如:

```
let user = null;
let x = 0;user?.sayHi(x++); // no "sayHi", so the execution doesn't reach x++alert(x); // 0, value not incremented
```

# 其他变体:？。(), ?。[]

可选链接`?.`不是一个操作符，而是一个特殊的语法结构，它也适用于函数和方括号。

例如，`?.()`用来调用一个可能不存在的函数。

在下面的代码中，我们的一些用户有`admin`方法，而一些没有:

```
let userAdmin = {
  admin() {
    alert("I am admin");
  }
};let userGuest = {};userAdmin.admin?.(); // I am adminuserGuest.admin?.(); // nothing (no such method)
```

这里，在这两行中，我们首先使用点(`userAdmin.admin`)来获取`admin`属性，因为我们假设用户对象存在，所以读取它是安全的。

然后`?.()`检查左边部分:如果管理功能存在，那么它就运行(对`userAdmin`来说也是如此)。否则(对于`userGuest`)，评估会无错误地停止。

如果我们想使用括号`[]`而不是点`.`来访问属性，那么`?.[]`语法也是有效的。与前面的情况类似，它允许从可能不存在的对象中安全地读取属性。

```
let key = "firstName";let user1 = {
  firstName: "John"
};let user2 = null;alert( user1?.[key] ); // John
alert( user2?.[key] ); // undefined
```

同样，我们可以将`?.`与`delete`一起使用:

```
delete user?.name; // delete user.name if user exists
```

# 摘要

可选链接`?.`语法有三种形式:

1.  `obj?.prop`–如果`obj`存在，则返回`obj.prop`，否则返回`undefined`。
2.  `obj?.[prop]`–如果`obj`存在，则返回`obj[prop]`，否则返回`undefined`。
3.  `obj.method?.()`–如果`obj.method`存在，则调用`obj.method()`，否则返回`undefined`。

正如我们所看到的，它们都简单明了，易于使用。`?.`检查`null/undefined`的左侧部分，如果不是，则允许评估继续进行。

一系列的`?.`允许你安全地访问嵌套的属性。

尽管如此，我们应该小心地应用`?.`,只有在左边部分不存在是可以接受的情况下，这样如果出现编程错误，它不会对我们隐藏。

希望你喜欢这篇文章。

## 表现出一些爱

地址:**0x 27180 EB 5f 52 D2 AAAA 5d 268 a1 b5 c 910 FD 9 DFC 7 df 4**

*更多内容请看*[***plain English . io***](http://plainenglish.io/)