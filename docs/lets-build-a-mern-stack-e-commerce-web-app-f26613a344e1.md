# 让我们建立一个 MERN 堆栈电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-f26613a344e1?source=collection_archive---------3----------------------->

## 第 6 部分:构建 Redux Reducers 并处理 Auth 组件

在第六部分中，我们将通过构建所有 reducers 文件来完成 Redux 设置。我们还将处理 React 应用程序中与身份验证相关的组件。

![](img/28a468350c94a4d08347ac3219f46246.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们好！这是 MERN 堆栈系列的第六部分。在前四部分中，我们详细讨论了应用程序的后端部分——从设置路线到通过 stripe 接受支付；我们在这四个部分做了所有的后台工作。然后在第五部分，我们开始构建我们的前端，设置 Redux 动作和存储。

如果你还没有阅读前五部分，我把它们链接在这里给你

[](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 1 部分:设置项目

js .平原英语. io](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 2 部分:设计模型

js .平原英语. io](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 3 部分:构建身份验证和项目路由和控制器

js .平原英语. io](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 4 部分:构建购物车并订购路线和控制器

js .平原英语. io](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) [](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 5 部分:设置客户机和 Redux

js .平原英语. io](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd) 

因此，在第六部分，我们将通过构建 Redux 文件来完成 Redux 设置，并且我们将开始处理一些组件。

所以，让我们首先开始构建 reducer 文件。我们将在*客户端*文件夹中创建一个文件夹，我们将其命名为 *reducers。*在这个文件夹中，我们将创建六个文件——index、authReducer、itemReducer、errorReducer、cartReducer 和 orderReducer。

## 自动减速器

所以，首先是 auth reducer 文件。顾名思义，这个文件用于身份验证。

我们首先从 *actions* 文件夹的 *types* 文件中导入认证所需的所有类型。

我们设置一个初始状态，从本地存储中检索令牌。我们还将 *isAuthenticated* 设置为 null，将 *isLoading* 设置为 false。我们还将*用户*字段设置为 false。

然后，我们开始检查每种行动类型，并进行适当的更改。

1.  **USER_LOADING** —如果是这种类型，我们可以说用户正在被加载，因此我们将 *isLoading* 设置为 true。
2.  **USER_LOADED —** 在这种情况下，我们将 *isLoading* 设置为 false，将 *isAuthenticated* 设置为 true。我们还将用户*设置为我们从动作文件中接收到的有效负载。*
3.  **LOGIN_SUCCESS，REGISTER_SUCCESS** —在这两个场景中，我们将 *isAuthenticated* 设置为 true，并且我们还设置了在本地存储中接收的令牌。
4.  **AUTH_ERROR、LOGIN_FAIL、LOGOUT_SUCCESS、REGISTER_FAIL** —在所有这四种情况下，我们都从本地存储中删除令牌。我们将令牌和用户设置为 *null。*我们还将 *isAuthenticated* 和 *isLoading* 设为 false。

## itemReducer

现在，我们将处理 itemReducer 文件，它将处理与该应用程序中的项目相关的所有任务。我们将首先导入与项目相关的所有类型。

我们设置了一个初始状态，其中我们将*项*设置为空数组，并将*加载*设置为假。

然后，我们开始检查每种行动类型，并进行适当的更改。

1.  **获取 _ 物品** —这是获取物品的缩减器。在这种情况下，我们将把 items 数组设置为从 actions 接收的有效负载。我们还将 loading 设置为 false，以表示项目已经被加载。
2.  **ADD_ITEM** —在这种情况下，我们使用 spread 操作符调用我们的状态，然后将从有效负载接收的新项添加到 items 数组中。
3.  **DELETE_ITEM** —在这种情况下，我们通过有效负载获取被删除项目的 id。因此，我们获取 items 数组，并通过过滤移除 id 匹配的项。
4.  **UPDATE_ITEM —** 在这种情况下，我们从有效负载中获取 id 和更新的项目。然后，我们使用 id 从 items 数组中找到该项，然后用新项更新它。
5.  **ITEMS_LOADING —** 我们将 LOADING 设置为 true，表示正在加载项目。

## 误差缩减器

在这个缩减器中，我们将管理应用程序的错误部分。我们导入两种与错误相关的类型。

然后，我们定义一个初始状态，将*消息*设置为空对象，*状态*设置为空，并且 *id* 也设置为空。

我们有两个案子要处理。第一种情况处理获取错误，第二种情况处理清除错误。

1.  **GET_ERRORS —** 我们设置从动作的有效负载中收到的消息、状态和 id。
2.  **CLEAR_ERRORS** —在这种情况下，我们只需重置一切。我们将消息设置为一个空对象，并将状态和 id 设置为 null。

## 卡式减速器

在这个文件中，我们将处理与用户购物车相关的减速器。我们从 actions 文件夹中定义的*类型*文件中导入与购物车相关的类型。

我们将初始状态定义为购物车设置为空，装载设置为假。

1.  **GET _ CART**—在这种情况下，我们通过来自 actions 文件的有效负载接收购物车，并将其设置为我们在初始状态中定义的购物车。我们还将 loading 设置为 false。
2.  **ADD_TO_CART，DELETE_FROM_CART—** 在这两种情况下，我们都获取更新后的购物车，并将购物车设置为从操作接收到的有效负载。
3.  **CART_LOADING** —在这种情况下，我们将 LOADING 设置为 true。

## 订单缩减器

在这个文件中，我们将处理与我们的应用程序中的订单相关的减速器。我们首先导入订单的所有相关类型。

然后，我们定义一个初始状态，在该状态下，我们将订单定义为一个空数组，还定义了 loading 并将其设置为 false。

1.  **GET_ORDERS —** 在本例中，我们将 ORDERS 数组设置为从 actions 文件接收的有效负载。我们还将 loading 设置为 false。
2.  **CHECKOUT** —在这种情况下，我们从有效负载接收新订单，并将其添加到订单数组中。
3.  **订单 _ 装载—** 我们将装载设置为 true。

## 索引(组合减速器)

在这个文件中，我们从所有不同的文件导入所有的 reducer——items、cart、order、auth 和 error，然后使用从 redux 获得的 *combineReducers* 函数将它们组合起来。

现在，我们已经完成了所有的冗余工作。现在，我们可以专注于为我们的应用程序构建组件。

> 注意:在这个应用程序中，我们将有一个非常糟糕的设计。我们不关注 CSS 和动画。我们只是关心 React，所以如何以一种更好的方式设计它们取决于你。

因此，我们将在这一部分讨论身份验证所需的组件，并在本系列的下一部分讨论所有其他组件。

首先，我们将在客户端文件夹中创建一个名为 *components* 的文件夹。因为我们将所有的认证组件与我们的其他组件分开，所以将在*组件*文件夹中创建另一个名为 *auth* 的文件夹。

我们的登录和注册将是基于模态的，这将显示在导航栏中。

## loginModal

因此，我们将在这个文件中构建我们的登录组件。我们将从 React 导入*组件*。我们从 Reactstrap 导入各种东西，我们将使用它们来制作我们的组件。我们还从 react-redux 导入了*连接*。

我们还导入了 PropTypes 来定义我们将在这个文件中使用的所有 prop 类型。此外，我们导入登录和清除错误操作。

我们定义了一个状态，将 email 和 name 设置为空字符串。我们还将 modal 设置为 false，msg 设置为 null。

然后我们定义我们所有道具类型。然后，我们将设置 *componentDidUpdate* ，并将之前的道具作为参数。然后我们检查当前的错误对象是否等于前一个错误。如果不是，那么我们检查错误是否来自 LOGIN_FAIL，如果是，我们将 msg 设置为错误的 msg；否则，我们将 msg 设置为空。

我们还检查我们是否被认证；如果是，我们关闭模态。

然后我们设置一个切换函数来切换模态的状态。我们还设置了一个 onChange 函数，当我们在表单字段中键入时，它会更新电子邮件和密码的值。

然后，我们设置一个 onSubmit 函数，它从状态中获取电子邮件和密码，并将它们传递给登录操作。

接下来，我们用 JSX 代码来显示我们的模态和模态中的表单。在表单中，我们有两个输入字段，电子邮件和密码。我们还有一个提交按钮。

之后，我们定义一个 *mapStateToProps* ，并从我们在 reducer 文件中设置的状态中获取 *isAuthenticated* 和 *error* 。最后，我们将 LoginModal 连接到这些状态和动作函数，并将其导出。

## 注册模式

这将处理我们网站上的注册。这将与登录模式非常相似，因此我们不会详细讨论。只有一些不同——比如我们使用了*注册*动作，而不是*登录*动作。这次我们有三个字段—姓名、电子邮件和密码。因此，我们的表单将有三个输入字段。

其余大部分保持不变。当提交表单时，我们调用 register 动作，并将三个值传递给它。

## 注销

这个很简单。它只是使用了一个导航链接和一个显示注销的按钮。单击时，它调用注销操作。我们将它与注销操作连接起来，然后将其导出。

所以，这就是这部分的全部内容。我们已经完成了 Redux 部分，还构建了认证所需的组件。

在下一部分，也是最后一部分，我们将构建其余的组件，并结束这个系列。

[](/lets-build-a-mern-stack-e-commerce-web-app-8b0ef902d25e) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 7 部分:完成项目

javascript.plainenglish.io](/lets-build-a-mern-stack-e-commerce-web-app-8b0ef902d25e) 

如果你想访问这个项目的完整代码，请访问这个项目的 [GitHub 库](https://github.com/shubham1710/MERN-E-Commerce)。

我希望它能帮助你学到一些东西，并让你感到兴奋。完成本系列后，您还可以阅读更多此类文章:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e) [## 用 Django 构建求职门户——概述(第 1 部分)

### 让我们使用 Django 建立一个工作搜索门户，它允许招聘人员发布工作并接受候选人，同时…

towardsdatascience.com](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e)