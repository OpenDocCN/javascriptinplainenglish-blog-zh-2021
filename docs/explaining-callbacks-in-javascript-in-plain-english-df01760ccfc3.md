# 用简单的英语解释 JavaScript 回调

> 原文：<https://javascript.plainenglish.io/explaining-callbacks-in-javascript-in-plain-english-df01760ccfc3?source=collection_archive---------18----------------------->

![](img/522f79d2101166c92dc826ce103e48aa.png)

Creator: Grafner | Credit: Getty Images/iStockphoto | Copyright: Grafner

JavaScript 中的回调函数是*一个在另一个函数执行完毕后被调用的函数。*

由于 JavaScript 使用事件驱动的编程模型，所以它不会等待一个函数完成执行，而是立即转移到下一个函数。回调使您可以将一个函数设置为仅在另一个函数完成执行后才执行。

JavaScript 中的函数是*一级对象*，这意味着它们可以被赋给变量，作为函数参数传递，或者可以被赋为另一个函数的返回值。任何作为参数传递给另一个函数并在外部函数中调用的函数都是回调函数。让我们看看下面的例子:

```
const hi = () => console.log('Hi');
const bye = () => console.log('Bye');hi();
bye();
```

在这种情况下，将首先执行功能`*hi*` ，然后执行功能`*bye*` 。控制台中记录的结果将是，

```
//Hi
//Bye
```

但是如果我们的函数在做一些复杂的事情呢？让我们假设这个函数正在从服务器获取数据。根据具体情况，服务器可能需要一些时间来处理这个请求。

为了更好地说明这个例子，我们可以使用`*setTimeout*` 函数，它在指定的时间后执行一段代码。我们将把函数的执行延迟 1 秒，就像它是一个获取请求一样。让我们看看我们的代码，

```
function hi() { // Imagine function hi is fetching data from the server here setTimeout(function() { console.log('Hi'); }, 1000);}function bye() { console.log('Bye');
} hi();bye();
```

现在我们已经将函数`*hi*` 的执行延迟了 1000 毫秒(1 秒)，我们在控制台中的结果是

```
//Bye
//Hi
```

在等待过程中,`Bye()`被执行。这就是为什么 Bye 印在 Hi 之前。JavaScript 不会破坏函数调用的顺序，它只是不等待函数`*hi*` 的响应，而是立即移动到下一个函数。

这里最重要的一点是*异步函数不会互相等待*。您无法预测哪个函数将花费最短的时间来执行。再一次， ***回调使得设置一个函数仅在另一个函数执行完*后执行成为可能。**

# 如何创建回调

可以使用`*callback*` 关键字作为最后一个参数来创建自定义回调函数。然后可以在函数结束时调用。如果我们想确定我们正在传递一个函数作为参数，我们可以使用`***typeof.***`

让我们打开一个控制台，写下:

```
const watchingNetflix = (movie) => console.log(`Watching ${movie}.`);
```

我们的函数接受一个参数。您可以通过在控制台中键入以下命令来调用它:

```
watchingNetflix('Friends'); // Watching Friends.
```

现在让我们给函数添加一个回调。

```
const watchingNetflix = (movie, callback) => {  
  console.log(`Watching ${movie}`)       if (typeof callback === 'function');       callback();
};watchingNetflix('Friends', () => console.log('Watched all the seasons'));
```

如果你在控制台中输入这个代码，你会得到两条消息，第一条消息是“观看朋友”，第二条消息是“观看了所有季节”。

```
// Watching Friends// Watched all the seasons
```

`*WatchingNetflix*` 函数先记录“看朋友”然后检查我们回调函数的类型，由于回调是一个函数，它得到执行并记录“看了所有季节”。

上面的例子非常简单，我用它们来演示回调语法。回调函数在异步编程中变得非常方便，在异步编程中，一个函数必须等待另一个函数完成执行(例如，像等待文件加载)。

## 概括一下

*   回调是作为参数传递给另一个函数的函数。
*   这种技术允许一个函数调用另一个函数。
*   回调函数可以在另一个函数完成后运行。