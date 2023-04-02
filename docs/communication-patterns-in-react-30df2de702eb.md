# React 中的通信模式

> 原文：<https://javascript.plainenglish.io/communication-patterns-in-react-30df2de702eb?source=collection_archive---------2----------------------->

## 从基础到更复杂的事情，爱丽丝终于和鲍勃说话了！

![](img/179571b8c6696776d6cc52fd4c495565.png)

Photo by [Quino Al](https://unsplash.com/@quinoal?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# TL；速度三角形定位法(dead reckoning)

*   **亲子沟通的道具**->儿童沟通
*   **回调道具**用于子- >父沟通
*   **共同祖先**:不可伸缩，几乎是一种反模式
*   **事件冒泡**:隐式耦合，显然是一种反模式
*   **通过服务器**:为什么不呢？
*   **反应上下文**，还有呢？
*   基于 React 上下文，让我们添加一些**契约**
*   **发布订阅**

React 现在是一个开发单页面应用程序(spa)的成熟环境，拥有专业开发人员有权期待的每一个工具:启动项目、(结构)打字、linters，加上许多维护良好的、可用于生产的库。

然而，当代码库增长时，人们面临两个主要问题:

*   **构图**。它的第一个目的是确保每个组件只有*一个*职责，这就是众所周知的 SRP(单一职责原则)。第二是避免一遍又一遍地写同样的代码，这就是所谓的干禁令(不要重复自己)。在 React 中，只有 4 种组合模式:直接调用子组件、高阶组件(HOC)、render-props 模式(与 HOC 相比，大多数人更喜欢这种模式)和钩子。没错。
*   但是更多的组件也意味着让它们相互交流的额外技术。沟通将是我们今天的重点。

在本文中，我们将讨论常见通信模式的优缺点，然后讨论对其他模式的需求。

# 先说第一件事:道具，回调道具和共同祖先模式。

得益于 React properties 对象，即众所周知的“ **props** ”，父->子通信非常简单。`message`是下面代码示例中的属性之一。

相反，子->父通信由**回调 props** 保证，即父(`sendMessage(message: string): void`)提供的一个函数被其子(`message`)用感兴趣的数据调用。在父组件中，这些数据必须处于一种状态(`useState()`)才能被使用。

这让我们很自然地想到了**公共祖先**模式，用于给定组件的后代之间的通信，从兄弟(同一个组件的两个孩子)开始。假设`Alice`必须与她的兄弟`Bob`通信，这个模式组合了一个回调属性用于从`Alice`到`Parent`的通信，然后组合了一个属性用于从`Parent`到`Bob`的通信。

```
Alice --(callback property)--> Parent (state) --(property)--> Bob
```

这是相当系统的，但它显然没有规模。对于一级亲属(兄弟姐妹)，该模式导致 1 个回调属性、1 个状态和 1 个属性。对于二级亲属(表亲)来说，已经是 2 个回调道具，1 个状态，2 个道具了。以此类推，对于 N 度亲属，就是 N 个回调道具，1 个状态，N 个道具。换句话说，这就是道具钻井的诅咒，我们应该寻求更好的解决方案。

# 为了全面起见

在跳到更适合“远距离”通信模式的附加部分之前，让我们先提一下**渲染道具**。对于单个`render`属性(或任何最合适的名称)，父组件避免传输`message`属性，因为相应的数据(`"Hello World!"`)仅用于`render`函数的目的。从父对象传递给子对象用于直接显示的数据越多，而没有子对象负责的进一步计算，使用 render props 模式就越有意义。

你还可以在下面这个优雅但不常见的“作为孩子的功能”变体下找到渲染道具模式。它稍微有些限制性，因为它只允许一个渲染属性:

# 有反模式吗？

是的…事件冒泡在这方面看起来是个不错的选择。事件冒泡描述了一个子组件发出一个事件而没有捕获它的情况。它在 React 树中的一个祖先代替了它。

这种模式使得组件之间的耦合是隐式的:通过查看单个的`Parent`组件，或者同样地查看单个的`Child`组件，通信并不明显。如果`Child`被移动到它的`Parent`树之外，所有东西都会坏掉。此外，在传输数据时，事件是非常有限的。通常，唯一可用的信息是事件本身的存在…

随着原生 DOM 事件冒泡，情况变得更糟。这与上面的情况相同，但是事件是本地 DOM 事件，而不是 React 事件(`React.ReactSyntheticEvent`)。

为什么会更糟？因为 React 的要点是虚拟 DOM，它是本地 DOM 之上的一个抽象层次。本质上，虚拟 DOM 提供了一个声明性的 API 来操作 DOM，而不是本地的命令式 API。因此，*虚拟 DOM* 组件之间通过*本地 DOM* 事件的通信混合了抽象层次，违背了总是在同一抽象层次[工作的原则](https://en.wikipedia.org/wiki/Abstraction_(computer_science)#Levels_of_abstraction)。

更一般地说，当稍后引入额外的通信模式时，我们将特别注意总是依赖虚拟 DOM。

# 简单点，笨蛋！

回到我们主要关心的问题:如何确保相距遥远的组件之间的通信？所谓“远亲”，我指的是两个组件都不是对方的后代:它们有一个共同的祖先，但是对于共同祖先模式来说，它在树中的位置太高了。

那么，在这种情况下，通过服务器进行通信是一个应该经常考虑的解决方案。基本模式是:

```
1\. Alice sends data to the server;
2\. Later, Bob fetches the data from the server.
```

在下面的例子中，延迟获取是由用户触发的，但是该模式也适用于来自服务器(WebSockets)的推送通知。

如果加以推广，这种模式会导致应用程序状态主要位于服务器上，而不是浏览器上。因此，尽管这种方法很实用，但与常规应用程序相比，它可能会质疑单页面应用程序的相关性。和往常一样，业务约束有助于做出架构决策:如果许多用户可能更新同一块数据，那么状态必须在服务器上。

# 现在，让我们以 React 上下文为基础

终于！好的。让我们停止旁敲侧击，考虑一下与我们关注的问题相关的常见疑点:[反应上下文](https://reactjs.org/docs/context.html)。

> 上下文提供了一种通过组件树传递数据的方式，而不必在每一层手动向下传递属性。

这是一个有趣的基础。人们可能希望有两个改进:

*   仅更新作为上下文提供的对象的子部分的能力，并且仍然受益于变更检测(当提供新的引用时触发变更检测`<MessageContext.Provider value={...}>`)；
*   某种契约化，因为上下文对象是应用程序状态将存在的地方。它必须被视为一个黄金来源，一个所有成分的真理的单一来源。

这就是引入 [Flux](https://facebook.github.io/flux/) 架构的地方，随后是 Redux、MobX 等。但是 Redux 远不止这些，因为它附带了事件源。

因此，让我们稍微倒退一下，构建最简单的商店对象。商店是保护国家的大门。我们通过一个`getState(): State`和一个`setState(reducer: Reducer<State>): void`方法来约束读写操作。

人们应该注意到`getState(): State`没有提供任何保护:返回状态可能会被错误地改变。没有实施不变性的库(想想[不可变](https://immutable-js.com/)或 [Immer](https://immerjs.github.io/immer/) )，不变性依赖于君子协定。

那么必须做出选择来更新状态。这里有两种选择:

*   直接更新:`setState(state: State): void`；
*   通过减速器`(state: State): State`和`setState(reducer: Reducer): void`更新。

直接更新至少有两个缺点。

首先，因为只有状态的一部分要被更新，所以必须首先检索当前状态，然后传播。这种逻辑`const state = getState();`会在每次更新时重复，这是我们想要避免的:

```
const state = getState();
const newState = {
  ...state,
  // override some attributes
};
setState(newState);
```

但是更深入地说，使用 Reducer 允许在一次重新渲染之前链接和批量更新，而第一个选项不允许。

下面有很多代码，您可以安全地跳到下一个代码示例，它展示了商店的运行情况。对于那些想深入了解的人来说，这里的难点是允许在状态更新时进行更改检测，而整个存储对象必须*而不是*发生更改。这里我们依靠一个简单的`renderIndex`作为密钥。

同样，如果上面的代码现在对你来说没有意义，它肯定是没问题的。更重要的是商场在运作:

这种契约化为人们认为有用的任何其他模式打开了大门。这正是我们将通过探索一个 PubSub 模式来实现的。

# 发布/订阅(发布订阅)

这种模式是众所周知的，甚至被[骨干](https://backbonejs.org/)用在前端。许多库，从 [PubSubJS](https://github.com/mroderick/PubSubJS) 、 [postal.js](https://github.com/postaljs/postal.js) 和 [EventEmitter](https://github.com/Olical/EventEmitter) 开始，用普通的 JavaScript 提供了很好的实现。但是如上所述，我们希望我们的实现在与 React 相同的抽象层次上工作，而不是更低。下面，`Channel`和`PubSub`是普通的 JavaScript 类，然后我们使用 React API(Context、HOC 和 hooks)使它们在 React 组件中可用。

发布/订阅的要点是解耦，或者说是松耦合。通信通过事件总线进行。因此，发布者不知道它在和谁交谈，反过来，订阅者也不知道事件来自谁。

```
Publisher --> Event bus --> Subscriber
```

在引擎盖下，它依赖于[观察者模式](https://en.wikipedia.org/wiki/Observer_pattern)。等等……什么？这意味着紧密耦合，对吗？右图:受试者保留了其观察者的记录。有道理，所以让我们把事情弄清楚:观察者模式发生在事件总线和订阅者之间，而不是发布者和订阅者之间:

```
Publisher --> Event bus --(observer pattern)--> Subscriber
```

顺便说一下，从轮询开始，其他实现也可以工作。

嗯……说了很多，还是没有代码！这就是:

瞧！

当然，这只是一个要点，而不是一个生产就绪的实现。为了简单起见，它是同步的，而在“现实世界”中通常以异步方式实现。但是，毕竟，在浏览器中，组件之间的异步通信有什么用呢？

这提供了一个相当简单的 API:

# 为了全面起见(再次)

同样，为了全面起见，让我们提一下 [React 门户](https://reactjs.org/docs/portals.html)。官方文件称:

> 门户提供了一种一流的方法来将子组件呈现到父组件的 DOM 层次结构之外的 DOM 节点中。

换句话说，它允许虚拟 DOM 中的`parent-child`关系，而它们在 DOM 中的具体化(渲染元素)位于不同的树中。

所有已经看到的交流模式都适用:道具、回调道具、上下文等。

这在特定的用例中非常有用，比如模态和通知，但是你不能把它想象成一个系统的通信模式。

我们到了！本文概述了 React 组件之间的通信模式。事实上，它们中的大多数确实适用于其他库和框架(Vue.js，Angular…)

我很乐意听到您的反馈，尤其是关于 PubSub 模式的用例:您遇到过它有用的情况吗？

感谢阅读！

# 进一步阅读

*   [https://github . com/mathieueveillard/react-communication-patterns](https://github.com/mathieueveillard/react-communication-patterns)
*   [https://stack overflow . com/questions/21285923/react js-two-components-communicating](https://stackoverflow.com/questions/21285923/reactjs-two-components-communicating)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)