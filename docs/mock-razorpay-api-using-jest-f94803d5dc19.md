# 使用 Jest 模仿 Razorpay API

> 原文：<https://javascript.plainenglish.io/mock-razorpay-api-using-jest-f94803d5dc19?source=collection_archive---------12----------------------->

![](img/426a02cd8470bd45e811ce480eb307c3.png)

Automated testing

Jest 是 JavaScript 中最流行的测试框架之一。通过编写测试用例，您可以确保新添加的功能没有错误，并且不会影响您现有的功能。这使得您的应用程序更加可靠、高效，同时也保证了应用程序的质量。使用第三方服务和库是现代项目的常见部分。测试项目中编写的代码很容易，因为您可以完全控制它。但是很难控制第三方服务的行为，为了解决这个问题，我们模仿第三方服务。

此外，作为测试的最佳实践，您应该只测试您的代码，而不是从其他地方导入的代码。理想情况下，供应商编写的测试用例应该覆盖这一部分。模仿只是允许您用一组假的/固定的期望输出来替换实际的实现。Razorpay 是印度流行的支付网关之一，开发者使用它进行在线支付。

让我们看看如何使用 Jest 模拟 Razorpay API 来测试我们的 API。

## 步骤 1: API 实现

下面是代码，展示了 index.js 中 Razorpay API 的实际实现，要了解更多 Razorpay 与 Node.js 的集成，[阅读这里。](/razorpay-integration-with-node-js-4915d03ad8ce)

```
const Razorpay = require('razorpay')const rzp = new Razorpay({
 key_id: "YOUR_KEY_ID",
 key_secret: "YOUR_KEY_SECRET",
})router.post('/create_order', async (req, res) => {
 try {
  const rzpOrder = await rzp.orders.create({
   amount: amount * 100, // rzp format with paise
   currency: 'INR',
   receipt: "receipt#1" //Receipt no that corresponds to this Order,
   payment_capture: true,
   notes: {
    orderType: "Pre"
   } //Key-value pair used to store additional information
  })
  res.send(rzpOrder)
 } catch (err) {
  res.status(501).send(err.message)
 }
})
```

## 步骤 2: API 模拟

现在让我们通过返回每个 Razorpay API 实现的固定输出集来完全模拟 Razorpay 模块。

```
jest.doMock('razorpay', () => {

return jest.fn(() => ({
  customers: {
   create: jest.fn(() => Promise.resolve({
    id: 'cust_123',
    name: "Jest_User",
    currency: "sgd",
    description: "Jest User Account created",
   })),
  },
  orders: {
   create: jest.fn(() => Promise.resolve({
    id: '7JS8SH'
   })),
   fetchPayments: jest.fn(() => Promise.resolve([{
    "entity":"collection",
    "count":1,   
    "items":[{
       "id":"pay_DaaSOvhgcOfzgR",
       "entity":"payment",
       "amount":2200,
       "currency":"INR"
    }]
   }])), 
  },
  subscriptions: {
   fetch: jest.fn(() => Promise.resolve({
    id: 'sub_00000000000001',
    "entity": "subscription",
    "plan_id": "plan_00000000000001",
   })),
   cancel: jest.fn(() => Promise.resolve({
    "id": "sub_00000000000001",
    "entity": "subscription",
   })),
  },
 }));
});
```

嘲讽了 Razorpay 之后，让我们将测试用例写入 index.test.js 文件，并检查 create account API。

```
const request = require('supertest')
const app = require('../../app')
const client = request(app)
const urlPrefix = '/'
let tokendescribe('Create order', () => {
 it('should create order', async () => {
  const res = await client.post(`${urlPrefix}/create_order`)
   .send({
     amount: "2200",
     currency: "inr",
     partial_payment: true,
    })
   expect(res.status).toEqual(200)
 })
})
```

当您运行上面的测试文件时，您将收到订单 id“7j S8 sh ”,而不是“实际订单 Id ”,因为您模仿了 Razorpay API。你可以在[官方文档中了解更多关于 Razorpay &可用功能的信息。](https://razorpay.com/docs)

***感谢阅读。如果你喜欢这篇文章，点击鼓掌按钮或留下评论。***

***原载于 2021 年 4 月 15 日***[***https://noob 2 geek . in***](https://noob2geek.in/2021/04/15/mock-razorpay-api-using-jest/)***。***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)