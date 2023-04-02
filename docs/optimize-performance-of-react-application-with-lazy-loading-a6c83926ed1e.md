# 通过延迟加载优化 React 应用程序的性能

> 原文：<https://javascript.plainenglish.io/optimize-performance-of-react-application-with-lazy-loading-a6c83926ed1e?source=collection_archive---------11----------------------->

## 改进 React 中的页面加载时间，减少暂停和延迟，并确保 React 应用程序优化

![](img/da0a3ea6fdab1d3d2277b5c4839bd477.png)

[Technofunnel](https://medium.com/technofunnel) 展示了另一篇文章，通过在执行过程中使用**组件的惰性加载**来提高 React 应用程序的性能。我们会明白**懒**和**悬疑**的概念。

默认情况下，React 应用程序的所有组件都捆绑在一个**中。js"** 文件并加载到浏览器上。由于所有应用程序组件都在捆绑文件中，因此，创建的 JavaScript 的大小相对较大。由于我们要加载一个更大的 JavaScript 文件，这可能会影响应用程序的初始加载时间。

# React 应用程序捆绑流程

**捆绑**是将多个文件导入并合并成一个文件的过程，这样应用程序就不必导入大量外部文件。如果每个组件都驻留在一个单独的文件中，我们将需要在初始页面加载期间加载许多“JavaScript”。每个请求都将在网络上传输，消耗网络带宽，HTML 解析器将不得不等待来自网络的大量文件。

***将组件捆绑成一个文件的问题:***

为了避免这种情况，React 编译器会将所有主要组件和外部依赖项合并到一个文件中，并通过网络发送该文件以启动和运行 web 应用程序。这节省了大量的网络调用，但也导致了一个问题，即这个单个文件变成了一个大文件，消耗了大量的网络带宽。应用程序一直在等待这个大文件的加载和执行，因此这个文件在网络上传输的延迟会导致应用程序的渲染时间更长。

***进一步理解问题:***

[https://gist.github.com/Mayankgupta688/fa7cb362028b8a512f4902d80edc663d](https://gist.github.com/Mayankgupta688/fa7cb362028b8a512f4902d80edc663d)

在上面的代码中，基于从“props”接收的“name”属性，我们决定呈现哪个组件。用户可以呈现“GuestLogin”或“MemberLogin”组件。在任何时候，这些组件中只有一个会被渲染。

当 React 捆绑应用程序时，它将这两个组件组合成一个 JavaScript 文件。然后在浏览器中加载该文件，虽然其中一个组件是必需的，但是我们在 JavaScript 中加载了这两个组件，这使得它很大，很难加载。这会导致应用程序的加载时间增加。

**违约行为问题:**

*   第一个问题是 JavaScript 代码变得太大，会延迟应用程序的页面加载
*   即使没有在屏幕上加载，组件也会被加载

## 解决延迟加载的问题:

为了解决这个问题，我们可以引入 ***代码拆分*** 的概念。我们可以将文件分成多个小的 JavaScript 输入。每个 JavaScript 文件可能包含某些组件，这些组件可以根据需要加载，而不是将所有内容绑定到一个文件中。

按照上面给出的例子，我们可以在运行时根据“props”值决定加载哪个组件。如果用户名是“Mayank ”,我们可以加载“MemberLogin ”,否则我们可以加载包含“GuestLogin”的文件。我们可以在执行过程中动态加载这些文件。

**使用惰性加载 React 组件的好处**:

1.  主 JavaScript 文件将包含所有组件
2.  组件可以根据需求在运行时加载
3.  所需的子组件将装入单独的小包装中
4.  更快的加载时间，因为主 JavaScript 相对较小

像[**web pack**](https://webpack.js.org/)**这样的捆绑器支持代码拆分的概念，它们可以为应用程序创建多个捆绑包，并且可以在运行时动态加载。我们以某种方式分解包，以便最初没有加载到应用程序中的组件可以推迟到以后需要时再加载。**

**这将减小主包的大小，并减少应用程序的加载时间。为此，我们使用**反应悬念**和**懒惰**。让我们寻找下面的代码来理解这个概念的实现。**

**在上面的代码中，我们将“name”值作为“Mayank”传递，因此它应该在一个单独的组件中加载“MemberLogin”组件。**

**![](img/5f896388293a8e24a585b6076dca2dd6.png)**

**在执行下面的代码时，它加载一个文件“1.chunk.js ”,该文件单独加载这个“MemberLogin”组件，从而使主 JavaScript 文件更小，加载和执行更快。**

****更多优化技巧，可以参考以下网址:****

**[](https://medium.com/technofunnel/https-medium-com-mayank-gupta-6-88-21-performance-optimizations-techniques-for-react-d15fa52c2349) [## 22 反应性能优化技术

### React 编程的最佳优化技术。

medium.com](https://medium.com/technofunnel/https-medium-com-mayank-gupta-6-88-21-performance-optimizations-techniques-for-react-d15fa52c2349) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)**