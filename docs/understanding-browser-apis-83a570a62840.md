# 了解浏览器 API

> 原文：<https://javascript.plainenglish.io/understanding-browser-apis-83a570a62840?source=collection_archive---------9----------------------->

![](img/0c9fa03188d7a4c4b9e80d59c05ea72f.png)

Photo by [Farzad Nazifi](https://unsplash.com/@euwars) on [Unsplash](https://unsplash.com/photos/p-xSl33Wxyc)

今天，技术进步的增加使每个人都受益。这一事件的转变极大地影响了各个领域，但在这篇文章中，我们更关注网络及其重大进步。web 上的持续改进使得许多 Web 过程变得更快更容易，增加了用户体验，并且通常使开发者和用户都受益。

在本文中，我们将了解 **API** 、**浏览器 API**，并进一步了解网络上可用的**不同类型的现代浏览器 API**。

# 什么是 API？

根据[维基百科对 API](https://en.wikipedia.org/wiki/Application_programming_interface) 的定义:API(应用编程接口)是定义多个软件应用之间交互的接口。它定义了可以发出的请求的种类、如何发出请求、应该使用的数据格式、应该遵循的约定等等。它还可以提供扩展机制，以便用户能够以各种方式扩展现有的功能。

不同类型的 API 有**开放 API**、**内部 API**、**伙伴 API**、**复合 API**、 **RESTFUL** 、 **JSON-RPC** 、 **XML** -RPC、 **SOAP** 。

# 什么是 Web/浏览器 API？

**浏览器 API**(或 web**API**)是内置在**浏览器**中的**API**。他们能够从浏览器和周围的计算机环境中公开数据，这有助于开发人员执行复杂的操作。有了这些 API，我们可以构建利用通知、振动、地理定位等本地特性的应用程序。在本文中，我们将了解 F *etch、支付请求、地理定位、拖放、页面可见性和振动*API。

# 获取 API

这是当今常用的 API 之一。它用于发出网络请求，由于其强大而灵活的特性集，它是`[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)`的更好替代方案。它还定义了相关的概念，如 CORS 和 HTTP Origin 报头。`fetch()`方法接受一个强制参数，即您想要获取的资源的路径。它通过使用`.then()`和`.catch()`方法返回一个解析为该请求的`[Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)`的`[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)`。我们还可以在请求中提供我们的头和主体内容。

在下面的代码中，`fetch()`接受一个参数，一个 Url 字符串，它是我们想要获取的资源的路径，然后返回一个包含响应和错误(如果有的话)的承诺。

```
fetch('[https://randomuser.me/api/](https://randomuser.me/api/)')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.log(error));
```

# 付款申请 API

在每个网上购物系统中，最重要的部分之一就是结账页面。要完成网上购物的过程，在其他地方填写所需的步骤也是困难和累人的。

多亏了 Web API，浏览器中引入了支付请求 API，以改善网上结账体验，并减少在线支付的步骤。它存储和记忆经常使用的支付信息，即卡信息，送货地址，并让用户快速有效地进行在线支付。

将付款申请 API 与“基本卡”配合使用的优势(基于卡的付款包括:

*   **快速购买体验**:一旦用户在浏览器中输入他们的详细信息，然后准备在网上支付商品和服务，他们就不再需要在不同的网站上重复填写相同的详细信息。这将节省他们的时间，并缓解每次购物时必须填写详细信息的压力。
*   **每个网站上的一致体验(支持 API):** 因为支付布局由浏览器控制，所以它可以为用户量身定制体验。这可以包括将 UI 本地化为用户的首选语言。用户将在不同的网站上体验 UX 相同的支付方式，并对此感到熟悉。用户将不再担心因为不了解支付程序或系统接口而放弃支付。
*   **可访问性**:由于浏览器控制支付表的输入元素，它可以确保每个网站上一致的键盘和屏幕阅读器可访问性，而无需开发人员做任何事情。浏览器还可以调整付款单的字体大小或颜色对比度，让用户付款时更加舒适。
*   **凭证管理**:用户可以直接在浏览器中管理自己的信用卡和送货地址。该浏览器还可以跨设备同步这些“凭证”，使用户在购物时可以轻松地在桌面和移动设备之间切换。
*   **一致错误处理:**浏览器可以检查卡号的有效性，可以告诉用户某张卡是否已经过期(或者即将过期)。浏览器可以根据过去的使用模式或商家的限制(例如，“我们只接受 Visa 或 Mastercard”)自动建议使用哪张卡，或者允许用户说出哪张是他们默认/最喜欢的卡。
*   开发人员必须为集成编写更少的代码。一旦初始化了一个`PaymentRequest`对象，API 就会处理剩下的事情。您可以通过提供的 API 方法访问所需的内部信息。

> ***注:*** *付款请求 API 仅适用于 HTTPS 环境。*

付款请求 API 公开了如下几种方法。

*   `[PaymentRequest()](https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequest)` -为创建和管理[用户代理的](https://developer.mozilla.org/en-US/docs/Glossary/User_agent)支付接口提供 API 的对象。
*   `[PaymentRequestEvent](https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequestEvent)`发生`[PaymentRequest](https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequest)`时传递给支付处理者的事件。
*   `[PaymentRequestUpdateEvent](https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequestUpdateEvent)`这使得网页能够响应用户动作来更新支付请求的细节。
*   `[PaymentMethodChangeEvent](https://developer.mozilla.org/en-US/docs/Web/API/PaymentMethodChangeEvent)`表示用户改变支付工具(例如，从信用卡切换到借记卡)。
*   用户选择付款方式并批准付款请求后返回的对象。
*   `[MerchantValidationEvent](https://developer.mozilla.org/en-US/docs/Web/API/MerchantValidationEvent)`代表要求商家(网站)验证自己被允许使用特定支付处理程序(例如，注册为允许使用 Apple Pay)的浏览器。

下面的代码片段包含了在您的网站上实现支付请求 API 所需要知道的一切。你可以在这里看我做的一个现场演示[。只是为了本文的目的，我把它做得很简单。随意创建一个](https://nonsodaniel.github.io/payment-request-demo/)`[p](https://developer.mozilla.org/en-US/docs/Web/API/MerchantValidationEvent)ayment.html`文件，将下面的代码复制到文件中，然后在你的浏览器上测试。

# 地理定位 API

**地理定位 API** 使用户能够向网络应用程序提供他们的位置，如果他们愿意的话。出于隐私的考虑，在该位置可用之前，用户需要获得许可。

WebExtensions 要获取用户的位置，需要在 manifest.json 中的`permissions`下添加`“geolocation”`，第一次请求时，用户的操作系统会提示用户允许位置访问。

地理定位 API 提供的重要方法:

*   `[Geolocation.getCurrentPosition()](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/getCurrentPosition)`:获取设备的当前位置。
*   `[Geolocation.watchPosition()](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/watchPosition)`:注册一个处理函数，每次设备位置改变时都会自动调用，返回用户的更新位置。

下面的代码是一个简单的地理定位代码，通过纬度和经度检索用户的当前位置。随意创建一个`geolocation.html`文件，复制并粘贴代码到其中，然后在你的浏览器上测试。

***注意:*** 地理定位 API 仅在[安全上下文](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts) (HTTPS)、部分或全部[支持浏览器](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API#browser_compatibility)中可用。

有关地理定位用法的更多信息，请阅读使用地理定位 API 的[。](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API)

# 拖放 API

HTML 拖放 API 允许应用程序在浏览器中使用拖放功能。当用户用鼠标选择*可拖动的*元素，将这些元素拖动到*可放下的*元素，并通过释放鼠标按钮放下它们。这个 API 使用从`[mouse events](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)`继承的`[DOM event model](https://developer.mozilla.org/en-US/docs/Web/API/Event)`和`[*drag events*](https://developer.mozilla.org/en-US/docs/Web/API/DragEvent)`。典型的*拖动操作*开始于用户选择一个*可拖动的*元素，将该元素拖动到一个*可放下的*元素，然后释放被拖动的元素。

拖动操作期间触发的各种事件

*   `[ondrag](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondrag)`当*拖动项*(元素或文本选择)被拖动时，该事件被触发。
*   `[ondragend](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondragend)`当拖动操作结束时(如释放鼠标按钮或点击或按下 Esc 键),触发该事件。
*   `[ondragenter](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondragenter)`当被拖动的项目进入有效的放置目标时，触发该事件。
*   当一个被拖动的项目离开一个有效的放置目标时，这个事件被触发。
*   `[ondrop](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondrop)`表示当一个项目被放到一个有效的放置目标上时触发此事件。(参见[执行下降](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#drop)。)

下面的代码是如何使元素*可拖动的示例代码，其中*需要添加`[draggable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-draggable)`属性和`[ondragstart](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondragstart)`全局事件处理程序。

# 页面可见性 API

页面可见性 API 使我们能够通过最小化窗口或切换到另一个选项卡或应用程序来跟踪用户何时活动或何时离开当前选项卡。

> 例如，当您查看 whatsapp 状态，然后最小化 whatsapp 以播放一些 youtube 视频时。当你回到 whatsapp 应用程序时，你会发现它会从你停止浏览的地方继续，为你创造一个流畅的体验。

当用户最小化窗口或切换到另一个标签时，API 会发送一个`[visibilitychange](https://developer.mozilla.org/en-US/docs/Web/API/Document/visibilitychange_event)`事件，让监听器知道页面的状态已经改变。您可以检测事件并执行一些操作或采取不同的行为。

值得注意的是，页面可见性 API 通过让页面在文档不可见时避免执行不必要的任务，对节省资源和提高性能特别有用。

# 振动 API

振动是大多数现代移动设备的普遍特征。这是可能的，因为振动硬件的存在，它让软件代码通过使设备振动来向用户提供物理反馈。**振动 API** 为网络应用提供了访问该硬件的能力(如果它存在的话),如果设备不支持它，它什么也不做。

> 根据 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Vibration_API) 的说法，振动被描述为开关脉冲的模式，其长度可能不同。该模式可以由描述振动毫秒数的单个整数组成，也可以由描述振动和暂停模式的整数数组组成。用单一方法控制振动:`[Navigator.vibrate()](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/vibrate)`。

您可以通过指定单个值或仅包含一个值的数组来使振动硬件产生一次脉冲。下面是触发设备振动 200 毫秒的示例代码

```
window.navigator.vibrate(200);
window.navigator.vibrate([200]);
```

我们还可以创造连续的振动，甚至处理停止/恢复振动。下面的代码解释了它。

# 结论

与目前 Web 上可用的 API 相比，本文中介绍的不同类型的 Web APIs 只是其中的一小部分。要了解其他 web 浏览器 API 的更多信息，包括一些仍在开发中的 API，请查看 [MDN Web API 文档](https://developer.mozilla.org/en-US/docs/Web/API)，了解其他 API、它们的规范、用法、兼容性以及您可能有的其他问题。

# 相关主题

[如何创建简单的文本到语音转换应用](https://nonsodaniel.medium.com/how-to-create-a-simple-text-to-speech-web-application-2a8fdb9ccbcc)

[如何创建一个简单的语音转文本应用](/how-to-create-a-voice-to-text-application-2cb12e6b50fd)

# 进一步的解释/参考

*   [Web API](https://developer.mozilla.org/en-US/docs/Web/API) ，“Mozilla 开发者网络

*更多内容请看*[***plain English . io***](http://plainenglish.io)