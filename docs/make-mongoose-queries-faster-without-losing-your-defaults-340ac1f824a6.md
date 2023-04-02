# 让 Mongoose 查询更快，而不丢失默认值

> 原文：<https://javascript.plainenglish.io/make-mongoose-queries-faster-without-losing-your-defaults-340ac1f824a6?source=collection_archive---------15----------------------->

## 如何在保持数据一致性的同时让查询速度更快

使用 Mongoose 在 Node.js 中与 MongoDB 交互时提供了许多优势。在构建、建模和存储应用程序的数据时，类型转换、验证、查询构建、业务逻辑挂钩、默认值都是必须的。Mongoose 提供了所有这一切，无需编写太多样板代码或使用多个库。

![](img/bc27d2b98f550405caa5a8411a389288.png)

Mongoose 通过为查询的每个结果文档添加大量魔法来实现这一点。这种*水合*将一个普通的旧 JavaScript 对象(POJOs)转换成一个奇妙而神奇的 Mongoose 文档。这是有代价的，因为 Mongoose 文档平均比 POJO 文档大 8 到 10 倍。

为了使我们的应用程序的性能尽可能快，我们需要尽可能有效和高效地查询我们的数据库。假设我们在一个查询中检索数千甚至数十万个文档，将每个文档缩小 10 倍将会在性能上获得巨大的提升。

![](img/b471a8cf33fb8ab30397a057cdfe1e6c.png)

Picture by [Vova Krasilnikov](https://www.pexels.com/es-es/@vovaflame?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

# 倾斜

Mongoose 的人已经考虑到了这一点，并为我们提供了一个简洁的解决方案，精益。Lean 跳过每个文档的水化，返回普通的旧 POJOs。

取以下猫鼬查询。

```
 const leanPerson = await Person.findOne()
```

使用精益的确非常简单。

```
const leanPerson = await Person.findOne().lean()
```

当精益传播到填充的文档时，它甚至与**填充**一起工作。

```
const leanPerson = await Person.findOne().lean().populate("interests")
```

完美！我们通过添加最少的代码极大地提高了查询性能。

# 维护默认值

扩展应用程序时，保持数据一致性至关重要。
尽管 MongoDB 允许我们以 JSON 对象的形式存储文档，但使用 Mongoose 的原因之一是它添加了验证和默认设置**之类的东西**。

为了在使用 **lean 的同时保持我们的默认值，**我们必须在定义我们的 mongose 模式时使用一个 NPM 包形式的漂亮的小插件，名为**mongose-lean-defaults**。

```
const mongooseLeanDefaults = require('mongoose-lean-defaults').defaultconst person = new mongoose.Schema({
  name: {
    type: String,
    default: 'Carlos',
  },
  language: {
    type: String,
    default: 'English',
  },
});

person.plugin(mongooseLeanDefaults);
```

然后只需在执行查询时添加 *defaults: true* 选项即可。

```
const carlos = await Person.findOne().lean({ defaults: true });
/**
 * carlos = {
 *    _id: ...,
 *    name: 'Carlos',
 *    language: 'English'
 * }
 */
```

现在你知道了。您现在可以查询数千个文档，同时保持数据一致性。

希望这篇小文章能帮助你把你的下一个应用从 100 个用户提升到 100，000 个用户。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)