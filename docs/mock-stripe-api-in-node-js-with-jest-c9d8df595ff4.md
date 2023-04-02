# 如何用 Jest 模仿 Node.js 中的 Stripe API

> 原文：<https://javascript.plainenglish.io/mock-stripe-api-in-node-js-with-jest-c9d8df595ff4?source=collection_archive---------3----------------------->

![](img/f617f7138783303441cc370ff28a725d.png)

Testing with Jest

Jest 是 JavaScript 中最流行的测试框架之一。开发人员使用它来自动防止 CRUD 崩溃。使用第三方服务和库是现代项目的常见部分。测试项目中编写的代码很容易，因为您可以完全控制它。但是很难控制第三方服务的行为，为了解决这个问题，我们模仿第三方服务。

此外，作为测试的最佳实践，您应该只测试您的代码，而不是从其他地方导入的代码。理想情况下，供应商编写的测试用例应该覆盖这一部分。模仿只是允许您用一组假的/固定的期望输出来替换实际的实现。Stripe 是一个流行的国际支付网关，被开发者用于在线支付。

因此，让我们看看如何使用 Jest 模拟 Stripe API 来测试我们的 API。

下面是代码，展示了 Stripe API 在 index.js 中的实际实现，要了解更多关于 Stripe 与 Node.js 的集成，[阅读这里。](https://medium.com/@shraddha.paghdar/stripe-integration-with-node-js-6adb8cbc81f7)

```
const stripe = require('stripe')('sk_test_...');router.post('/create_account', async (req, res) => {
 try {
  const customer = await stripe.customers.create({
   email: req.body.email,
   name: `${req.body.firstName} ${req.body.lastName}`,
   phone: `${req.body.countryCode} ${req.body.phoneNo}`,
   description: 'User Account Created'
  })
  res.send(customer)
 } catch (err) {
  res.status(501).send(err.message)
 }
})
```

现在，让我们通过返回每个 Stripe API 实现的固定输出集来完全模拟 Stripe 模块。

```
jest.doMock('stripe', () => {

return jest.fn(() => ({
  customers: {
   retrieve: jest.fn(() => Promise.resolve({
    id: 'cust_123'
   })),
   create: jest.fn(() => Promise.resolve({
    id: 'cust_123',
    name: "Jest_User",
    currency: "sgd",
    description: "Jest User Account created",
   })),
  },
  coupons: {
   create: jest.fn(() => Promise.resolve({
    id: '7JS8SH'
   })),
  },
  subscriptions: {
   retrieve: jest.fn(() => Promise.resolve({
    id: 'sub_123',
    object: 'subscription',
   })),
   del: jest.fn(() => Promise.resolve({
    id: 'sub_123'
   })),
  },
  checkout: {
   sessions: {
    create: jest.fn(() => Promise.resolve({
     id: '123'
    })),
   },
  },
 }));
});
```

嘲讽完 stripe 之后，让我们将测试用例写入 index.test.js 文件，并检查 create account API。

```
const request = require('supertest')
const app = require('../../app')
const client = request(app)
const urlPrefix = '/'
let tokendescribe('Create user profile', () => {
 it('should create user profile', async () => {
  const res = await client.post(`${urlPrefix}/create_account`)
   .send({
     email: "testuser@example.com",
     phoneNo: "787840255",
     firstName: "Test",
     lastName: "User",
    })
   expect(res.status).toEqual(200)
 })
})
```

当您运行上述测试文件时，您将收到客户的名称“Jest_User ”,而不是“Test User ”,因为您已经模仿了 Stripe API。

***感谢阅读。如果你喜欢这个帖子，请随意点击“鼓掌”按钮或发表评论。***

[*更多内容看 plainenglish.io*](http://plainenglish.io/)