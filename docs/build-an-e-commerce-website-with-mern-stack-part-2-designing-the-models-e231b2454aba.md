# 让我们建立一个 MERN 堆栈电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba?source=collection_archive---------2----------------------->

## 第 2 部分:设计模型

## 在第二部分中，我们将使用 Mongoose 设计所有需要的模型，通过我们的 Express 应用程序连接到 MongoDB 数据库。

![](img/ed190bc13c1e058e6f7ab3802d4efdb2.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们好！这是我们最近开始的 MERN 堆栈系列的第二部分。在第一部分，我们都学习了如何建立项目，并对项目中要用到的各种东西进行了解释。

如果你还没有读第一部分，这里有第一部分的链接

[](https://shubhamstudent5.medium.com/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [## 用 MERN 堆栈构建一个电子商务网站——第 1 部分(设置项目)

### 让我们使用 MERN 堆栈(MongoDB，Express，React 和 Node)建立一个简单的电子商务网站，用户可以在其中添加项目…

shubhamstudent5.medium.com](https://shubhamstudent5.medium.com/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) 

在第二部分中，我们将开始为我们的应用程序构建模型。我们使用 **MongoDB** 作为数据库来存储我们所有的数据。我们将使用**mongose**连接到 MongoDB 数据库，这将使我们的工作更容易构建数据库模式，然后基于该模式构建模型。

为了保持简洁，我们将在根文件夹中创建一个名为 ***models*** 的新文件夹。

然后，我们将在其中创建四个文件，分别代表我们的四个模型— **用户、商品、购物车**和**订单。**

> **注意:**我们不需要给我们的模式一个惟一的 id 参数，因为一旦我们在其中保存了任何文档，MongoDB 就会自动提供一个惟一的 ID。

因此，我们现在将逐一研究每个模型的细节。先说 ***用户*** 型号。

## 用户模型

因此，我们现在将创建我们的第一个模型——***用户*** 模型。这将定义存储用户数据的模型。我们将首先在之前创建的***‘models’***文件夹中创建一个 **User.js** 文件。

因此，我们将首先在我们的文件中要求*mongose*。我们还需要一个 ***isEmail*** 验证器，它来自我们在第一部分中安装的**【验证器】**依赖项。

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
const { isEmail } = require('validator');
```

然后我们继续从我们之前定义的**模式**中创建我们的 ***用户模式*** 。

```
const UserSchema = new Schema({
    name: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: [true,'Please enter an email'],
        unique: true,
        lowercase: true,
        validate: [isEmail, 'Please enter a valid email']
    },
    password: {
        type: String,
        required: [true, 'Please enter a valid password'],
        minlength: [6, 'Minimum password length must be 6 characters']
    },
    register_date: {
        type: Date,
        default: Date.now
    }
})
```

所以，在你看到了构建*用户模式的代码之后，*我们现在可以通过把它分解成小部分来讨论它，并且理解每件事是如何有意义的。

该模式中有各种字段，每个字段都有自己的类型和属性。这些是我们应用程序中的每个用户都会有的参数或字段。所以，让我们一个接一个地看看每一个领域

1.  **name** —它将包含使用我们应用程序的用户的姓名。这个字段将是字符串数据类型，因为它必须存储用户名。这是一个必填字段，在我们的应用程序中，每个用户都应该有一个名字。
2.  **电子邮件** —它将包含在我们网站注册的用户的电子邮件。它将再次成为字符串数据类型。我们希望电子邮件是独一无二的，所以我们把独一无二变成了真实。我们还想用小写存储电子邮件，所以我们把它设为 true。当然，电子邮件是必填字段，我们还附加了一个自定义错误消息，以便在没有提供电子邮件时触发。此外，我们检查提供的电子邮件地址是否实际上是电子邮件格式；为此，我们使用了之前需要的*isEmail* 验证器，并附上了一条定制的错误消息。
3.  **密码** —该字段用于存储用户的密码。它将是字符串数据类型，并且是每个用户的必填字段。我们还设置了最小长度限制，因此不允许密码短于该长度。我们也可以设置最大长度，但我们不在这里这样做。
4.  **register_date** —该字段存储用户首次在我们的网站上注册的日期。它默认为当前日期，因此用户不必明确提及。

> **注意:**我们不会以纯文本格式存储密码，因为如果有人入侵我们的数据库，密码很容易被破解。因此，为了安全起见，我们将使用 **bcrypt** 库来散列我们的密码，然后将散列后的密码保存在数据库中。我们将在控制器文件中进行哈希运算，而不是在模型文件中，但我仍然在这里提到了这一点，以便您以更好的方式理解它。当我们实际散列它时，我们将进入细节。

现在，既然我们已经构建了我们的*用户模式*，我们可以基于我们创建的模式构建**用户**模型。

```
module.exports = User = mongoose.model('user',UserSchema);
```

我们导出创建的*用户*模型，我们将这个集合称为*‘用户’*。因此，在数据库中，MongoDB 将对其进行复数化，并将集合名称保存为***‘users’。***

User Model

## 项目模型

我们需要创建的下一个模型是*项目*模型。在这里，我们将为商店中用户将要购买的商品设计模式。我们将保持我们的项目模式简单，不会包括*图像。你当然可以添加产品图片或任何你想添加的额外字段。*

但是对于这个系列，我们将只有这五个字段— **标题、描述、类别、价格和日期 _ 添加**。

我们将在 models 文件夹内名为 ***Item.js*** 的文件中构建我们的*项*模型。我们首先需要*mongose*并创建模式对象。

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
```

接下来，我们将开始设计我们的**项目模式**。它有五个字段，将建立在我们之前定义的模式之上。

```
const ItemSchema = new Schema({
    title: {
        type: String,
        required: true
    },
    description: {
        type: String,
        required: true
    },
    category:{
        type: String,
        required: true
    },
    price: {
        type: Number,
        required: true
    },
    date_added: {
        type: Date,
        default: Date.now
    },
});
```

这个模式中有五个字段，每个字段都有自己的类型和属性。这些将是我们的应用程序中的每一项都会有的参数或字段。所以，让我们一个接一个地看看每一个领域

1.  **标题** —存储我们商店中商品或产品的标题。它属于字符串数据类型，并且是必填字段。
2.  **描述** —存储物品或产品的详细信息或描述。它也是字符串数据类型，也是必填字段。
3.  **类别** —它存储我们商店中商品或产品的类别。它表示一个项目属于哪个类别。它也是字符串数据类型，并且是必填字段。
4.  **价格** —它存储我们商店中产品或物品的价格。它是数字数据类型，因为价格将以数字表示。这是一个必填字段，因为我们需要每个产品都有一个价格。
5.  **date_added** —存储商品或产品添加到我们商店的日期。它是自动设置的，因为我们将当前日期作为默认值。

现在，既然我们已经构建了我们的 *ItemSchema* ，我们可以基于我们创建的模式构建 **Item** 模型。

```
module.exports = Item = mongoose.model('item',ItemSchema);
```

我们导出创建的*项目*模型，我们将这个集合称为'*项目'*。因此，在数据库中，MongoDB 将对其进行复数化，并将集合名称保存为***‘items’。***

Item Model

## **推车型号**

我们将构建的下一个模型是购物车模型。这是我们在 web 应用程序中存储任何用户购物车的模型。购物车包含用户添加到购物车中的所有商品。

因此，我们的 ***CartSchema*** 将包含以下内容——userId、items 和总账单。

我们将在 models 文件夹内名为 ***Cart.js*** 的文件中构建我们的 *Cart* 模型。我们首先需要*mongose*并创建模式对象。

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
```

接下来，我们将开始设计我们的 **CartSchema** 。它有三个字段，将建立在我们之前定义的模式之上。

```
const CartSchema = new Schema({
    userId: {
        type: String,
    },
    items: [{
        productId: {
            type: String,
        },
        name: String,
        quantity: {
            type: Number,
            required: true,
            min: [1, 'Quantity can not be less then 1.'],
            deafult: 1
        },
        price: Number
    }],
    bill: {
        type: Number,
        required: true,
        default: 0
    }
});
```

这个模式有三个主字段和四个子字段(在 items 字段的内部)，每个字段都有自己的类型和属性。这些将是我们的应用程序中的每一项都会有的参数或字段。所以，让我们一个接一个地看看每一个领域

1.  **用户标识** —存储购物车所有者用户的唯一标识，即登录并向购物车添加物品的用户。我们将存储这些信息，以便为该特定用户识别正确的购物车。
2.  **项目**-该字段包含用户添加到其购物车中的所有项目。它将有各种子字段，如**产品标识** (添加到购物车中的产品或物品的唯一标识)、**名称**(添加的物品的名称)、**数量**(该物品在购物车中的添加数量，默认为 1，最小数量也只能是一个)和**价格**(添加到购物车中的物品的成本)。
3.  **清单** —该字段存储购物车中所有商品的总成本。它属于数字数据类型，并且是必填字段，当购物车为空时，默认值为 0。

现在，由于我们已经构建了 *CartSchema* 了，我们可以基于我们创建的模式构建 **Cart** 模型。

```
module.exports = Cart = mongoose.model('cart',CartSchema);
```

我们导出创建的 *Cart* 模型，我们将这个集合称为*【Cart】*。因此，在数据库中，MongoDB 将对其进行复数化，并将集合名称保存为***“cards”。***

Cart Model

## 订单模型

订单模型由我们应用程序中的所有用户订单组成。它的设计方式与 cart 模型非常相似，所有字段都与 Cart 模型相同，因为 Cart 项目将成为订单。

> **注意:**用户结账付款后，购物车中的所有商品都会转化为订单，购物车将被清空。

不过，订单模型有一个额外的字段。这个额外的字段是*添加的*字段，它将自动存储订单创建时的日期。

由于所有字段都与 Cart 模型相同，因此我们不再赘述了，因为这是多余的。

下面是 Order Model 文件的代码，我们将在名为 **Order.js** 的文件中创建该文件，该文件位于 *models* 文件夹中。

Order Model

所以，这就是我们应用程序中的所有模型。我们现在将结束第二部分，因为我们已经完成了在应用程序中使用的所有模型的构建。

在下一部分，我们将处理路由和控制器。此外，我们将在下一部分处理一些定制的中间件功能。

[](/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [## 让我们构建一个 MERN Stack 电子商务网络应用程序

### 第 3 部分:构建身份验证和项目路由及控制器

javascript.plainenglish.io](/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) 

如果你想访问这个项目的完整代码，请访问这个项目的 [GitHub 库](https://github.com/shubham1710/MERN-E-Commerce)。

希望你喜欢这部分教程。我希望你今天学到了新的有趣的东西。

如果你有任何建议或有任何疑问，请通过评论这篇文章让我知道。我很想得到你们所有人的反馈！

完成本系列后，还有更多的文章可供阅读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221) [## 使用 Django 构建一个社交媒体网站——设置项目(第 1 部分)

### 在第一部分中，我们集中在设置我们的项目和安装所需的组件，并设置密码…

towardsdatascience.com](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221)