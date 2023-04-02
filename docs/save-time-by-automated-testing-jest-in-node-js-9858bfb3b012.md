# 通过自动化测试节省时间:Jest in Node.js

> 原文：<https://javascript.plainenglish.io/save-time-by-automated-testing-jest-in-node-js-9858bfb3b012?source=collection_archive---------13----------------------->

![](img/c656c6fd992cb255db4df3ba326ca609.png)

Automated testing using Jest

Jest 是一个流行的 JavaScript 测试框架，用于应用程序的自动化测试。自动化测试有助于您在应用程序投入使用之前最大限度地减少程序中的错误。通过编写测试用例，您可以确保新添加的功能没有错误，并且不会影响您现有的功能。

这使得您的应用程序更加可靠、高效，同时也保证了应用程序的质量。未经测试的应用程序可能会在生产环境中导致灾难。在生产环境中识别 bug 也要困难得多。

在这篇文章中，我们将学习如何在 Node.js 项目中建立 Jest 测试框架，以及一些测试用例的例子。

## 步骤 1:设置 Jest 环境。

**1。**安装 jest 作为开发依赖项，因为我们在生产环境中不需要 jest。我们需要超级测试来测试我们的 Node.js HTTP 服务器。

```
npm i --save-dev jest supertest
Or 
yarn add --dev jest supertest
```

**2。**您总是可以在 package.json 文件中配置 jest，但是为 jest 所需的所有配置创建一个 jest.config.js 文件是一个很好的做法。

```
module.exports = {
 clearMocks: true,
 collectCoverage: true,
 coverageDirectory: 'coverage',
 coveragePathIgnorePatterns: [
  '/node_modules/',
  '/tests/',
  '/views/'
  '/keys/',
  '/public/',
  '/models/',
 ],
 globalSetup: './tests/setup.js',
 globalTeardown: './tests/teardown.js'
 setupFiles: [
  './tests/globalmocks.js',
 ],
 testEnvironment: 'node',
}
```

在上面的文件中，我们列出了一些配置属性，如:

**我**。clearMocks 用于指定是否在每次测试之间自动清除模拟调用和实例。

**二**。收集覆盖率指定在执行测试时是否应该收集覆盖率信息。

**三**。覆盖率目录指定 Jest 应该输出其覆盖率文件的目录。

**四**。coveragePathIgnorePatterns 指定用于跳过覆盖率收集的 regexp 模式字符串数组。

**v** 。全局设置指定模块的路径，该模块导出在所有测试套件之前触发一次的异步函数。

**六**。globalTeardown 指定一个模块的路径，该模块导出一个在所有测试套件之后触发一次的异步函数。

**七**。安装文件指定了在每次测试之前设置测试环境的路径。

**viii** 。测试环境指定了测试环境。
关于每个配置属性的详细说明，请访问[这里](https://jestjs.io/docs/en/configuration.html)。

**3。**现在在项目的根目录下创建一个 Tests 文件夹。这个文件夹将包含所有与你的测试用例相关的文件。

a.创建 setup.js 文件来初始化数据库连接。您可以将测试数据库植入到初始化的数据中。

```
const path = require('path')
const dotenv = require('dotenv')
dotenv.config({
 path: path.join(__dirname, '..', 'test.env'),
})const models = require('../models')module.exports = () => {
 return models.sequelize.authenticate()
 .then(()=> {
   return models.sequelize.query('SET FOREIGN_KEY_CHECKS = 0')
 })
 .then(() => {
   return models.sequelize.sync({
    force: true,
  })
 })
.then(()=> {
  return models.sequelize.query('SET FOREIGN_KEY_CHECKS = 1')
 }).then(() => {
   //seed you DB here
 })
}
module.exports.models = models
```

b.创建一个 teardown.js 文件来关闭数据库连接。

```
const path = require('path')
const dotenv = require('dotenv')
dotenv.config({
 path: path.join(__dirname, '..', 'test.env'),
})const models = require('../models')module.exports = async function () {
 await models.sequelize.close()
};
```

c.创建一个 globalmock.js 文件来模拟第三方服务函数。使用第三方服务和库是现代项目的常见部分。很难控制第三方服务的行为，为了解决这个问题，我们模仿第三方服务。模仿只是允许您用一组假的/固定的期望输出来替换实际的实现。我们将在这篇文章的后面模拟一些函数。

**4。**让我们在 Tests 文件夹中创建 Routes 文件夹来测试所有路由文件。所有的测试用例都应该有一个“test.js”或者“spec.js”的扩展名。jest 通过它识别测试文件。

a.创建一个 index.test.js 文件，写下 index.js 文件的所有测试用例。

```
const request = require('supertest')
const app = require('../../app')
const client = request(app)describe('index', () => {
 it('should show 200', async () => {
  const res = await client.get('/')
  expect(res.status).toBe(200)
 })
})
```

在上面的代码中，我们导入了 supertest，这将允许我们创建一个测试 node.js HTTP 服务器来测试所有的 CRUD API。初始化你的模拟应用服务器。

i. "Describe "创建一个块，将相关的测试用例组合在一起。这用于将与单个 API 相关的所有测试用例分组，就像将所有正面和负面测试用例分组在一起一样。它是完全可选的，你可以独立测试功能。

二。“It”函数执行 API 的实际测试。你也可以用“test”来代替它，两者是一样的。它以函数名和函数实现作为参数。

三。“expect”指定了期望通过测试用例的输出。例如，响应状态代码应该是 200。有各种各样的方法，你可以在这里阅读。

**5。**我们来为账户更新 API 写一套完整的测试用例。

```
const request = require('supertest')
const app = require('../../app')
const client = request(app)
const urlPrefix = '/user'describe('update User account Info', () => { it('should update user account info', async () => {
   const res = await client.put(`${urlPrefix}/account_info`)
    .set({
      authorization: token,
      Accept: 'json',
     })
    .send({
      uId: 2,
      emailId: "johnDoe@gmail.com",
      firstName: "John",
      lastName: "Doe",
      birthDate: "1996-02-02",
      height: 5.10Ft,
      weight: 80Kg,
      phoneNo: "+91-7777777777",
      metaData: {},
     })
    expect(res.status).not.toEqual(200)
  })it('should not update user info without id', async () => {
  const res = await client.put(`${urlPrefix}/account_info`)
    .set({
      authorization: token,
      Accept: 'json',
     })
    .send({
      emailId: "johnDoe@gmail.com",
      firstName: "John",
      lastName: "Doe",
      birthDate: "1996-02-02",
      height: 5.10Ft,
      weight: 80Kg,
      phoneNo: "+91-7777777777",
      metaData: {},
     })
    expect(res.status).not.toEqual(200)
  })it('should not update user info with wrong id', async () => {
  const res = await client.put(`${urlPrefix}/account_info`)
    .set({
      authorization: token,
      Accept: 'json',
     })
    .send({
      uId: 2000,
      emailId: "johnDoe@gmail.com",
      firstName: "John",
      lastName: "Doe",
      birthDate: "1996-02-02",
      height: 5.10Ft,
      weight: 80Kg,
      phoneNo: "+91-7777777777",
      metaData: {},
     })
    expect(res.status).not.toEqual(200)
  })
})
```

您可以进行所有 HTTP 调用，如 get、post、put、delete 等。您可以使用“set”方法设置标题。使用“Send”方法将数据作为主体参数传递。

```
// Mock Send email featurejest.mock('../email-helper.js')
const emailHelper = require('../email-helper')emailHelper.sendEmail.mockImplementation((fromEmail, toEmail, substitutions) => {
 if (emailHelper.fromEmail && emailHelper.toEmail) {
   return Promise.resolve({
    status: 200
   })
 } else {
   return Promise.reject(new Error("Email template dosen't exist"))
 }
});
```

在上面的代码中，我们模拟了 send email 函数，该函数使用 nodemailer 向用户发送电子邮件。您可以简单地模拟该函数，并在传递状态代码 200 时解决它。您可以模拟所有需要其输出的函数。在我们之前创建的 globalmock.js 文件中编写所有被模拟的函数。

**6。**要运行测试用例，请使用:

```
npx jest
```

就这样，你可以使用 describe 块编写 CRUD 的所有测试用例，以覆盖所有可能的场景，作为一个独立的测试用例。

在开发应用程序时编写测试用例可能很耗时，但有助于您在将来减少大量修复 bug 的时间。在将应用程序代码作为 CI/CD 管道的一部分移动到生产环境之前，您可以编写所有的测试用例并运行它们。

***感谢阅读。***

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)