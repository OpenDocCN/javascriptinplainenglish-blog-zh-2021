# 用例子解释 JavaScript 中的错误处理

> 原文：<https://javascript.plainenglish.io/error-handling-in-javascript-explained-with-examples-bab0868ed879?source=collection_archive---------11----------------------->

## 了解 JavaScript 中错误处理的基础知识。

![](img/69db51e0337d4386d8fb1016f18e071d.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名开发人员，错误是最令人讨厌的事情。这是编码过程的一部分，你会习惯的。在 JavaScript 中，当访问未定义的变量或函数时，很多时候你会遇到运行时错误。

幸运的是，JavaScript 提供了一种处理运行时错误的方法。语句`try`、`catch`、`throw`和`finally`就是一个很好的例子。例如，在处理异步操作以及处理来自其他资源的数据或用户输入时，您可以使用这些方法轻松处理错误。

在本文中，我们将学习 JavaScript 中错误处理的基础知识。所以让我们开始吧。

# try 和 catch 语句

JavaScript 中的语句`try`允许我们在代码块执行时检查其中的错误。

```
**try** {
  //Your code here.}
```

另一方面，语句`catch`允许您处理语句`try`中出现的错误。

这里有一个例子:

```
**try** {
  //Your code here.}**catch(*err*)** {
  //Code for handling the error.}
```

如您所见，`catch`接受了一个错误参数`err`。你可以给它取任何你想要的名字。它是一个对象，我们可以访问它来获得关于错误的信息。

对象`err`有一些有用的属性，我们可以使用点符号来访问这些属性以获得错误信息。

```
**try** {
  //Your code here.}**catch(*err*)** {
  console.log(**err.name**); //error name.
  console.log(**err.message**); //error message.
  console.log(**err.stack**); //Where the error occured
}
```

让我们看一个真实的例子，向您展示 JavaScript 中的错误处理是如何工作的:

在下面的例子中，我们将调用一个我们还没有定义的函数`getData()`来引起一个错误。因此，我们将使用语句`try`和`catch`来检查和处理该错误。

下面是一个例子:

```
**try**{
    console.log('Hello World');
   ** getData()**; //Calling a function that we haven't defined.
}
**catch(err)**{
    console.log(`${**err.name**}: ${**err.message**}`)
}//output:
Hello World
ReferenceError: getData is not defined
```

如你所见，语句`try`发现了一个错误(调用一个未定义的函数`getData()`)。当错误发生在 try 语句中时，它会自动在 catch 语句中得到处理。如果没有错误，catch 语句中不会发生任何事情。

在上面的例子中，我们使用了语句`catch`来捕获错误，并在控制台中输出其名称和消息。

# throw 和 finally 语句

语句`throw`允许您创建自定义错误。您可以随时使用它来抛出错误。

这里有一个例子:

```
**throw new SyntaxError**("syntax error has occured");//or:
**throw Error**("error has occured");//or:
**throw** "this is a custom error"
```

另一方面，不管有没有错误，语句`finally`都允许您运行代码。无论 try 和 catch 语句的结果如何，您放在语句`finally`中的代码都将一直运行。

让我们来看一个简单的例子，将`try`、`catch`、`throw`和`finally`一起使用:

下面的例子将检查一个名为`user`的对象是否有一个 truthy name 值。如果没有，我们将使用语句`throw`创建一个错误对象。我们将在 catch 语句中处理和访问错误对象。

```
let user = {
    name: "",
    age: 19
}**try**{
   if(!user.name){
      **throw new ReferenceError**("The user doesn't have a name property");
    }
}**catch(err)**{
    console.log("No name: " + **err.message**);
}**finally**{
    console.log("This will always run.");
}//output:
No name: The user doesn't have a name property
This will always run.
```

如您所见，通过使用 catch 语句，我们访问并打印了使用`throw`语句创建的错误。

您还应该记住，这些语句只适用于运行时错误(可以执行的代码)。如果代码语法错误，它们就不会工作。

# 承诺和异步/等待

大多数时候，您会希望将`try`和`catch`与承诺和 async/await 混合起来进行错误处理。

这里有一个例子:

```
const ourPromise = **new Promise**((resolve, reject)=>{
    setTimeout(()=> reject("This is an error"), 2000)
});const testPromise = **async** ()=>{
    **try**{
        let data = **await** ourPromise;
    }**catch(err**){
        console.error(err); 
    }
}
```

在上面的例子中，当承诺被拒绝时，错误被捕获并显示在控制台中。try 语句检查承诺是否被拒绝。如果是这样，catch 语句将捕获错误。

# 结论

错误处理在 JavaScript 中非常重要。所以，如果你想更好地处理错误，你需要练习所有这些语句。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/how-to-customize-your-vscode-for-front-end-web-development-b80c8eb562d1) [## 如何为前端 Web 开发定制 VSCode

### 定制您的 VSCode，使其更好地为您服务。

javascript.plainenglish.io](/how-to-customize-your-vscode-for-front-end-web-development-b80c8eb562d1) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)