# 让我们建立一个 MERN 堆栈电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-8b0ef902d25e?source=collection_archive---------2----------------------->

## 第 7 部分:完成项目

在最后一部分，我们将通过构建所有的 React 组件并使用 Stripe Checkout 接受付款来结束我们的应用程序。

![](img/7c7eedc2bb2e998fcb62708b434fe583.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们好！这是 MERN 堆栈系列的最后一部分。在前四部分中，我们详细讨论了应用程序的后端部分——从设置路线到通过 stripe 接受支付；我们在这四个部分做了所有的后台工作。然后，在第五和第六部分中，我们处理了 Redux 动作、reducers 和存储，并构建了身份验证组件。

1.  [第 1 部分—建立项目](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696)
2.  [第二部分——设计模式](https://js.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba)
3.  [第 3 部分—认证和物品路线和控制器](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73)
4.  [第 4 部分——购物车和订单路线及控制器](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71)
5.  [第 5 部分—设置客户端和 Redux](https://js.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd)
6.  [第 6 部分—冗余减速器和认证组件](/lets-build-a-mern-stack-e-commerce-web-app-f26613a344e1)

在最后一部分，我们将通过构建这个项目所需的 React 组件来完成这个项目。

因此，我们将逐个构建所有组件。我们将在上一篇文章中创建的 components 文件夹中构建所有这些组件。

## AppNavbar

这是我们要构建的第一个组件。导航栏将包含登录模式，注册模式，注销按钮，以及链接到我们网站上的各个页面。

我们在这里使用 Reactstrap 组件来构建我们的 Navbar 组件。你可以用最适合你的。

然后，我们从 auth 文件夹导入 LoginModal、Logout 和 RegisterModal。我们还导入了 PropTypes 和 connect 函数。

我们定义一个状态来评估导航条是否打开。我们有一个开关来改变打开和关闭，反之亦然。

我们从 auth props 获取用户和 isAuthenticated 状态。然后我们检查我们是否被认证；如果是，那么我们显示用户名，链接到主页，购物车和订单，还有一个注销按钮。另一方面，如果我们没有被认证，我们得到注册和登录模式。

我们还显示一个 Navbar 品牌，当我们通过认证时，我们显示认证链接，当我们没有通过认证时，我们显示访客链接。

最后，我们定义 mapStateToProps 并在其中添加 auth 状态。然后，我们将它连接到 AppNavbar 类。

## 主页

这是我们应用程序的主页，在这里我们显示所有的商品，并给用户一个将商品添加到购物车的选项。

因此，我们从 actions 文件夹中引入 getItems 和 addToCart 函数，我们将使用它们来获取商品并将商品添加到购物车中。

在挂载时，我们使用 getItems 函数获取所有项目。我们还定义了一个 onAddToCart 函数，当我们在任何产品中单击 AddToCart 按钮时就会触发该函数。它接收 userId 和 productId，并具有 addToCart 函数，将这些值作为参数发送给该函数，并将添加的项数保持为 1。我们当然可以给用户选择项目数量的选项，但是为了简单起见，我们没有在这里实现它。

我们使用基于网格的布局来显示我们的所有项目，所有项目都显示为卡片。我们使用映射功能来映射项目，并在其卡片中显示每个项目的数据。我们还为每个产品提供了一个“添加到购物车”按钮。仅当用户通过身份验证时，才会显示“添加到购物车”按钮。

我们还定义了 mapStateToProps，其中定义了 items、user 和 isAuthenticated。最后，我们使用 connect 函数将动作和 mapStateToProps 与 Home 组件绑定在一起。

## AddItem

该组件用于向商店添加商品。我们没有将此页面链接到导航栏，因为我们不希望用户向我们的商店添加新项目。

> 虽然我们必须创建一个单独的卖家门户，并设置不同的访问安全措施，但由于这是一个初学者教程，我们不会走那么远，只会构建这个组件并允许任何人访问，尽管我们不会将它添加到 Navbar 中(只能通过 URL 访问)。

我们有一个带有标题、描述、类别和价格的状态，这些都与产品相关。

我们有一个类似的 onChange 函数和 onSubmit 函数，就像在注册或登录组件中一样，但有不同的变量和不同的函数(addItem)。

我们有一个包含所有这些字段的表单和一个将商品添加到购物车的按钮。我们在添加时显示一个警告，尽管我们可以有更好的方法来处理这个问题，比如在发生错误时显示一个错误，或者在成功添加时重定向。

最后，我们有一个 mapStateToProps，以及一个将它与 AddItem 组件链接起来的 connect 函数。

## 检验

这是我们创建的助手功能，用于通过 Stripe Checkout 处理支付。我们首先从 react-stripe-checkout 导入 StripeCheckout 函数。

然后，我们添加 Stripe 可发布密钥，然后创建两个函数——onToken 仅使用用户和令牌 id 进行结帐，checkout 函数从购物车组件接收金额、用户和结帐，稍后我们将对其进行定义。

> 在这里，checkout 是我们通过 props 从 Cart 组件接收的一个函数。这是我们用来结帐的动作。

我们使用 StripeCheckout，金额为最低货币值(*我们乘以 100，因为我们使用的是印度卢比，最低值是 1 派斯，等于 1 印度卢比，就像 1 美元有 100 美分)，*令牌、货币和条带密钥。

## 手推车

这是显示用户购物车的组件。它显示了用户购物车中的所有商品，给出了从购物车中删除这些商品的选项，并给出了结帐的选项(为商品付款并订购)。

> 在这篇文章中，我们没有一个好的方法来处理结账和付款后发生的事情。理想情况下，我们应该重定向到订单页面，这可以通过历史和路由器来完成。我们让您来决定在支付失败或支付成功的情况下该怎么做。

我们定义了两个函数— getCartItems 和 onDeleteFromcart，这两个函数都具有获取所有购物车商品和从购物车中删除商品的功能。

只有当用户被加载后，我们才能从购物车中获取商品。否则，我们将获取一个错误。然后，我们通过映射显示购物车中的所有商品，并显示一个删除按钮来从购物车中删除该商品。

显示完所有商品后，我们就有了一个显示账单和我们之前定义的结帐组件的卡片。

然后我们定义 mapStateToProps，然后将它与这个组件连接起来。

## 命令

这是显示用户到目前为止已经下的所有订单的页面。我们使用 actions 文件中的函数 getOrders 来做同样的事情。

一旦我们通过了身份验证并拥有了一个用户，我们就可以获得所有的用户订单，并使用地图功能将它们显示在一个基于卡片的视图中。

接下来，我们定义 mapStateToProps，然后将函数和 mapStateToProps 与 Orders 组件连接起来。

## 主要的

在这个组件中，我们使用 React 路由器为每个组件定义各种路由。这有助于我们拥有一个多路线布局，不同的组件有自己的路线。

我们使用 withRouter、Switch、Route 和 Redirect 来完成所有这些路由。最后，我们用 withRouter 函数包装了主要组件。

要了解更多关于 React 路由器的信息，[请访问官方指南](https://reactrouter.com/)。

这些就是我们需要在组件文件夹中定义的所有组件。

现在，我们将更新我们的 App.js 文件，以反映所有这些更改，并将其与 Redux store 连接。

## 应用

当组件挂载时，我们调度 loadUser 函数。然后，我们用 store={store}值将所有 JSX 代码包装在提供程序中。这里，商店是从我们在第 5 个教程中定义的商店导入的。

我们还使用 BrowserRouter 用 className App 包装 div，因为我们在应用程序中使用了 Routing。

然后我们在 div 中有了 Main 函数。我们在代码的最后一行导出应用程序。

```
import { Component } from 'react';
import { Provider } from 'react-redux';
import 'bootstrap/dist/css/bootstrap.min.css';
import Main from './components/Main';
import store from './store';
import {loadUser} from './actions/authActions';
import { BrowserRouter } from 'react-router-dom';

class App extends Component {
  componentDidMount(){
    store.dispatch(loadUser());
  }
  render(){
    return ( 
      <Provider store={store}>
        <BrowserRouter>
          <div className="App">
            <Main/>
          </div> 
        </BrowserRouter>
        </Provider> 
    );
  }
}

export default App;
```

这个系列到此结束。希望你在这个系列中学到了一些新的有用的东西，并且喜欢这个完整的系列。

感谢大家阅读该系列。更多此类文章系列阅读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，了解 DRF 和 REST APIs 如何工作，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e) [## 用 Django 构建求职门户——概述(第 1 部分)

### 让我们使用 Django 建立一个工作搜索门户，允许招聘人员发布工作和接受候选人，同时…

towardsdatascience.com](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e) [](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221) [## 使用 Django 构建一个社交媒体网站——设置项目(第 1 部分)

### 在第一部分中，我们集中在设置我们的项目和安装所需的组件，并设置密码…

towardsdatascience.com](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221) [](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) [## 使用 React 构建博客应用程序—介绍和设置

### 第 1 部分:在第一部分中，我们处理项目的基础并设置它。

javascript.plainenglish.io](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) 

*在* [***获取更多内容***](https://plainenglish.io/)