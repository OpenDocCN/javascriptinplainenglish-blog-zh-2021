# Web 开发:静态基础

> 原文：<https://javascript.plainenglish.io/web-development-the-static-fundamentals-94270a9daab8?source=collection_archive---------14----------------------->

## 从基础角度看网络技术

![](img/e1febcfce7a2d31ec1edb4cd09c6ffd0.png)

Image By [Arek Socha](https://pixabay.com/users/qimono-1962238/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2492010)

这是这个系列的第一部分，在这里我将提供一个对你日常使用的网站的基本理解。在第一部分，我们将了解***静态* web 开发**的基础知识。我不会把重点放在实现上，因为这是为了了解这个领域中存在的事情。所以，我想我们现在可以开始了！👨‍🏫

在最基本的意义上，网站与原生应用程序没有什么不同，例如 android/ios 应用程序；除了它只能做网络浏览器允许它做的事情。它不能像其他应用程序一样在客户端系统上运行，因为它是在网络浏览器内 ***渲染****；这是只有网络浏览器才能理解的东西。*

web 开发有两大部分——***前端*** (客户端)和 ***后端*** (服务器端)。先说前端。

# 前端 Web

网站是网页的集合，网页只是普通的 HTML 文件。当你向一个网站的服务器发出请求时，你的浏览器会收到大量的响应数据；但是有一样东西是永远不会缺少的，那就是 HTML。

每个网页都是一个单独的 HTML 文件。每当我们导航到不同的路径时，浏览器都会发出新的请求来获取该页面的 HTML 文件。例如，如果您从 ***/home*** 导航到 ***/about-me*** 路线，它会再次请求服务器获取 ***/about-me*** 页面的 HTML 文件。

最好的检查方法是注意浏览器中的加载指示器。如果它表示正在加载，那么您实际上已经向服务器发出了请求；它在等待回应。如果你想知道为什么在一些网站上没有发生，你会在本系列的下一部分的[中知道原因。😉](https://medium.com/weekly-webtips/the-dynamic-web-ee3c89a14225)

> HTML 代表超文本标记语言，其中 [**超文本**](https://en.wikipedia.org/wiki/Hypertext) 是指包含对某些其他文本的引用的文本。所以本质上，这就是你如何从一个网页跳到另一个网页。

现在，你喜欢这个按钮的样子吗？(点击“运行笔”进行预览)

很可能不是！但是这个呢？

第一个是带有默认样式的普通 HTML 按钮，但是第二个利用 CSS 来应用自定义样式。下面是这个奇特按钮的示例代码:

```
<!-- HTML -->
<button>I'm a Fancy Button!</button>/* CSS */
button {
  color: value; /* consider 'value' as a placeholder */
  background: value;
  border: value;
  padding: value;
  border-radius: value;
  box-shadow: value;
}
```

CSS 代表 ***层叠*** 样式表，实际上陈述了它的作用。样式按照定义的顺序从上到下应用*，就像瀑布一样。**任何重复的样式都会覆盖其先前对应的值**，如下例所示。*

```
*button {
  color: white;
}/* This will override the previous value for 'color' */
button {
  color: black;
}*
```

## *Java Script 语言*

*现在，仅仅 HTML 和 CSS 对于一个现代网站是不够的。比如上面那个 ***花式按钮*** 当你点击它的时候什么都不做。但是按钮实际上是用来触发一些动作的。现在点击下面的按钮，看看会发生什么。*

*你猜对了——是 ***JavaScript*** ！😄它为这些展品增加了功能。就像 HTML & CSS 一样， **JavaScript 是客户端语言**；这意味着它由网络浏览器解释和执行。它不像 C++、Java、Python 和其他常用的 ***服务器端*** 语言，不能在网络浏览器之外本地运行。*

*在 JavaScript 中工作类似于许多其他语言，例如，下面的语句声明了一个名为`myName`的变量，我们可以用它做任何事情。*

```
*var myName = 'Sapinder Singh';*
```

*我们可以在需要的时候使用和操作这个变量。但是在 JavaScript 中，我们不想只处理这些变量；相反，我们希望对页面上的 ***HTML 元素进行操作！***那么我们如何在 JavaScript 中操作 HTML 元素呢？*

*你肯定至少听说过 [**API**](https://developer.mozilla.org/en-US/docs/Glossary/API) (应用编程接口)这个术语。顾名思义，API 是不同软件之间相互通信和提供数据的接口。*

***说到与 HTML 交互，JavaScript 需要**[**DOM API**](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model#html_dom)**即代表文档对象模型**。它以对象模型的形式将 HTML 文档提供给 JavaScript。这个 ***倒树状*** 对象的根就是文档本身。文档中的每个元素都有自己的节点，节点的深度与其包含的子元素的数量一样。*

*因此，如果我想使用 DOM API 选择 JavaScript 中的“漂亮按钮”，我会这样做*

```
*// assuming the button does have an id
var fancyButton = document.getElementById("fancy-button");*
```

*我不会给某个变量赋值，而是给它赋值一个 DOM 元素。然后，我可以将这个变量视为页面上的一个实际元素。下面的语句实现了按钮上“click”的一部分。*

```
*/* Don't worry if you don't understand the syntax, you're here just to understand what it does. */fancyButton.onclick = () => alert("I've been clicked! :)");*
```

*所以本质上， **HTML、CSS 和 JavaScript 构成了一个*现代*网站**前端的基础。我们可以-*

*   *拥有一个或多个 HTML 文件(以及其他 ***可选*** 文件如*)。css* ，*。js* 等。从 HTML 内部链接)*
*   *在任何 web 浏览器中打开**根*根*HTML 文件***
*   *并看到它以网页的形式呈现*

*但是正如你可能猜到的，只要只有我们能看到网页，它就完全没有用。这就是我们现在需要进入下一部分的原因。😛*

# *后端 Web*

*为了向全世界提供我们的网页，需要一个网络服务器。对于这个任务，我们有很多服务器端语言，比如 Java、PHP、Ruby、Python、C++等。我之前提到过，JavaScript 是一种 ***客户端*** 语言，因为它不能在 web 浏览器之外运行以充当 web 服务器。现在我准备承认- **那是一种谎言！**😅*

## *Meet Node.js*

*我们有 [**Node.js**](https://nodejs.dev/learn) 那是一个 [**JavaScript 运行时环境**](https://olinations.medium.com/the-javascript-runtime-environment-d58fa2e60dd0) 。运行时环境结合了不同的工具和技术来提供合适的环境，使其能够运行特定的程序或应用程序。*

*您的 web 浏览器也为 JavaScript 提供了运行时环境，为核心 JavaScript 引擎提供了各种 API，如用于解析 HTML 的 DOM、 [**存储 API**](https://developer.mozilla.org/en-US/docs/Web/API/Storage) 用于在客户端系统上存储网站数据、[**CSSOM**](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)**用于使用 JavaScript 操纵样式等。但是 JavaScript 运行时环境的核心部分是 JavaScript 引擎。***

***谷歌 Chrome 和其他基于 Chromium 的网络浏览器使用谷歌的 V8 引擎运行 JavaScript，JavaScript 是用 C++编写的。有趣的是，Node.js 也使用相同的引擎。但是它没有提供像 DOM 这样的 API，而是使用其他工具来访问操作系统、文件系统、网络等。因此，这使我们能够使用 JavaScript 作为服务器端语言。***

***Node.js 是当今其他后端语言的流行选择。对于那些来自前端的人来说，一个主要的优势是 ***你不需要学习另一种语言来设置服务器*** ！如果你对 JavaScript 足够了解，你就都准备好了。***

## ***服务器的工作***

***服务器总是启动并运行(如果没有崩溃的话！🙄)，监听请求并向其客户端发送适当的响应。响应类型取决于用户提出的请求类型。这些都叫做 ***法*** 。以下是通过 [**HTTP**](https://developer.mozilla.org/en-US/docs/Web/HTTP) 使用的两种最常见的请求方法:***

*   *****GET** —该方法用于从服务器中检索 资源。例如，当您访问任何网站时，浏览器向服务器发出`GET`请求，请求在该路线上显示网页。***
*   *****POST** —这种方式应该用于 ***向服务器发布/提交*** 数据，通常是在 ***创建新资源*的时候。**填写网络表单时，该表单主要采用`POST`方式，如下图所示。***

```
***<!-- HTML -->
<form method="POST">
  <!-- The form fields go here -->
</form>***
```

***我无法向您展示服务器如何在 Node.js 中处理请求和响应的实际实现，因为对于初学者来说可能有点复杂；但是这里有一个 [**伪代码**](https://en.wikipedia.org/wiki/Pseudocode) 为这个工作——***

```
***CREATE an http server using http.createServer()
CALL server.listen() to activate the server// Now handle requests from different routes, e.g. '/home' or any routeIF request.url EQUALS '/home'
  SEND '/home.html'ELSE IF request.url EQUALS '/create-user' // the user wants to visit the page where it can create a new account
  IF request.method EQUALS 'GET'
    SEND '/create-user.html' // if the method is POST, it means the user submitted a form on '/create-user' route
  ELSE IF request.method EQUALS 'POST'
    SEND newlyCreatedAccount***
```

***这是为了让您对服务器有一个简单的了解。如果您注意到 ***/create-user*** 路线上的`POST`方法的处理程序，我们正在尝试基于通过`request`对象接收的数据创建一个新的用户；然后将该`newlyCreateAccount`提供给用户。但我们实际上需要存储该帐户，以便将来记住它。所以，是时候进入下一部分了。***

## ***数据库***

***您可能已经对数据库有了一个概念。数据库就像一个商店，有某种组织和处理数据的方式。一个你会听到的与数据库相关的常见术语是**CRUD**； ***的缩写创建*** 、 ***改为*、、**、T52、更新**和**、删除、。这四项是数据库执行的最基本的操作。*******

***数据库的种类很多，但是 [**两大类**](https://www.logianalytics.com/relational-vs-non-relational-databases/) 是**关系型**和**非关系型**。有时它们也被分别称为 SQL(结构化查询语言)和 NoSQL。让我们来看看每一个-***

*   *****关系/SQL 数据库** —这些类型的数据库以类似表格的格式存储数据，其中每行代表一个实体，而每列保存关于该实体的某些数据，如名称、地址等。MySQL 和 PostgreSQL 是使用 Node.js 时要考虑的两种流行的关系数据库。***
*   *****非关系/NoSQL 数据库**——NoSQL 的“否”不仅指还指*，这意味着它可以是任何形式。这些比它们的 SQL 对应物更加灵活。Node.js 最受欢迎的 NoSQL 选择是 MongoDB 和 Redis。****

***选择数据库取决于要存储的数据类型，建议在做出选择以获得最佳性能之前研究不同的选项。***

## ***服务器端 API***

***想知道你手机上的天气应用程序是如何收集如此大量的天气信息的吗？而谷歌地图是怎么知道什么地方是哪里的呢？而这个小小的[**IP-address-tracker-app**](https://sapinder-pal.github.io/IP-Address-Tracker-Vanilla-JS-CSS/)是从哪里获得所有数据的呢？***

***这都是通过 API 完成的。服务器端 API 类似于 web 服务器，但它不是服务于 web 应用程序，而是将 ***数据*** 提供给其他应用程序，以便它们可以使用它。那个 **ip-address-tracker-app** 利用 ipify 的 [**IP 地理定位 API 来收集关于不同 IP 地址的数据。**](https://geo.ipify.org/)***

***端点可以被认为是最终的目的地，我们可以访问它来获取数据或执行与该数据相关的一些其他操作。端点可能被认为是 URL 的一个奇特的名字。访问一个 API 的任何端点应该返回一些数据而不是一个网页。例如，如果你访问[](https://docs.thecatapi.com/)**的 [**这个端点**](https://api.thecatapi.com/v1/images/search) ，你会收到一个由某个随机图像的 URL 组成的对象，以及关于它的其他细节。*****

*****我们可以在服务器端 API 中拥有任意数量的端点，但是 API 必须遵循一些经过深思熟虑的架构，以便在大型项目中可以访问和维护。web APIs 的标准协议是使用 RESTful 架构。如果你想了解更多，参考这篇关于 RESTful API 的 [**帖子。**](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)*****

*****总结到目前为止-*****

1.  *****我们让 HTML、CSS 和 JavaScript 在客户端协同工作*****
2.  *****我们有一个使用 Node.js 处理客户端请求/响应的服务器*****
3.  *****我们也可以使用数据库来存储数据*****
4.  *****我们也可以提供一个 API 来代替一个应用程序*****

*****现在让我们进入下一部分。*****

# *****托管提供商和域*****

*****我们目前所知的所谓的 ***web 服务器*** 只在我们的本地机器上。我们可以在后台运行服务器，并在浏览器中打开例如 *localhost:8000* 来查看我们的网站。`8000`是一个 [**端口的**](https://computersciencewiki.org/index.php/Ports) 号。但是我们现在需要把服务器 ***托管在本地*** 而不是**托管在其他地方**让全世界都可以使用。我们想把我们的应用程序部署到一个主机服务提供商那里，这个提供商将在它的大型机器上全天候运行我们的服务器。*****

*****你还需要一个 [**域名**](https://en.wikipedia.org/wiki/Domain_name) 以便人们能够在互联网上访问你的服务器，因为现在不能通过本地主机访问。一个域名是 ****。com*** 网址的一部分。比如我网站的网址[**https://blog . sapinder . dev**](https://blog.sapinder.dev)，域名是***sapinder . dev***
其中 ***dev*** 是顶级域名就像***com******org***等。如果你想知道， ***博客*** 部分是一个子域。*****

> *******有趣的事实** 一旦你拥有了域名，你就可以拥有任意数量的子域名。还有， **www** 也是子域！*****

*****除了购买域名，我们还必须定期向我们的主机提供商支付费用，因为他们全天候运行我们的服务器。但是大多数主机提供商提供资源有限的免费服务，我们可以随着需求的增长升级我们的账户。同时，免费层服务对初学者来说绰绰有余，而且他们还提供了一个免费的域名！主要的警告是，它以他们的默认域名结尾。比如 Heroku 的**、T6 * . Heroku app . com**、netlify 的 ****.netlify.app*** 等等。如果你想要你自己的域名，看起来 ***实际上*** 专业，你将不得不购买一个。*****

# *****版本控制*****

*****维护代码也非常重要，因为这是识别和修复当前存在的错误以及为应用程序带来新功能的唯一方法。[版本控制系统](https://careerfoundry.com/en/blog/web-development/whats-version-control-and-why-do-i-need-it/)允许我们跟踪&添加的更改，甚至**将整个应用恢复到之前的版本！现在你知道这些系统有多强大了。*******

*****使用最广泛的 VSC 是 [**Git**](https://git-scm.com/) 。使用 Git 时，您应该知道一些术语，其中一些是-*****

*   *******分支**——分支允许开发人员将他们的 ***代码库*** 放在单独的分支中，每个分支都有特定的用途。例如，我通常为我的代码维护两个不同的分支，即`main`和`development`。实现 git 时，`main`是默认的分支，而出于开发目的，我保留了一个单独的`development`分支。在大型项目中，分支的数量和目的可能会增加。*****
*   *******Stage**——git 中有一个 [**staging area**](https://git-scm.com/about/staging-area) ，存放我们代码中所有*的现成变更。我们通过`git add <file-name>`命令将代码中更改的文件添加到暂存区，以便能够在进行最终的 ***提交*** 之前检查更改，这将我们带到下一点。******
*   ********提交** —在我们审查了变更之后，我们准备运行`git commit`命令，最终在 git 历史中为我们的代码库创建一个新版本。******
*   ********合并** —我们可以 ***将对任何分支所做的*** 变更合并到另一个分支中。假设我对`development`分支进行了更改，并且我也测试了它们，现在我可以将它们`merge`到我的`main`分支中，以将更改发布到服务器。******

## ******远程存储库******

******保存在本地系统某个位置的应用程序代码永远安全的可能性有多大？如果它被删除了，或者被其他人访问了怎么办？你明白了——我们需要把它存储在网上，这样只有我们才能在任何时间和任何系统上访问它。**如果我们不知何故丢失了本地存储库，我们可以*从我们的远程存储库中克隆*它以及所有的 git 历史！********

******远程存储库并不总是 ***私有*** ，而是 ***公有*** 的。他们被称为 [**开源**](https://en.wikipedia.org/wiki/Open_source) 项目，任何人都可以为之做出贡献，因为他们的*源代码*(或者仅仅是代码)对社区中的其他开发人员开放。比如 Firefox，Node.js，VLC 播放器，Linux 等等。，都是任何人都可以参与的开源项目。******

******说到基于云/远程存储平台，最流行的两个是[**Github**](https://github.com)**和 [**Gitlab**](https://about.gitlab.com/) ，前者是领先的解决方案。对于开发者和程序员来说，这些就像脸书，展示他们的项目，并维护它们。如果你想看看，这里有 [**我的 Github 简介**](https://github.com/sapinder-pal) ( *不，我不是这个意思！*😅).********

# ******包扎******

******所以，这是我试图给你最好的网络技术基础概述。在本系列的下一部分中，我们将了解网络的动态部分[](https://medium.com/weekly-webtips/the-dynamic-web-ee3c89a14225)**，它为我们所见的现代网站提供动力。如果你喜欢我的写作风格，请留下来！
你可以跟着我，永远不会错过我未来的任何帖子。而且你也可以在 [Twitter](https://twitter.com/sapinder_dev) 、 [Github](https://github.com/sapinder-pal) 和 [LinkedIn](https://www.linkedin.com/in/sapinder-singh/) 上查看我。********

*********更多内容请看*[***plain English . io***](http://plainenglish.io/)********