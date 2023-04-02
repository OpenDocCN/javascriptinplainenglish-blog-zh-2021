# 连续交易

> 原文：<https://javascript.plainenglish.io/sequelize-transactions-4ca7b6491e86?source=collection_archive---------4----------------------->

![](img/8b65810559b6b8e6ab62fa888dc4d3b4.png)

Sequelize transactions

原子事务是关系数据库的支柱。像 MySQL 或 Postgres 这样的符合 ACID 的数据库在事务的帮助下提供了一些非常重要的数据完整性属性。这实质上意味着在单个事务范围内执行的所有语句要么全部成功执行，要么整个块被回滚。

在我之前的两篇文章中，我们已经了解了顺序化和[顺序化关联](/four-sequelize-associations-you-should-know-415d8d413e1e)的[基础。在这最后一篇文章中，我们将学习 Sequelize 中的事务。](/save-time-learn-sequelize-in-7-mins-part-1-3e4fde67d037)

Sequelize 支持两种使用事务的方式:

1.  非托管事务
2.  托管交易

**非托管事务:**
事务的提交和回滚应该由用户通过调用 Sequelize transaction . commit()&transaction . roll back()方法手动完成。

```
const transaction = await models.sequelize.transaction();  
try {    
 const user = await models.User.create({
     firstName: 'Bart',
     lastName: 'Simpson'
   }, {
    transaction
   });
 const account = await models.Account.create({
  uId: user.uId,
  accountType: 'Free'
 }, {
   transaction
 })
 await transaction.commit();  
} catch (error) {    
  await transaction.rollback();
}
```

在上面的非托管事务示例中，首先创建一个用户实体&然后应该创建一个帐户条目。用户需要通过调用 commit()手动提交事务&如果出现任何错误，使用 roll back()回滚事务。

**托管事务** :
如果抛出任何错误，Sequelize 将自动回滚事务，否则提交事务。

```
// Example of managed transaction code
try {    
 const result = await models.sequelize.transaction(async (t) => {
   const user = await models.User.create({
    firstName: 'Abraham',
    lastName: 'Lincoln'
   }, { 
     transaction: t 
   });
  const account = await models.Account.create({
    uId: user.uId,
    accountType: 'Free'
   }, {
    transaction: t
  });
  return user
 })
} catch (error) { 
   console.log(error)   
}
```

在上面的示例中，通过向生成事务对象“t”的`sequelize.transaction`传递回调来启动事务。Sequelize 执行回调，将`t`传递给它。如果回调抛出错误，Sequelize 将自动回滚事务&如果回调成功，Sequelize 将自动提交事务。

我们已经在三篇文章中讨论了几乎所有的主题。如果在 Sequelize 中需要任何帮助，请随时联系。

***感谢阅读。***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)