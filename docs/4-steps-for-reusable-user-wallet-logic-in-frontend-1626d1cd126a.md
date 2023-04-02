# 前端可重用用户钱包逻辑的 4 个步骤

> 原文：<https://javascript.plainenglish.io/4-steps-for-reusable-user-wallet-logic-in-frontend-1626d1cd126a?source=collection_archive---------16----------------------->

一次编写，随时随地使用。😎✌️

![](img/87f4cd88383f7065b75e4eaae7aa8a4e.png)

Photo by [Tech Daily](https://unsplash.com/@techdailyca?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

这个想法从关于前端认证的可重用逻辑的最后一个故事开始。如果你还没有读过，我强烈建议给它一个机会，因为这个故事是一个故事链，我所有的文章最多需要 7 分钟来阅读😎。

[](https://shreyvijayvargiya26.medium.com/reusable-authentication-logic-in-frontend-beded754d4b7) [## 前端中可重用的身份验证逻辑

### 一次编写，随时随地使用😎

shreyvijayvargiya26.medium.com](https://shreyvijayvargiya26.medium.com/reusable-authentication-logic-in-frontend-beded754d4b7) 

好了，让我们开始今天的故事，想法是编写可重用的前端逻辑来执行用户钱包系统。

## 概观

这个想法很简单，每个与支付相关的移动应用都有自己的钱包系统。现在这种情况很常见，所以为什么不写一个可重用的基本逻辑，让它随时随地都可以使用。

## 关键要求

前端业务中的每个钱包只需要很少的东西，这些是访问钱包和相应的`beneficialId`的令牌。我们甚至可以将这些细节存储在数据库中，但是与其通过网络获取数据，为什么不在前端编写逻辑呢？

## 要遵循的步骤

我们整个逻辑的步骤包括以下内容-

*   创建初始用户钱包状态或全局存储
*   创建相应的操作以在应用程序中启用用户钱包系统
*   创建一个操作来更新全局存储中的用户钱包详细信息。
*   每次进行新交易时，重复使用用户钱包的详细信息

## 初始全局存储

如果您已经阅读了前面的故事，那么我们已经为用户创建了相同的默认全局状态。类似地，我们将为用户定义默认或初始钱包状态。您可以选择通过扩展在用户状态中定义状态，或者将钱包状态从用户数据状态中分离出来。

```
const initialState = {   
   isUserLoggedIn: false,
   loggedInUserData: { // user emails and id },
   token: String,
   userWalletData: { 
    beneficialId: String,
    upiId: String
    }
};
```

对于这个故事，我只假设我们只存储用户`beneficialId`和 UPI id。我们可以创建多个状态，例如，另一个 UPI ID 或相应的电子邮件连接到相应的 UPI ID 等等。您的产品提供的可扩展特性越多，您需要定义的状态就越多。

## 启用钱包的操作

用户必须做的第一步也是最重要的一步是启用钱包系统。在大多数情况下，我们使用第三方支付或钱包系统，所以我们需要用户通过提供 UPI id 来启用它。

然后，我们进行网络调用或 API 调用，以获取相应的用户详细信息，如电子邮件和用户 UPI id 的授权确认。该步骤基本上是在启用钱包系统之前的确认检查，以防止任何误用，尤其是当应用程序被外来实体使用时。

一旦网络调用给出了关于用户钱包细节和 UPI id 的绿色信号，我们就从同一个网络调用中获取用户`beneficialId`，作为响应，我们可以将它存储在我们的`userWalletData`中的全局存储中。

```
function setUserWallet({ upiId, beneficialId }{
   initialState.userWalletData.upiId = upiId;
   initialState.userWalletData.beneficialId = beneficialId;
};async function enableUserWallet(upid){
  const response = await.post('/enable-wallet', { upi: upi });
  if(response.success){ 
   setUserWallet({ upidId, beneficialId: response.benefialId });
  };
};
```

在上面的过程中，我们可以通过在 post 请求的主体中提供 UPI id 来进行网络调用，一旦响应成功，我们就可以在全局存储中使用用户`UPI` id 来设置用户`beneficialId`。

## 进行交易的行动

如果您查看默认的初始状态，我们也已经定义了令牌，现在是使用令牌的时候了。用户进行的每一笔交易都必须是安全的，所以大多数时候，我们的服务器会检查用户是否经过授权和认证，这仅由令牌进行检查。

一旦用户成功登录到我们的应用程序，我们就存储这个令牌，现在为了进行每一个新的交易，我们必须在 POST 请求的头中提供这个令牌以及交易的金额。

大多数情况下，令牌也可能是由第三方提供的，您将使用该第三方的钱包，因此在网络调用中对用户 UPI id 进行身份验证时，我们会得到两个响应:`beneficialId`和交易令牌。因此，在这种情况下，您可以用一个密钥存储新令牌，如`transactionToken`

```
const initialState = {   
   isUserLoggedIn: false,
   loggedInUserData: { // user emails and id },
   token: String,
   userWalletData: { 
    beneficialId: String,
    upiId: String
    }
    transactionToken: String, // token recived with beneficialId
};
```

接下来的部分是进行交易。每笔交易都需要一个令牌在头部，金额在请求体，如果交易成功，我们得到交易细节，如 id，我们可以存储的`transactionStatus`告诉交易成功。

我们甚至可以在初始状态下存储事务的细节，这是你的选择，但我建议只存储少量的事务细节，否则`intitalState`的大小会增加，并可能导致性能问题。

```
function setTransaction({ transactionId,amount,transactionStatus }{
   initialState.traactions.push = 
        { 
           transactionId, 
           amount, 
           transactionStatus  
        }
};async function enableUserWallet(upid){
  const response = await.post('/enable-transation', 
   { upi: upi });
  if(response.success){ 
   setUserWallet({ upidId, beneficialId: response.benefialId });
  };
};
function makeTransation({ amount, beneficalId, token }){
  const response = await axios.get('/make-transaction', 
   headers: {
     token: Bearer token
   }
   {
     body: { amount, beneficialId  } 
   }
  );
  if(response.success){
    setTransaction({ 
     transactionId: response.transactionId, 
     amount: amount,
     transactionStatus: true
     })
  }else {
     setTransaction({ 
       transactionId: response.transactionId, 
       amount: amount,
       transactionStatus: false
     })}
  }
}
```

在网络呼叫响应的基础上，我们设置交易状态，以向用户给出关于交易的适当指示。这是钱的问题，所以对交易给出适当的指示对产生信任非常重要。

我们最终的全球商店将如下所示-

```
const initialState = {   
   isUserLoggedIn: false,
   loggedInUserData: { // user emails and id },
   token: String,
   userWalletData: { 
    beneficialId: String,
    upiId: String
    }
    transactionToken: String, // token recived with beneficialI
    transactions: [
       transactionId: String, 
       amount: Number,
       transactionStatus: Boolean
     ]
};
```

## 结论

同样，这个逻辑是基本的基础，每次和大多数情况下，这个逻辑都是围绕这个概念解决的。所以我们的想法是创造一次，随时随地使用。

具有讽刺意味的是，我们正在使用相同的逻辑在我们即将发布的网站( [**iHateReading**](http://www.ihatereading.in) )中启用钱包支付系统。因此，您可以信任流程和逻辑，并根据自己的方便修改它。

今天就到这里吧，下次再见，祝你愉快。

```
For more such stories, Our wesbite - 💻 [**iHateReading**](http://www.ihatereading.in)
```

## 更多阅读

[](/forget-the-browser-drag-drop-api-this-library-is-perfect-to-add-drag-and-drop-feature-f2a1a9e7d8e3) [## 在你的网络应用中开发拖放功能

### 与 React DnD 合作，将拖放功能添加到您的网站

javascript.plainenglish.io](/forget-the-browser-drag-drop-api-this-library-is-perfect-to-add-drag-and-drop-feature-f2a1a9e7d8e3) [](https://medium.com/codex/there-are-high-chances-that-redux-will-be-replaced-98f1c469bcce) [## redux 很有可能被取代

### 看看 redux 的竞争对手，redux 很有可能在未来被取代。

medium.com](https://medium.com/codex/there-are-high-chances-that-redux-will-be-replaced-98f1c469bcce) [](https://medium.com/nerd-for-tech/forms-and-validation-in-react-6f185108037f) [## React 中的表单和验证

### React 钩子形式入门。

medium.com](https://medium.com/nerd-for-tech/forms-and-validation-in-react-6f185108037f) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)