# 使用 bcrypt、Sequelize 和 Node.js 进行密码加密

> 原文：<https://javascript.plainenglish.io/password-encryption-using-bcrypt-sequelize-and-nodejs-fb9198634ee7?source=collection_archive---------3----------------------->

这篇文章讲述了如何使用 Sequelize 加密用户密码并存储在 PostgreSQL 中。

![](img/f9bd1547634a425020a70b8511a8f41b.png)

Architecture Diagram ( IMG 1 )

## 通过 NPM 安装

```
npm install bcrypt
npm install sequelize
```

## 与顺序模型一起使用

```
const bcrypt = require('bcrypt');var userSchema = sequelize.define("users", {
 userId: {
  field: 'user_id',
  autoIncrement: true,
  primaryKey: true,
  type: Sequelize.INTEGER
},
 password: {
  field: 'user_password',
  type: Sequelize.STRING,
  allowNull: true
 },
 name: {
  type: Sequelize.STRING,
  field: 'user_name',
  allowNull: false
 },
 email: {
  type: Sequelize.STRING,
  field: 'user_email',
  allowNull: false
 },
},
{
 hooks: {
  beforeCreate: async (user) => {
   if (user.password) {
    const salt = await bcrypt.genSaltSync(10, 'a');
    user.password = bcrypt.hashSync(user.password, salt);
   }
  },
  beforeUpdate:async (user) => {
   if (user.password) {
    const salt = await bcrypt.genSaltSync(10, 'a');
    user.password = bcrypt.hashSync(user.password, salt);
   }
  }
 },
 instanceMethods: {
  validPassword: (password) => {
   return bcrypt.compareSync(password, this.password);
  }
 }
});
userSchema.prototype.validPassword = async (password, hash) => {
 return await bcrypt.compareSync(password, hash);
}
 return userSchema;
}
```

***验证密码***

```
const authenticateUserWithemail = (user) => {
 return new Promise((resolve, reject) => {
  try {
   usermodel.findOne({
   where: {
    user_email: user.userName // user email
   }
   }).then(async (response) => {
    if (!response) {
     resolve(false);
    } else {
      if (!response.dataValues.password || 
       !await response.validPassword(user.password, 
        response.dataValues.password)) {
         resolve(false);
      } else {
       resolve(response.dataValues)
      }
     }
    })
   } catch (error) {
   const response = {
    status: 500,
    data: {},
   error: {
    message: "user match failed"
   }
   };
  reject(response);
  }
 })
}
```

## 序列模型

模型是序列的本质。模型是表示数据库中的表的抽象。在 Sequelize 中，它是一个扩展[模型](https://sequelize.org/master/class/lib/model.js~Model.html)的类。

该模型告诉 Sequelize 关于它所代表的实体的一些事情，例如数据库中的表的名称和它有哪些列(以及它们的数据类型)。

续集中的一个模特有名字。该名称不必与其在数据库中表示的表名相同。通常，模型有单数名称(如`User`)，而表格有复数名称(如`Users`)，尽管这是完全可配置的。

## 序列挂钩

钩子(也称为生命周期事件)是在 sequelize 中的调用执行之前和之后被调用的函数。例如，如果您想在保存模型之前总是设置一个值，您可以添加一个`beforeUpdate`钩子。

**注意:** *不能和实例一起使用钩子。钩子与模型一起使用。*

***创建前***

实体创建前初始化。

***更新前***

实体更新前初始化。

***钩子击发顺序***

下图显示了最常见钩子的触发顺序。

***注:*** *此列表并不详尽。*

```
(1)
  beforeBulkCreate(instances, options)
  beforeBulkDestroy(options)
  beforeBulkUpdate(options)
(2)
  beforeValidate(instance, options)[... validation happens ...](3)
  afterValidate(instance, options)
  validationFailed(instance, options, error)
(4)
  beforeCreate(instance, options)
  beforeDestroy(instance, options)
  beforeUpdate(instance, options)
  beforeSave(instance, options)
  beforeUpsert(values, options)[... creation/update/destruction happens ...](5)
  afterCreate(instance, options)
  afterDestroy(instance, options)
  afterUpdate(instance, options)
  afterSave(instance, options)
  afterUpsert(created, options)
(6)
  afterBulkCreate(instances, options)
  afterBulkDestroy(options)
  afterBulkUpdate(options)
```

***实例方法***

实例方法是在模型的*实例*上可用的方法。我们经常写这些来获取信息或者做一些与实例相关的事情。

***定义***

```
**const** Pug = db.define('pugs', {*/* etc*/*})*// instance methods are defined on the model's .prototype*
Pug.prototype.celebrateBirthday = **function** () {
  *// 'this' in an instance method refers to the instance itself*
  **const** birthday = **new** Date(**this**.birthday)
  **const** today = **new** Date()
  **if** (birthday.getMonth() === today.getMonth() && today.getDate() === birthday.getDate()) {
    console.log('Happy birthday!')
  }
}
```

***用法***

```
**const** createdPug = **await** Pug.create({name: 'Cody'}) *// let's say `birthday` defaults to today*
*// the instance method is invoked *on the instance**
createdPug.celebrateBirthday() *// Happy birthday!*
```

***类方法***

类方法是在*模型本身*(又名*类*)上可用的方法。我们经常写这些来获取实例，或者对多个实例做一些事情。

***定义***

```
**const** Pug = db.define('pugs', {*/* etc*/*})*// class methods are defined right on the model*
Pug.findPuppies = **function** () {
  *// 'this' refers directly back to the model (the capital "P" Pug)*
  **return** **this**.findAll({ *// could also be Pug.findAll*
    where: {
      age: {$lte: 1} *// find all pugs where age is less than or equal to 1*
    }
  })
}
```

***用法***

```
**const** foundPuppies = **await** Pug.findPuppies()
console.log('Here are the pups: ', foundPuppies)
```

***bcrypt***

是由[尼尔斯·普罗沃斯](https://en.wikipedia.org/wiki/Niels_Provos)和大卫·马齐埃设计的[密码散列函数](https://en.wikipedia.org/wiki/Password-hashing_function)，基于[河豚](https://en.wikipedia.org/wiki/Blowfish_(cipher))密码，并于 1999 年在 [USENIX](https://en.wikipedia.org/wiki/USENIX) 上展示。除了包含一个 [salt](https://en.wikipedia.org/wiki/Salt_(cryptography)) 来抵御 [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) 攻击之外，bcrypt 还是一个自适应函数:随着时间的推移，迭代次数可以增加以使它变得更慢，因此即使计算能力增加，它仍然可以抵抗[暴力搜索](https://en.wikipedia.org/wiki/Brute-force_search)攻击。

bcrypt 函数是默认密码[哈希算法](https://en.wikipedia.org/wiki/Hash_algorithm)用于 [OpenBSD](https://en.wikipedia.org/wiki/OpenBSD) 和其他系统，包括一些 [Linux 发行版](https://en.wikipedia.org/wiki/Linux_distribution)如 [SUSE Linux](https://en.wikipedia.org/wiki/SUSE_Linux) 。

***bcrypy API***

**genSaltSync(rounds，minor)**
**rounds** —【可选】—处理数据的开销。(默认值— 10)
**次要版本**—[可选] —要使用的 bcrypt 的次要版本。(默认— b)
**genSalt(rounds，minor，cb)**
**rounds** —【可选】—处理数据的开销。(默认值— 10)
**次要版本**—[可选] —要使用的 bcrypt 的次要版本。(default-b)
**CB**—[可选] —一旦生成 salt 就要触发的回调。使用 eio 使其异步。如果未指定 cb，则在承诺支持可用的情况下返回承诺。
**err** —回调的第一个参数，详细说明任何错误。
**salt** —提供生成的 salt 的回调的第二个参数。
**hashSync(数据，盐)**
**数据** —【必选】—要加密的数据。
**salt** —【必需】—用于散列密码的 salt。如果指定为一个数字，那么将生成一个具有指定轮数的盐并使用(参见用法下的示例)。
**hash(data，salt，cb)**
**data** —【必选】—要加密的数据。
**salt** —【必需】—用于散列密码的 salt。如果指定为一个数字，那么将生成一个具有指定轮数的盐并使用(参见用法下的示例)。
**CB**—[可选] —数据加密后将触发的回调。使用 eio 使其异步。如果未指定 cb，则在承诺支持可用的情况下返回承诺。
**err** —回调的第一个参数，详细说明任何错误。
**加密** —提供加密形式的回调的第二个参数。
**compareSync** (数据，加密)
**数据** —【必需】—要比较的数据。
**加密的** —【必需】—要比较的数据。
**compare(data，encrypted，cb)**
**data** —【必选】—要比较的数据。
**加密的** —【必需】—要比较的数据。
**CB**—[可选] —一旦数据被比较，将被触发的回调。使用 eio 使其异步。如果未指定 cb，则在承诺支持可用的情况下返回承诺。
**err** —回调的第一个参数，详细说明任何错误。
**same** —回调的第二个参数，提供数据和加密形式是否匹配[true | false]。
**get rounds(encrypted)**—返回用于加密给定哈希的轮数
**encrypted** —【必需】—从中提取轮数的哈希。

这个帖子到此为止。希望你觉得有帮助，感谢您的阅读。

[*更多内容看 plainenglish.io*](http://plainenglish.io/)