# 让我们建立一个 MERN 堆栈电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd?source=collection_archive---------2----------------------->

## 第 5 部分:设置客户机和 Redux

在第五部分中，我们将使用 React 为我们的应用程序设置客户端，并将使用 Redux 进行应用程序中的状态管理。

![](img/8ce17b54b76c94bbe0e4f40f965ca908.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们好！这是 MERN 堆栈系列的第五部分。在前四部分中，我们详细讨论了应用程序的后端部分——从设置路线到通过 stripe 接受支付；我们在这四个部分做了所有的后台工作。

如果你还没有阅读前四部分，我把它们链接在这里给你

[](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 1 部分:设置项目

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 2 部分:设计模型

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 3 部分:构建身份验证和项目路由和控制器

medium.com](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 4 部分:构建购物车并订购路线和控制器

medium.com](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) 

因此，从第五部分开始，我们将开始关注前端部分。在这一部分中，我们将开始用 React 设置项目的客户端，还将利用 Redux 库来管理 React 应用程序中的所有状态。

因此，首先，我们需要在我们的根文件夹中创建一个新的文件夹(这里有我们所有的后端文件)。我们将这个文件夹命名为*‘客户端’，*，我们将所有与客户端相关的文件都放在这个文件夹中。

我们将使用 *create-react-app* 为我们建立一个 react 项目，这样我们就不需要处理各种复杂的东西，比如 babel 和 webpack。使用这个命令将使这个过程变得容易得多，并且我们将能够把注意力集中在重要的事情上。

因此，在创建名为 *client、*的文件夹后，我们将移动到该文件夹中，并运行以下命令在该文件夹中创建一个新的 react 应用程序。

```
npx create-react-app .
```

或者，如果您还没有创建 *client* 文件夹，您可以输入这个命令在名为 *client* 的文件夹中建立一个新的 React 项目，然后移动到 *client* 文件夹中。

```
npx create-react-app client
```

这将在我们的应用程序中建立一个新的 React 项目。我们可以同时运行服务器和客户机，正如我们在本系列的第 1 部分中同时安装了*和*并为此定义了节点脚本。我们需要运行`npm run dev`来同时运行它们。

现在，打开客户端文件夹中的 *package.json* 文件。我们将看到它包含安装的各种依赖项。我们还将安装更多我们将在项目中使用的依赖项。

这里是客户端的 *package.json* 文件。看，这里提到了很多依赖。我们将在我们的项目中需要所有这些。

现在，您已经看到了依赖项，让我们一个接一个地检查一下，看看我们安装了什么，它为我们提供了什么功能。

1.  **Axios** — Axios 将用于与 REST APIs 交互，并从服务器获取数据。
2.  **Bootstrap** — Bootstrap 将是我们用来设计前端的前端 CSS 库。
3.  **redux —** 这是我们将用来管理状态的状态管理库。
4.  **react-redux —** 这是 redux 的 react 版本，将用于管理我们的应用程序的状态。(由于 Redux 可以与各种框架和库一起使用。这个是用来反应的。)
5.  **react-router-dom —** 这将管理我们的应用程序的路由。它将帮助我们定义路线，并允许它们从一条路线到另一条路线。
6.  **redux-thunk** —这是我们将在应用程序中使用的中间件，它将帮助我们管理应用程序的状态。
7.  **reactstrap** —它是用于引导样式的 React 版本，允许我们使用引导类作为 React 组件。
8.  **react-stripe-checkout —** 它用于在我们的应用程序中使用 stripe 来接受支付。

此外，我们将设置一个代理，允许我们将请求传输到 *localhost:4000* 。因为我们在端口号 3000 上运行我们的应用程序，并且我们不想编写一个完整的 URL 来与 API 交互，所以我们将定义一个代理来将请求从 3000 传输到 4000。

现在，我们将查看客户端文件夹中的文件。因此，我们将查看 *src* 文件夹。我们有一个 *index.js* 文件，在其中我们不需要做任何修改。这里是 *index.js* 文件:-

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

接下来，我们来看看 *App.js* 文件:-

```
import { Component } from 'react';
import 'bootstrap/dist/css/bootstrap.min.css';

class App extends Component {
  render(){
    return ( 
        <div className="App">
          <h1>Hello everyone!</h1>
        </div> 
    );
  }
}

export default App;
```

我们已经将*引导程序*导入到这个文件中。此外，我们将清除所有预先编写的代码。

稍后，我们将对该文件进行一些修改，以合并 Redux 状态管理和路由。

接下来，我们将开始设置 Redux 状态管理。我们将在 *src* 文件夹中创建一个名为 *store.js* 的新文件。

所以，这是我们的 *store.js* 文件。它将作为我们州的仓库。要了解这是怎么回事，强烈建议对 Redux 有一些了解。

```
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};

const middleWare = [thunk];

const store = createStore(rootReducer, initialState, compose(
    applyMiddleware(...middleWare),
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
));

export default store;
```

如果你仔细观察，我们已经从 reducers 文件夹中导入了一些我们到现在还没有创建的东西，即 *rootReducer* 文件。我们一会儿会做的。

如果你不明白这是怎么回事，我建议你先学习 Redux 如何工作，以便更好地理解它。我也相信 Redux 具有挑战性。

但是这里的好消息是我们不需要为了任何目的再次访问这个文件。这是建立 Redux 商店的标准方式。我们对此无能为力，因为这就是 Redux 的工作方式。

现在，我们将开始在 *src* 文件夹中构建 *actions* 文件夹。这是标准的 Redux 方式，有*存储，动作*和*减速器。*

所以，首先，我们从 *actions* 文件夹内的 *types.js* 文件开始。这里我们将定义所有的动作类型。这是重复的做事方式。

```
export const GET_ITEMS = 'GET_ITEMS';
export const ADD_ITEM = 'ADD_ITEM';
export const DELETE_ITEM = 'DELETE_ITEM';
export const UPDATE_ITEM = 'UPDATE_ITEM';
export const ITEMS_LOADING = 'ITEMS_LOADING';

export const CART_LOADING = 'CART_LOADING';
export const GET_CART = 'GET_CART';
export const ADD_TO_CART = 'ADD_TO_CART';
export const DELETE_FROM_CART = 'DELETE_FROM_CART';

export const ORDERS_LOADING = 'ORDERS_LOADING';
export const GET_ORDERS = 'GET_ORDERS';
export const CHECKOUT = 'CHECKOUT';

export const USER_LOADING = 'USER_LOADING';
export const USER_LOADED = 'USER_LOADED';
export const AUTH_ERROR = 'AUTH_ERROR';
export const LOGIN_SUCCESS = 'LOGIN_SUCCESS';
export const LOGIN_FAIL = 'LOGIN_FAIL';
export const LOGOUT_SUCCESS = 'LOGOUT_SUCCESS';
export const REGISTER_SUCCESS = 'REGISTER_SUCCESS';
export const REGISTER_FAIL = 'REGISTER_FAIL';

export const GET_ERRORS = 'GET_ERRORS';
export const CLEAR_ERRORS = 'CLEAR_ERRORS';
```

首先，我们拥有与项目相关的所有类型；接下来，我们有购物车、订单，然后是用户，最后是错误。

因此，在这个 *actions* 文件夹中，我们将有另外五个文件，分别是— *itemActions、authActions、cartActions、orderActions* 和 *errorActions* 。

因此，我们将在这里逐一处理它们。因此，我们将从 errorActions 开始，因为这非常简单，不需要与服务器交互。

## 错误操作

这个动作文件中有两个函数。我们有一个用于返回应用程序中的任何错误，另一个用于在不需要显示错误时清除这些错误。

第一个函数将在函数中接收消息、状态和 id，并将它们作为 GET_ERRORS 类型的有效负载返回。

下一个函数是通过将类型作为 CLEAR_ERRORS 发送来清除错误。

这些将在我们将在下一部分构建的错误减少器文件中处理，该文件将处理这些函数指定的状态。

## authActions.js

这是动作文件中最复杂的部分，因为它将处理所有的认证部分。这部分我们有四个功能——*加载用户，注册，登录*和*注销*。

我们还有一个助手函数 *tokenconfig* ，它将从本地存储中获取令牌，并设置配置以使用 loadUser 发送请求，从而获取当前登录的用户详细信息。

现在，我们可以详细了解这四个函数了

1.  **loadUser** —首先将类型设置为 USER_LOADING，表示用户当前正在加载。然后，我们使用 Axios 向 api 端点 *'/api/user'* 以及从 *tokenconfig、*获得的令牌发出一个请求，该请求将获得结果并将有效负载设置为从 API 端点获取的数据。类型将被设置为 USER_LOADED，因为我们已经成功加载了用户。如果出现任何错误，我们将调用 returnErrors 函数，并将类型设置为 AUTH_ERROR。
2.  **register** —它从前端获取用户名、电子邮件和密码，然后将它们变成一个 JSON 对象。然后，我们点击 API 端点来注册并传入数据。然后，我们接收一个响应，并将接收到的数据设置为有效载荷，类型设置为 REGISTER_SUCCESS。我们处理错误的方式与前面的函数相同，并将错误类型设置为 REFGISTER_FAIL。
3.  **登录** —其工作方式类似于注册功能。不同之处在于，登录函数只获取电子邮件和密码，然后点击 API 端点进行登录。我们得到一个响应，并将有效负载设置为从响应接收的数据，并将类型设置为 LOGIN_SUCCESS。我们以类似的方式处理错误，并将错误类型设置为 LOGIN_FAIL。
4.  **注销** —我们只需将类型设置为 LOGOUT_SUCCESS，这就是我们注销所需要做的一切。

我们将在下一部分描述的 reducers 文件中处理所有这些响应类型及其有效负载。

## 项目操作

在这里，我们将处理与项目相关的所有操作，即我们将在网站上显示的产品。

它有五个功能来管理获取项目，添加一个新的项目，删除一个项目，更新一个项目和设置项目状态为加载。

虽然在本系列中我们不会在应用程序组件中使用删除和更新项目，但是做好一切准备是一个不错的选择，以防我们以后需要添加这些内容。

> 注意:您可以添加一个单独的门户来管理所有项目，如添加、删除和更新项目。虽然我们已经为所有这些任务准备好了 API、actions 和 reducers，但是我们只涉及添加项目和获取组件中的所有项目。

1.  **getItems** —这个函数用于使用一个为获取项目而设计的 API 端点从后端获取所有项目。我们首先将项目设置为 loading，然后到达 API 端点来获取所有项目。然后，我们将类型设置为 GET_ITEMS，将有效负载设置为作为响应接收的数据。
2.  **addItem** —该函数用于向数据库添加一个新项目。为此，我们通过前端表单接收 item 对象，并将这些数据发送给负责添加项目的 API 端点。然后，我们将类型设置为 ADD_ITEM，将有效负载设置为从响应接收的数据。
3.  **deleteItem —** 该函数用于从数据库中删除一个现有项目。它接收我们想要删除的项目的 id，并使用删除请求将其发送到用于此目的的 API 端点。然后，我们将类型设置为 DELETE_ITEM，将有效负载设置为已删除项的 id。
4.  **updateItem —** 此功能用于更新我们库存中的现有项目。它在 id 的帮助下向 API 端点发出 put 请求，并发送新的 item 对象。然后，我们将类型设置为 UPDATE_ITEM，将有效负载设置为 id，将从服务器接收的数据设置为响应。
5.  **setItemsLoading** —该函数将类型设置为 ITEMS_LOADING。

## 行动

它处理与任何用户的购物车相关的所有操作。它有四个功能，分别是获取购物车、向购物车添加商品、从购物车中删除商品以及将购物车状态设置为正在装载。

1.  **getCart** —该函数用于为任何用户获取购物车。首先，我们将购物车设置为 loading。这个函数将 id 作为一个参数传递给 API 端点，并接收一个包含用户购物车的响应。我们将类型设置为 GET_CART。
2.  **添加购物车** —该功能用于向购物车添加商品。它接受用户的 id 作为参数，并传递 productId 和 quantity 作为请求体。然后，我们接收一个响应，并将其分配给有效负载，并将类型设置为 ADD_TO_CART。
3.  **deletefromcarth**—该功能用于从购物车中删除商品。它接收 userId 和 itemId，并将它们作为参数传递给 API 端点。然后，我们将类型设置为 DELETE_FROM_CART，并将有效负载设置为响应的数据。
4.  **setCartLoading** —将类型设置为 CART_LOADING。

## **订单操作**

这个操作文件处理与我们的应用程序中的订单相关的所有操作。它有三个功能，用于获取用户的所有订单，下一个新订单(结帐)和设置订单为加载。

1.  **getOrders** —该功能首先将订单设置为加载。接下来，它使用接收到的用户 id 作为发出 GET 请求的参数。然后，我们将类型设置为 GET_ORDERS，将有效负载设置为作为响应接收的数据。
2.  **结账** —该功能用于下订单。它从组件接收两个参数，即用户的 id 和源。源代码是从条带检出函数中生成的，我们将在后面的部分创建它们时详细处理这些函数。然后，我们使用 id 作为参数，使用 source 作为请求体，并发出 POST 请求。然后，我们将类型设置为 CHECKOUT，将有效负载设置为响应的数据。
3.  **setOrdersLoading** —该功能将订单类型设置为 ORDERS_LOADING。

## 结论

这就是我们在这部分要处理的。在下一部分中，我们将处理减速器，并开始处理一些组件，然后在最后一部分中，我们将在处理剩余的组件部分后结束该系列。

教程的下一部分可以在这里找到:-

[](/lets-build-a-mern-stack-e-commerce-web-app-f26613a344e1) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 6 部分:构建 Redux Reducers 并处理组件

javascript.plainenglish.io](/lets-build-a-mern-stack-e-commerce-web-app-f26613a344e1) 

如果你想访问这个项目的完整代码，请访问这个项目的 [GitHub 库](https://github.com/shubham1710/MERN-E-Commerce)。

我希望你喜欢教程系列的这一部分，也希望你对即将到来的部分感到兴奋。

看完这个系列后，还有更多故事要读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221) [## 使用 Django 构建一个社交媒体网站——设置项目(第 1 部分)

### 在第一部分中，我们通过设置密码来集中设置我们的项目和安装所需的组件…

towardsdatascience.com](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221)