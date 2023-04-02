# 如何检测浏览器标签的关闭

> 原文：<https://javascript.plainenglish.io/how-to-detect-the-closing-of-a-browser-tab-94eee00a4e39?source=collection_archive---------0----------------------->

![](img/bf13195537a509f8cbb2a837c8158fb2.png)

Photo by [Remotar Jobs](https://unsplash.com/@remotarjobs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/browser?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

有时候，你需要在用户关闭标签页之前做一些事情。它可能是清除 cookies 或发送 API 调用。

然而，在 JavaScript/TypeScript 中，没有直接/标准的方法来识别用户是否关闭了标签和/或浏览器窗口。我惊讶地发现没有直接的方法可以做到这一点。在本文中，您将学习一种有效检测页面重新加载、标签关闭和浏览器关闭动作的方法，并区分它们。

*下面我将展示的例子是使用角度 10。如果您使用另一个框架或 JavaScript，语法会有所不同，但理论是相同的。*

# 卸载前

JavaScript 提供了一个名为 beforeunload 的事件处理程序。每当从客户端删除/卸载资源时，都会调用此事件。

这意味着每当用户重新加载页面、关闭选项卡或浏览器窗口时，都会触发此事件。如果你正在寻找的正是这一点，这就足够了。然而，对于大多数应用程序，我们需要区分“关闭”(标签或窗口)和“重新加载”。让我们看看我们能做些什么。

```
// Angular Example for beforeunload event handler
@HostListener('window:beforeunload', ['$event'])
beforeunloadHandler(event): void {
  // Do something
}
```

# 1)识别页面重载

到目前为止，我们知道页面重载也会触发 beforeunload 事件。当事件被触发时，我们不知道是什么触发了它(重新加载、标签关闭或浏览器关闭)。在该事件处理程序中，我们需要确定页面是否被重新加载。

可以使用 NavigationTiming API 识别页面重新加载。你可以在这里阅读关于[的所有内容。](https://www.w3.org/TR/navigation-timing/)

请注意，window.performance.navigation 已被弃用，因此您应该避免使用它。请改用 NavigationTiming API 提供的属性。

根据 NavigationTiming 的文档，我们需要在导航条目类型数组中查找导航类型“reload”。为了简单起见，我们将避免使用循环。让我们编码

```
let pageReloaded = window.performance
                 .getEntriesByType('navigation')
                 .map((nav) => (nav as any).type)
                 .includes('reload');
```

就像那样，现在 pageReloaded 携带了页面是否重载的布尔值。您可能希望将它放在 beforeunload 事件处理程序中。

**注:** *我们没有使用循环的原因有很多。我在这篇* [*文章*](/why-you-should-stop-using-loops-88a6a789106e) *中详细阐述了为什么不应该使用循环。如果您使用的是 JavaScript 而不是 TypeScript，唯一的变化就是在 map 中使用 arrow 函数。*

# **2)检测标签关闭**

与页面重新加载不同，没有标准的方法来检测选项卡是否关闭。然而，我们可以利用本地存储来实现这一点。

浏览器中的本地存储由同一个域共享。这意味着你可以在浏览器中打开多个标签，比如说从[www.google.com](http://www.google.com)开始，它们都共享同一个本地存储。

这个想法很简单，我们可以为一个特定的域计算浏览器中打开的标签总数。在 1 处实例化，它将在每次打开新选项卡(实例化新页面)时增加 1，在选项卡关闭时减少 1(使用 beforeunload 事件处理程序)。

**注意:** *对于选项卡关闭，我们需要确保在页面重新加载时不会减少选项卡计数。我们已经在第 1 点中看到了如何检测页面重载。*

让我们看一下代码

**2.1)增加标签数**

```
ngOnInit() {
  // We need to parse into integer since local storage can only
  // store strings.
  let tabCount = parseInt(localStorage.getItem("windowCount")); // Then we instantiate tabCount if it doesn't already exist
  // OR Increment by 1 if it already exists
  tabCount = Number.isNaN(tabCount) ? 1 : ++tabCount;

  // Set the count on local storage
  localStorage.setItem('tabCount', tabCount.toString());
}
```

**2.2)减少标签计数**

```
@HostListener('window:beforeunload', ['$event'])
beforeunloadHandler(event): void {
  if(!pageReloaded) { // The pageReloaded boolean we set earlier
    let tabCount = parseInt(localStorage.getItem('tabCount'));
    --tabCount;
    localStorage.setItem('tabCount', tabCount.toString());
  }
}
```

就像这样，我们现在可以知道标签何时关闭。每次我们的标签数减少 1，标签就会被关闭。你现在可以做任何你想做的事情。

还有一种方法可以在浏览器中获取所有打开的标签页。使用 [window.getAll()](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/windows/getAll) 我们可以实现完全一样的东西，甚至更多。但是，最新的 Firefox 和 Safari 版本不支持它。它还需要用户的许可。就我们的目的而言，使用本地存储方法更合适(因为 window.getAll()是异步的),并且它使事情变得简单。

现在让我们更进一步。我们现在将检测它是浏览器关闭还是标签关闭。

**注意:** *如果你想要的只是检测一个标签页或者浏览器是否被关闭，并且不区分它们，你甚至不需要保存一个标签页计数。如果您点击 beforeunload 事件处理程序并且 pageReloaded 布尔值为 false，则确认选项卡或窗口已关闭。*

# **3)检测到浏览器关闭**

要理解浏览器关闭，我们需要先了解浏览器是如何关闭的。

当用户关闭浏览器窗口时，浏览器中的每个标签都会被一个接一个地关闭(根据我的实验，Chrome 在轻负载到平均负载时的延迟大约为 1 毫秒)。

现在，我们知道浏览器关闭将触发 beforeunload 事件处理程序。由于每个标签页会一个接一个地关闭，我们可以试着捕捉两个连续标签页关闭之间的延迟。**如果关闭延迟是一分钟(1 毫秒-50 毫秒)，那就是我们浏览器正在关闭的信号。**

```
isBrowserClosed() {
  var localStorageTime = parseInt(localStorage.getItem('storageTime'));
  var currentTime = new Date().getTime();
  var timeDifference = currentTime - localStorageTime; if (timeDifference < 50) {
    //Browser is being closed
    // Do something before browser closes.
  }
}
```

**注意:** *为了准确检测浏览器关闭，如果当前时间和 onbeforeunload 上的存储时间相差太大，我们需要更新 storageTime。下面的代码就是一个例子。*

```
@HostListener('window:beforeunload', ['$event'])
beforeunloadHandler(event): void {
  if(!pageReloaded) { // The pageReloaded boolean we set earlier
    if (storageTime === null || storageTime === undefined
        || (storageTime - new Date().getTime()) > 1000) {
      // If storageTime is null, undefined or is older than 1 second
      // we update the storage time.
    }
  }
}
```

这个小技巧也降低了我们因为客户端硬件性能差而错过浏览器关闭事件的概率。

在客户端硬件性能非常差的情况下，最坏的情况是每个 beforeunload 事件都被检测为 tab 关闭。

# 结论

基于目前所见，我们可以将检测方法归结为三点:

1.  如果导航条目具有重新加载导航类型，则用户重新加载了页面。
2.  如果选项卡计数减少，则用户关闭了一个选项卡。
3.  如果标签计数减少且存储时间差小于 50ms，则用户*可能*关闭了浏览器。

我们在第三点中说可能是因为我们的瓶颈是客户端的硬件性能。即使我们采取了额外的措施来确保准确的结果，我们仍然有可能错过它。也就是说，在大多数情况下，这就足够了。

**我希望你喜欢这本书。**

**我的名字是毗湿奴·萨西德哈兰，我写技术文章、代码和讲故事。我的目标是把复杂的概念简化成简单的东西，并用通俗易懂的语言解释它。我也分享激励过我的真实生活故事。**

**如果你喜欢这篇文章，你可能也会喜欢:**

[](/why-you-should-stop-using-loops-88a6a789106e) [## 为什么应该停止使用循环

### 如果你和我一样，你在 JavaScript 中使用 for 和 while 循环的时间最长。我是说如果它得到了…

javascript.plainenglish.io](/why-you-should-stop-using-loops-88a6a789106e) [](/explaining-javascripts-this-keyword-in-simple-terms-238e26b1d0df) [## 用简单的术语解释 JavaScript 的“this”关键字

### “this”关键字在 JavaScript 中可能有不同的含义，这取决于调用它的位置。

javascript.plainenglish.io](/explaining-javascripts-this-keyword-in-simple-terms-238e26b1d0df) [](/promises-in-typescript-27d887a8d380) [## 打字稿中的承诺

### 想象一下，你去店主那里买糖果。你要一颗糖，店主答应了(即给你一颗糖)

javascript.plainenglish.io](/promises-in-typescript-27d887a8d380) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)