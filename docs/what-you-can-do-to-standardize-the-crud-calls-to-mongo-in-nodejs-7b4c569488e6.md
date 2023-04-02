# 如何标准化 Node.js 中对 Mongo 的 CRUD 调用

> 原文：<https://javascript.plainenglish.io/what-you-can-do-to-standardize-the-crud-calls-to-mongo-in-nodejs-7b4c569488e6?source=collection_archive---------15----------------------->

## 关于从 Node 到 Mongo 的 CRUD 调用，有一些代码方面的标准化。这里是模式及其 CRUD 操作的简单展示，随后是建议的标准化方法以及最终的实现。如果您是 node 和 mongo 的新手，请尽可能多地使用它！

## 你的准则，你的标准

![](img/0c05bfb483b4703a80adaffd0833c657.png)

Image Credit: [Kelly Sikkema](https://unsplash.com/@kellysikkema)

# Node.js？

除了轻量级和开源的特性之外，Node.js 由于其效率、可伸缩性和社区支持而越来越受欢迎。它的跨平台运行时环境非常适合多平台应用程序开发。

此外，利用非阻塞 I/O 模式有助于提高流媒体服务和实时应用的可靠性。一些科技巨头如网飞、LinkedIn、Trello 和 PayPal 也对它的可靠性下了很大的赌注！

# MongoDB？

MongoDB 是一个文档数据库，其中的数据存储为文档的集合，而不是由外键关联的特定模式的表。凭借其高度的可伸缩性和灵活性，可以通过查询和索引功能轻松存储和访问各种类型的数据。

# 猫鼬

它是被设计用于异步运行时环境 [node.js](https://nodejs.org/en/) 的 [MongoDB](https://www.mongodb.org/) 对象建模工具。此外，它确实支持体面的承诺和回电行为。

```
npm install mongoose --S
```

## 看一看我们的模型模式

> 请详细说明{versionKey : false}的设置。
> 文档将不再被版本化，这里的[将告诉您结果。](https://stackoverflow.com/questions/12495891/what-is-the-v-field-in-mongoose/31872302#31872302)

Currency Model Schema

# 样本污垢

```
const **Currency** = require("../models/Currency");
```

## 创建:

```
var data = {name: "United State Dollar", code: "USD", rate: 1}
await new **Currency**(data).save();
```

## 阅读:

```
var code = "USD"
var name = "United States Dollar"// Find One
await **Currency**.findOne({ code })
await **Currency**.findOne({ name, code });// Find All
await **Currency**.find({})
await **Currency**.find({}).**sort**({ createdAt: "desc" });
```

## 更新:

```
var options = { useFindAndModify: false, new: true };
var query = { code: "USD" }
var payload = { name: "United States Dollar" }await **Currency**.findOneAndUpdate(**query, payload, options**);
```

## 删除:

```
await **Currency**.deleteOne( { "code" : "USD" } );
```

# 下一步是什么？

*   同一个罩下的多种型号管理
*   MongoDB 的错误处理
*   接下来，看看 [js 变量全球化](https://seanpang.medium.com/globalize-variables-in-nodejs-application-f782f52deffe)。

## 引擎盖下:多模型管理

```
// mongo_db_utils.jsconst moment = require("moment"); /* Models*/
const User = require("../models/User");
const Shop = require("../models/Shop");
const Currency = require("../models/Currency");
const Listing = require("../models/Listing");const **DbModel** = {
  User: User,
  Shop: Shop,
  Listing: Listing,
  Currency: Currency
};const mod_db = {
  **dbGetAll**: async function(table, params) {
    return params
    ? await DbModel[table].find(params).sort({ createdAt: "desc" })
    : await DbModel[table].find({}).sort({ createdAt: "desc" });
  },
  **dbGet**: async function(table, key) {
    return await DbModel[table].findById(key);
  },
  **dbGetOne**: async function(table, params) {
    return await DbModel[table].findOne(params);
  },
  **dbCreate**: async function(table, params) { 
    return await new DbModel[table](params).save();
  },
  **dbUpdate**: async function(params) {
    const options = { useFindAndModify: false, new: true };
    const { table, query, payload } = params;
    return 
      await DbModel[table].findOneAndUpdate(query,payload,options);
  }
};**module.exports = mod_db;**
```

> 示例用法:
> **dbGetOne** 从我们的 **mod_db 模块**导入，如上图所示，分别输入**型号名称**和**有效载荷**。

```
const db = require("./helper/mongo_db_utils");......**await** db.**dbGetOne**("Currency", { code });**await** db.**dbGetOne**("User", { name });
**await** db.**dbGetOne**("Listing", { id });
```

## MongoDB 创建和更新的错误处理

```
const **errorHandler** = (mongoError) => {
  let computedErrors = [];
  if (!is_empty(mongoError["reason"])) {
    const { **kind, value, path** } = mongoError;
    computedErrors.push(**`Field: ${path}, expected *${kind}*; receive'${value}'`**);
  }if (!is_empty(mongoError["errors"])) {
   for (var field in mongoError["errors"]) {
     const { **message, kind, path, value** } = mongoError["errors"][field];
    computedErrors.push(**`${message} (Field: ${path}, expected *${kind}*; receive '${value})'`**);
    }
  }
  return **computedErrors.join(", ")** }...
... const **mod_db** = {
  **...
  ...** **dbCreate**: async function(table, params) {
    let err = await new DbModel[table](params)
        .validate()
        .catch(errors => errors);
    if (err) {
      result["error"] = **errorHandler**(err);
    } else {
      result["data"] = **await new DbModel[table](params).save();
**    } return **result**;
  },
  ...
  ...};**module.exports = mod_db;**
```

## 完整的模块内容如下所示:

mongo_db_utils.js

# JavaScript 变量全球化

轻量级 JS 模块非常适合作为项目中的助手。然而，当在项目中跨区域需要该模块时，可能会出现代码冗余，并且我们确实在每次需要时手动导入它们。

接下来的标准化是，使函数 **dbGetAll** 、 **dbGetOne** 、 **dbCreate、**和 **dbUpdate** 全局可达。

对于那些错过了这一点的人，您可以找到 [**相关文章**](https://seanpang.medium.com/globalize-variables-in-nodejs-application-f782f52deffe) 来解释 Node.js 中全球化变量的实现。

# 结论

代码的标准化在不同的开发人员之间会有所不同。然而，我们都在寻求代码的可维护性和可伸缩性。因此，来自上面的分享发生了！*如果这对你有一点帮助，一定要在评论里让我知道！*