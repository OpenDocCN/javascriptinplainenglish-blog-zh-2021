# 如何在 React 中使用 Cookies 实现“购物车”功能

> 原文：<https://javascript.plainenglish.io/cookies-in-react-202c3df273c6?source=collection_archive---------8----------------------->

我在项目中解决的问题实现了类似购物车的功能。

![](img/f17cb649f64ef172372c68a90ae4565f.png)

Shopping cart resting on keyboard

## **背景**

当我在[熨斗](https://flatironschool.com/)为我的最终项目创建一个 React 应用程序时，我遇到了一个问题，我需要能够将我的应用程序的各个方面与不同的用户相关联，但不需要进行用户认证——我的应用程序中没有任何部分需要保密。

我开发的应用程序的基础是允许用户查看由 [Picsum API](https://picsum.photos/) 生成的随机图片，并对它们进行投票，因此，总的来说，用户会在互联网上找到“最好”的图片，或者至少是 Picsum 生成的最好的图片。

用户还可以查看一系列热门图片(基于喜好)，以及趋势图片(你可以在这里找到趋势/流行算法的介绍)。用户喜欢的图片会被添加到他们的“收藏”中。用户不能对他们收藏的图片做任何事情，除了查看或下载，因此，我认为没有必要允许用户拥有个人资料。相反，我使用 cookies 来识别用户——类似于网站如何保存你的购物车，即使你从未登录或创建个人资料。

## **使用 Rails 作为 API**

顺便提一下，虽然我的应用前端使用 React，但我在后端使用 Rails 来跟踪图片及其与用户的关联。我保持简单。用户可以通过客户端 cookies 中创建和存储的 id 找到或创建(稍后将详细介绍)，图片可以通过 Picsum 提供的 id 找到或创建。

当用户喜欢一张图片时，我的后端会检查用户是否存在，图片是否存在，用户和图片之间是否已经存在关联。用户可以从他们的收藏中删除图片，从而删除用户和 pic 之间的关系，但不能否决他们收藏中的图片。

## **创建 cookie**

我能够保存用户的照片集合，同时通过在前端实现 cookies 来防止用户对同一张照片进行多次投票。其实很简单:

```
// add 'react-uuid' via yarn add or npm install
// *cookieHelpers.js*
import uuid from 'react-uuid'export const createCookie = () => {
  if (document.cookie) {    
    return document.cookie
  } else {
    // console.log(uuid()) => '57e1ef0-b8c3-3b81-252c-e54fb572dc'
    const userUUID = `userUUID=${uuid()}`

    // make sure your cookies don't expire
    const expiration = `expires=${new Date('01/01/2100').toUTCString()}`

    // SameSite=Lax should be default, but I had issues while
    // testing on firefox
    document.cookie = `${userUUID};${expiration};SameSite=Lax`;
    return document.cookie// *App.js*
...
import {createCookie} from './helpers/appHelpers'class App extends Component {
  // Create and set the cookie when component mounts
  componentDidMount() {
    const cookie = createCookie()
    // Assuming you have a redux store with a setCookie
    // action and reducer
    this.props.setCookie()
  }
}
```

这就是全部了。我也使用 Redux，所以我将用户的标识符存储在应用程序的商店中。

## **使用创建的 Cookie**

由于我在用户启动应用程序时检索或分配用户的标识符，因此我可以在向后端发送获取请求时使用该 id。我能够检索用户喜欢的图片集，并确保它们不会重复喜欢一张图片。

## **结论**

虽然我使用 React 只有几个星期，但我绝不是专家，我相信我在项目中试图解决的问题类似于让用户的“购物车”持久化的问题，因此上面的代码可以被派生和抽象用于广泛的应用程序。感谢阅读！

*更多内容尽在*[plain English . io](http://plainenglish.io/)