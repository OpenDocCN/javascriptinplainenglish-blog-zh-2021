# 7 个简单的 MongoDB/mongose 技巧让你的代码更快

> 原文：<https://javascript.plainenglish.io/7-simple-mongodb-tips-make-your-code-faster-and-optimize-f696211f1431?source=collection_archive---------1----------------------->

## 学习如何用几个技巧给你的 MongoDB 或 Mongoose 加电。

![](img/cd4f1dd1e08a70e3901b62d2dc86a774.png)

Photo by [Benjamin Sow](https://unsplash.com/@bensow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

去年圣诞节前后，我作为 MongoDB 的 NodeJS 开发人员开始了我的旅程。我知道一开始。我犯了很多菜鸟的错误，花了大量的时间在 StackOverflow 和 GitHub 中寻找合适的解决方案。经历了几次精疲力尽之后。我在 MongoDB 或 mongoose 中发现了一些小但非常有用的技巧。

# 1.精益()

当您在 mongose 中在结果之前执行任何查询时，mongose 会执行`hydrate()`一个模型函数，该函数用于从预先保存在 DB 中的现有原始数据创建一个新文档。返回的文档是 mongose`Document`类的一个实例，这个实例很重，因为它们有很多内部状态用于变更跟踪。`**lean()**` 从`hydrate()`函数中创建一个快捷方式，使查询速度更快，占用的内存更少，但是返回的文档是普通的旧 JavaScript 对象(POJOs)而不是 mongoose 文档。

```
*// Module that estimates the size of an object in memory*
**const sizeof = require('object-sizeof');**

**const normalDoc = await MyModel.findOne();**
*// To enable the `lean` option for a query, use the `lean()` function.*
**const leanDoc = await MyModel.findOne().lean();**

**sizeof(normalDoc);** *// >= 1000*
**sizeof(leanDoc);** *// 86, 10x smaller!*
```

# 2.虚拟财产

我们中的一些人已经熟悉猫鼬虚拟财产。但是这里有些隐藏行为的虚拟。基本上，virtual 只是不存储在 MongoDB 中的 MongoDB 文档的计算属性。

假设有两个字符串属性:firstName 和 lastName。您可以创建一个虚拟属性 fullName，让您可以同时设置这两个属性。

```
**const** **userSchema = mongoose.Schema({
  firstName: String,
  lastName: String
});***// Create a virtual property `fullName`.*
**userSchema.virtual('fullName').get(function() {
  return `${this.firstName} $(this.lastName}`;
});
const User = mongoose.model('User', userSchema);

let doc = await User.create({ firstName: 'Tim', lastName: 'Burton' });***// `fullName` is now a property on documents.*
**doc.fullName;** *// 'Tim Burton'*
```

当您将文档转换为 JSON 或 POJO 时，Mongoose 不包含 virtuals。如果你使用`.lean()`，那就意味着没有虚拟。例如，如果您将一个文档传递给[Express](http://expressjs.com/en/4x/api.html#res.json)函数，默认情况下会包含**而不是**。如果你想在`res.json()`中获得虚拟，只需将`toJSON`模式选项设置为`{virtuals: true}`。

```
**const** **userSchema = mongoose.Schema({
  firstName: String,
  lastName: String
}, { toJSON: {virtuals: true} });**
```

# 3.索引()

当我读到 MongoDB 索引功能时，我感到很惊讶。您可以将 MongoDB 索引与 SQL 索引进行比较，两者几乎相同。我们可以在路径级别或模式级别的模式中定义这些索引。创建复合索引时，必须在模式级别定义索引。

> *索引支持在 MongoDB 中高效执行查询。如果没有索引，MongoDB 必须执行集合扫描，即扫描集合中的每个文档，以选择那些匹配查询语句的文档。如果某个查询有合适的索引，MongoDB 可以使用索引来限制它必须检查的文档数量。*

```
**const userSchema= new Schema({
    name: String,
    email: { type: [String], index: true }** *// field level* **});

userSchema.index({ email: 1, name: -1 });** *// schema level*
```

***注意:*** *索引使用内存和磁盘上的临时文件的组合来完成索引构建，内存使用的默认限制是 200 兆字节(对于 4.2.3 和更高版本)和 500 兆字节(对于 4.2.2 和更低版本)。您可以通过设置* `[*maxIndexBuildMemoryUsageMegabytes*](https://docs.mongodb.com/manual/reference/parameters/#param.maxIndexBuildMemoryUsageMegabytes)` *服务器参数来覆盖内存限制。*

# 4.排序()

我知道 sort()函数在 MongoDB 中很常见，但是这里我要说的是给 sort()函数一些额外的功能。如果您知道默认的 sort()通过区分大小写的排序来给出结果。我猜很少有读者知道 MongoDB 中的`**collation**`****选项。`collation`允许用户指定特定语言的字符串比较规则，例如字母大小写和重音符号的规则。****

```
****User.find().collation({locale:'en',strength: 1}).sort({username:1})
    .then( (users) =>{** //do your stuff
 **});** // sort by username without case sensitivity.**UserSchema.index(
  {username:1}, 
  {collation: { locale: 'en', strength: 1}}
);** //index on username without case sensitivity.**
```

****在这里，`locale: 'en'`显示集合是英文的，`strength: 1`显示 collation 只对基本字符进行比较，忽略其他差异，比如音调符号和大小写。另外，`collation`还有几个 [**选项**](https://docs.mongodb.com/manual/reference/collation/#collation-document-fields) 你可以探索一下。****

# ****5.实例方法****

****在 MongoDB 中，文档基本上是真实模型的小实例。MongoDB 有丰富的内置实例方法。此外，MongoDB 提供了定制的文档实例方法。这些方法可以访问模型对象，并且可以非常有创造性地使用它们。****

```
**// Define `getFullName` instance method.
**userSchema.methods.getFullName = function() {
  return 'Mr.' + this.firstName+ ' ' + this.lastName
}**// This method accessible via a model instance.
**let model = new UserModel({
  firstName: 'Thomas',
  lastName: 'Anderson'
})****let initials = model.getFullName();
console.log(initials)** // This will output: Mr. Thomas Anderson**
```

******注意:** Do **not** 使用 ES6 箭头函数(`=>`)声明方法。箭头函数[显式地阻止绑定](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#No_binding_of_this) `this.`因此，你的方法**而不是**可以访问文档，上面的例子将不起作用。****

# ****6.静态方法****

****静态方法类似于实例方法，但区别只是`statics`是在模型上定义的方法，而`methods`是在文档(实例)上定义的。`statics`关键字定义了静态方法。让我们创建一个`getAllUser`静态方法来从数据库中获取所有用户数据。****

```
****userSchema.statics.getAllUsers = function() {
  return new Promise((resolve, reject) => {
    this.find((err, docs) => {
      if(err) {
        console.error(err)
        return reject(err)
      }
      resolve(docs)
    })
  })
}****
```

****使用`getAllUsers`静态，模型类通过调用这些静态从数据库返回所有用户数据。****

```
****UserModel.getAllUsers()
  .then(docs => {
    console.log(docs)
  })
  .catch(err => {
    console.error(err)
  })****
```

****在我的建议中，您应该使用`statics`方法，而不是多次重复相同的查询。添加实例和静态方法是在集合和记录上实现数据库交互接口的好方法。****

# ****7.中间件****

****中间件用于操作管道的特定阶段。Mongoose 有 4 种类型的中间件:文档中间件、模型中间件、聚合中间件和查询中间件。****

****例如，模型有带两个参数的`pre`和`post`函数:****

1.  ****事件的类型(“初始化”、“验证”、“保存”、“删除”)****
2.  ****用引用模型实例的 **this，** by 执行的回调。****

****让我们用邮箱和密码创建`userSchema`。****

```
****const userSchema= new Schema({
    email: {
      type: String,
      unique: true** *// `email` must be unique* **},
    password: String
  });****
```

## ****预挂钩:****

****如果你想保存密码总是加密格式。对于这一点，一个解决方案是你必须在保存之前手动加密密码，另一个解决方案是 mongoose 帮助你在存储到数据库之前加密你的密码字段。钩子将处理你的中间件逻辑。****

```
****userSchema.pre('save', function (next) {
  this.password =** **hashPassword(this.password)****;** // Replace with encrypted password // Call the next function in the pre-save chain **next(); 
})****
```

> ****如果任何预挂钩出错，mongoose 将不会执行后续的中间件或被挂钩的功能。Mongoose 将向回调传递一个错误和/或拒绝返回的承诺。****

## ****柱钩****

****Post hook 中间件运行在数据库和查询响应之间。这将有助于您在将查询结果发送到端点之前对其进行操作。我们再举一个例子。我们的`userSchema`说电子邮件字段是唯一的。但是当您试图保存已经存储在数据库中的电子邮件时，MongoDB 会发送一个错误，并且您的节点服务器会立即崩溃。您必须重新启动节点应用程序。****

****为了避免节点服务器崩溃，post 挂钩负责错误处理，并试图保持服务器运行。****

```
****userSchema.post('save', function(error, doc, next) {
  if (error.name === 'MongoError' && error.code === 11000) {
    next(new Error('There was a duplicate key error'));
  } else {
    next();
  }
});****
```

****![](img/ffed36b76af3261340e1fcaa12155924.png)****

****Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)****

# ****结论****

****现在，我敢肯定，现在没有人能低估你在 MongoDB 中的原始技能，也永远不要试图称你为这一领域的菜鸟。我只是试着涵盖那些对你方便的功能，让你的代码更快更优化。我们仅仅触及了 Mongoose 的一些功能。这是一个丰富的库，充满了有用和强大的功能。祝你编码愉快。****