# 如何用 IndexedDB 在客户端存储数据

> 原文：<https://javascript.plainenglish.io/how-to-store-data-client-side-with-indexeddb-7d924bebe8f3?source=collection_archive---------18----------------------->

## 它得到了很好的支持，允许您存储大文件，而且使用起来也没那么糟糕。

![](img/a987f0a1f90a48c292ec5f7efee280ae.png)

A database isn’t much more than a set of drawers, really | Photo Credit: [Jan Antonin Kolar](https://unsplash.com/@jankolar)

想象一次微积分考试，你必须在脑子里做所有的计算。这在技术上是可能的，但是绝对没有理由这样做。同样的原则也适用于在浏览器中存储内容。

今天，有许多广泛实施的客户端存储技术。我们有 cookies、 [Web 存储 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) 和 [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) 。虽然完全有可能编写一个功能完整的 web 应用程序而不用担心这些问题，但是您不应该这样做。那么如何使用它们呢？他们每个人都有最适合的用例。

# 浏览器存储快速概述

## 饼干

基本上每个请求都会发送 Cookies，它最适用于短数据。cookies 的最大优点是服务器可以通过使用`Set-Cookie`头直接设置它们，不需要 JavaScript。对于任何后续请求，客户端将发送一个包含所有先前设置的 cookies 的`Cookie`头。这样做的缺点是，大的 cookies 会严重降低请求速度。这就是接下来两项技术的用武之地。

## 网络存储

Web 存储 API 由两个相似的存储组成— `localStorage`和`sessionStorage`。它们都有相同的界面，但后者仅在浏览会话处于活动状态时持续。只要有可用内存，前者就会持续存在。这个内存限制既是它最大的优点，也是它最大的缺点。

因为这些值不会随每个请求一起发送，所以可以在不影响性能的情况下在其中存储大量数据。然而，“大”是相对的，不同浏览器的存储限制可能会有很大差异。一个好的经验法则是为你的*整个*站点存储不超过 5 MB。这个限制并不理想，如果你需要存储更多，你可能需要第三个也是最后一个 API。

## 索引 b

有人可能会说，指数化 DB 被严重低估了。尽管基本上每个浏览器都支持它，但它远没有其他两个受欢迎。它不像 cookies 那样随每个请求一起发送，也没有网络存储的任意限制。那么是什么原因呢？

IndexedDB 不太受欢迎的原因是，事实证明，它的使用是绝对痛苦的。您需要手动定义成功和错误处理程序，而不是使用`Promises`或`async/await`。许多库都封装了这种功能，但是它们经常是多余的。如果你需要的只是保存和加载数据，你可以自己写所有你需要的东西。

# 整齐地包装索引 DB

虽然有很多方法可以与 IndexedDB 交互，但我将描述的是我个人的、**固执己见的**方法。这段代码适用于一个数据库和一个表，但是应该很容易修改以适应其他用例。在我们开始编写代码之前，让我们快速列出我们需要的需求。

**1。理想情况下，它是某种我们可以导入和导出的类或对象。**

**2。每个“对象”应该只代表一个** `database` **和** `table` **。**

**3。很像 CRUD API，我们需要读取、保存和删除键值对的方法。**

这似乎很简单。只是一个旁注——我们将在这里使用 ES6 `class`语法，但是你可以随意修改。如果你只对一个文件使用一个类，你甚至不需要使用它。现在让我们开始吧。

## 一些样板文件

我们本质上知道我们需要什么方法，所以我们可以剔除这些方法，并确保所有的函数都有意义。这样，就更容易编码和测试(我没有这样做，因为这是一个个人项目，但我真的应该去做)。

嘿，看起来你在一个稍微窄一点的屏幕上。下面的代码块可能看起来不太好，但文章的其余部分应该没问题。如果你想跟上，你可以跳到一个更宽的屏幕上。我哪儿也不去(保证)。

在这里，我们设置了一些样板文件，其中包含了我们所有的功能和一个很好的常量配置。`_config`周围的`setter`确保配置在任何点都不能改变。这将有助于调试任何错误，并从一开始就防止它们发生。

样板文件完成后，是时候进入有趣的部分了。让我们看看可以用 IndexedDB 做些什么。

## 从数据库中读取

即使 IndexedDB 不使用`Promises`，我们也将把所有的函数包装在其中，这样我们就可以异步工作。从某种意义上说，我们将要编写的代码将有助于弥合 IndexedDB 和更现代的 JavaScript 编写方式之间的差距。在我们的`read`函数中，让我们将所有内容包装在一个新的`Promise`中:

如果我们从数据库中获得值，我们将使用`resolve`参数沿着`Promise`链传递它。这意味着我们可以在代码中的其他地方做类似的事情:

现在我们已经设置好了，让我们看看我们需要做些什么来打开连接。要打开实际的数据库，我们需要做的就是调用`window.indexedDB`对象的`open`方法。我们还需要处理三种不同的情况——如果有错误，如果操作成功，如果我们需要升级。我们现在就把这些剔除掉。到目前为止，我们看到的是这样的:

如果`open`错误出来了，我们可以简单地用一个有用的错误信息`reject`它:

对于第二个处理程序`onupgradeneeded`，我们不需要做太多。只有当我们在构造函数中提供的`version`不存在时，才会调用这个处理程序。如果数据库的版本不存在，就没有什么可读取的。因此，我们所要做的就是中止交易并拒绝`Promise`:

这就给我们留下了第三个也是最后一个处理程序，用于成功状态。这是我们真正阅读的地方。我在前面的处理程序中忽略了事务，但是现在值得花时间回顾一下。因为 IndexedDB 是一个 NoSQL 数据库，所以读写是在**事务**中执行的。这些只是对数据库执行的不同操作的记录，可以用不同的方式还原或重新排序。当我们中止上面的事务时，我们所做的只是告诉计算机取消任何未决的更改。

现在我们已经有了数据库，我们需要对我们的事务做更多的工作。首先，让我们获得实际的数据库:

现在我们有了数据库，我们可以连续地获得事务和商店。

第一行创建了一个新事务，并声明了它的*范围*。也就是说，它告诉数据库它将只处理一个存储或表。第二个获取存储并将其赋给一个变量。

有了这个变量，我们终于可以完成我们的目标了。我们可以调用该商店的`get`方法来获取与键相关联的值。

我们就快结束了。剩下要做的就是处理错误和成功处理程序。需要注意的一件重要事情是，我们正在检查实际结果是否存在。如果没有，我们也会抛出一个错误:

完成后，下面是我们的`read`函数的全部内容:

## 从数据库中删除

`delete`功能经历了许多相同的步骤。这是整个函数:

您会注意到这里有两个不同之处。首先，我们在`objectStore`上调用`delete`。其次，成功处理程序会立即解决问题。除了这两个，代码基本上是相同的。第三个也是最后一个函数也是如此。

## 保存到数据库

同样，因为它是如此的相似，这里是`save`函数的全部:

这里有三点不同。首先是需要填写`onupgradeneeded`处理程序。这很有意义，因为应该支持在新版本的数据库中设置值。在这里，我们简单地使用恰当命名的`createObjectStore`方法创建了`objectStore`。第二个区别是我们使用了`objectStore`的`put`方法来保存值，而不是读取或删除它。最后一个区别是，与`delete`方法一样，成功处理程序会立即解析。

完成所有这些后，下面是所有这些看起来的样子:

要使用它，您只需创建一个新的`DB`对象并调用指定的方法。例如:

# 一些收尾工作

如果您想在另一个文件中使用它，只需在末尾添加一个导出语句:

然后，在新脚本中导入它(确保一切都支持模块)，并将其命名为:

然后，按原样使用。

一如既往，别忘了关注我，获取更多类似这样的内容。我目前正在写关于[开发到](https://shaile.sh/devto)和[介质](https://shaile.sh/medium)的文章，非常感谢您对这两个平台的支持。我还建立了一个会员资格，在那里你可以获得文章的预览，并独家访问一大堆资源。此外，如果你特别喜欢这篇文章，可以考虑请我喝杯咖啡来支持我。下次见！

*原载于*[*https://shaile . sh*](https://shaile.sh/codes/posts/2021/01/21/storing-files-indexed-db/)*。*