# 让我们构建一个 MERN Stack 电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73?source=collection_archive---------0----------------------->

## 第 3 部分:构建身份验证和项目路由及控制器

在第三部分，我们将构建这个项目中身份验证和项目处理所需的 REST APIs。我们还将构建一些我们将在项目中使用的定制中间件功能。

![](img/f385d3cfaedd0fb115cfa76b49337302.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们，你们好！这是我们最近开始的 MERN 堆栈系列的第三部分。在第一部分，我们都学会了如何建立这个项目，并对我们将在这个项目中使用的各种东西进行了解释。在第二部分，我们在**猫鼬**和**猫鼬**的帮助下，为这个项目开发了我们所有的模型。

如果您尚未阅读前两部分，以下是前两部分的链接:-

[](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [## 让我们构建一个 MERN Stack 电子商务网络应用程序

### 第一部分:项目设置

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [## 让我们构建一个 MERN Stack 电子商务网络应用程序

### 第二部分:模型设计

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) 

现在，在第三部分，我们将构建后端部分，它将通过在 Express Router 的帮助下构建 API 来处理 web 应用程序中的身份验证和项目，我们还将定义一个定制的中间件功能来检查用户是否通过身份验证。

为了保持简单明了，我们会在根文件夹中创建一个名为 ***routes*** 的新文件夹。这个文件夹将包含我们这个项目需要的所有路线。

我们还将创建一个名为 ***控制器*** 的文件夹，一旦我们遇到一个应用编程接口端点，我们将在其中放置我们将要调用的所有函数。因此，我们会将该函数放在不同的文件夹中，然后将它们导入到 routes 文件夹中使用。

在*路线*文件夹中，我们会创建四个文件-**授权、项目、购物车**和**订单。**这四个文件分别包含与认证相关的路径、物品、购物车和订单。

同样，我们会在*控制器的*文件夹中创建四个文件，每个文件对应于*路由*文件夹中的一个文件。这些将分别是-**身份控制器、项目控制器、cart controller**和**订单控制器**。

因此，我们现在开始构建我们的 Routes 文件夹，这很简单，因为我们将把所有的逻辑放在*控制器的*文件夹中，而不是直接放在 *routes* 文件夹中。

> **注意**:本教程只处理与身份验证和项目相关的路由和控制器，下一教程将处理购物车和订单。

# 路线

## 授权路由

该文件将包含我们在 web 应用程序中验证用户身份所需的所有路由。

***当我们谈论认证时，您会想到什么？***

*注册用户，登录和注销。此外，我们需要不断检查用户当前是否登录。*

下面是我们将在应用程序中使用的身份验证路由的代码。首先，检查代码，然后我会详细解释代码中每一行的用途。

Auth Routes

所以，首先，我们从要求文件中的 *express* 的 ***路由器*** 开始。我们将使用快速路由器来建立所有的路由。我们还从控制器文件夹中引入了 *authControllers* ，并从中间件文件夹中引入了我们的定制中间件函数 *auth* 。我们稍后将构建这些文件。

然后，我们有三个路径— **注册、登录**和**用户。让我们来看看每一个是如何运作的。**

1.  **register** —这个路由处理一个 *post* 请求，在这个请求中，一个用户提供他的名字、电子邮件和密码，以便在我们的系统中注册。
2.  **登录** —这个路由处理网站的用户登录部分。它允许用户登录并检查凭证是否正确。
3.  **用户** —该路由是一个 *get* 请求，我们试图检索用户是否使用该路由登录。

> 注意:现在，你可能想知道我们错过了注销路径，但是我们不需要它。我们将使用**本地存储**来存储我们的 **JWT** 令牌，它在客户端处理它，所以我们将直接在客户端处理用户的注销。为此，我们不需要与服务器打交道。

## 项目路线

该文件包含与项目相关的所有路由—获取项目、添加新项目、更新项目和删除项目。所以，让我们先检查代码，然后再深入研究更多的细节。

Item Routes

它有四条路线。正如我们在上面看到的，它们各自处理特定的功能。

1.  **get_items** —这个路由是一个 *get* 请求，这个路由的目的是从服务器获取所有的项目。
2.  **post_item** —此路由是一个 *post* 请求，用于向数据库添加一个新项目。
3.  **update_item** —该路线是一个 *put* 请求。其目的是更新数据库中的现有项目。
4.  **delete_item** —该路由是一个 *delete* 请求，用于从数据库中删除一个项目。

> **注意** : delete_item 和 update_item 都有一个参数字段**‘id’**，它也是和 URL 一起传递的。它包含我们想要删除或更新的项目的 id。然后，我们使用 id 在数据库中搜索该商品。

# 控制器

## 授权控制器

这个控制器文件将处理注册、登录和获取用户的所有逻辑，以检查用户是否经过身份验证。

这将由三个函数组成，每个函数对应我们拥有的三条路线，每条路线处理一个特定的目的。

因此，我们将详细讨论这三个功能。但在此之前，我们需要在这个文件中要求一些东西。

```
const User = require('../models/User');
const jwt = require('jsonwebtoken');
const config = require('config');
const bcrypt = require('bcrypt');
```

如上所述，我们需要四样东西。让我们讨论一下每个人的责任

1.  **用户** —我们需要我们在之前的教程中创建的用户模型。既然我们要和用户打交道，我们就需要它。
2.  **jwt** —我们需要文件中的 *jsonwebtoken* 来创建 JSON Web 令牌，我们需要存储这些令牌来验证用户是否已经过身份验证。
3.  **config** —这是引入 config 包所必需的，以便我们访问存储在 config 文件夹中的 JSON。它能让我们储存 JWT 密码。
4.  **bcrypt** —在将密码保存到数据库之前，需要使用 bcrypt 库来散列密码。

现在，我们可以开始构建我们的函数了。所以，我们将从注册开始。

这是注册函数的代码，我们将其命名为*‘sign up’。*

```
module.exports.signup = (req,res) => {
    const { name, email, password } = req.body;

    if(!name || !email || !password){
        res.status(400).json({msg: 'Please enter all fields'});
    }

    User.findOne({email})
    .then(user => {
        if(user) return res.status(400).json({msg: 'User already exists'});

        const newUser = new User({ name, email, password });

        // Create salt and hash
        bcrypt.genSalt(10, (err, salt) => {
            bcrypt.hash(password, salt, (err, hash) => {
                if(err) throw err;
                newUser.password = hash;
                newUser.save()
                    .then(user => {
                        jwt.sign(
                            { id: user._id },
                            config.get('jwtsecret'),
                            { expiresIn: 3600 },
                            (err, token) => {
                                if(err) throw err;
                                res.json({
                                    token,
                                    user: {
                                        id: user._id,
                                        name: user.name,
                                        email: user.email
                                    }
                                });
                            }
                        )
                    });
            })
        })
    })
}
```

正如我们所看到的，在箭头函数中有一个请求和响应。首先，我们从请求体中分解出名称、电子邮件和密码字段，这些字段通过 API 请求传递给我们。

接下来，我们将检查任何字段是否为空；如果是，我们会发送一条消息，告诉用户填写所有字段。

然后，我们尝试使用提供的电子邮件来搜索用户。如果我们在数据库中找到使用该电子邮件的用户，我们会向用户返回一个响应，告诉他该电子邮件 id 已经存在于我们的系统中，用户应该使用不同的电子邮件或使用该电子邮件登录，而不是注册。

接下来，我们使用从请求主体收到的名称、电子邮件和密码创建一个新的用户实例。我们不会将它保存到数据库中，因为我们需要在保存之前对密码进行哈希运算。

接下来，我们生成一个 salt，然后使用该 salt 散列密码。然后，我们将散列值设置为密码，然后将 *newUser* 实例保存在数据库中。

在数据库中保存用户后，我们需要创建一个签名的 JWT 令牌，并将其存储在本地存储中。我们通过提供用户 id、JWT 秘密和到期时间来创建令牌。然后，我们发送令牌作为响应，同时发送不带密码的用户详细信息。

所以，这就是在我们的系统中注册一个新用户。

接下来，我们转到登录部分。它允许已经注册的用户登录我们的应用程序。

这是登录函数的代码，我们将其命名为*‘log in’。*

```
module.exports.login = async (req,res) => {
    const { email, password } = req.body;
    if(!email || !password){
        res.status(400).json({msg: 'Please enter all fields'});
    }
    User.findOne({email})
        .then(user => {
            if(!user) return res.status(400).json({msg: 'User does not exist'});

            // Validate password
            bcrypt.compare(password, user.password)
                .then(isMatch => {
                    if(!isMatch) return res.status(400).json({ msg: 'Invalid credentials'});

                    jwt.sign(
                        { id: user._id },
                        config.get('jwtsecret'),
                        { expiresIn: 3600 },
                        (err, token) => {
                            if(err) throw err;
                            res.json({
                                token,
                                user: {
                                    id: user._id,
                                    name: user.name,
                                    email: user.email
                                }
                            });
                        }
                    )
                })
        })
}
```

与注册类似，我们从解构请求体开始，从中获取电子邮件和密码值。

如果两者中的任何一个缺失，我们会向用户发送一条消息，说明他们需要输入电子邮件和密码。

然后，我们使用电子邮件 id 搜索用户。如果用户不存在，我们将向用户发送一个响应，声明该用户在数据库中不存在，他们应该在登录前首先注册。

接下来，我们将把提供的密码与数据库中的用户密码进行比较。您可能想知道我们将如何比较它们，因为我们在数据库中有散列密码。

因此，为了进行比较，我们需要使用 bcrypt 的 compare 函数。它获取提供的密码，然后对其进行哈希处理，并将其与数据库中保存的哈希密码进行比较。如果它们不匹配，我们将返回一条消息，声明凭据无效。

然后，我们以与注册函数中相同的方式创建一个签名的 JWT 令牌。然后，我们返回令牌以及用户的详细信息，但不提供密码。

接下来，我们将处理 *get_user* 函数。它通过 id 找到一个用户，然后返回不带密码的用户作为 JSON 响应。

```
module.exports.get_user = (req,res) => {
    User.findById(req.user.id)
        .select('-password')
        .then(user => res.json(user));
}
```

下面是身份验证控制器文件的完整代码。

Auth controllers

## 项目控制器

这个控制器文件将处理与项目相关的所有逻辑——添加项目、获取所有项目、删除项目或修改项目。

这将由四个函数组成，我们拥有的四条路线各有一个函数，每个函数处理一个特定的目的。

因此，我们将详细讨论这四个功能中的每一个。我们只需要这个文件中的项目模型。

```
const Item = require('../models/Item');
```

现在，我们将从从数据库中获取所有项目的函数开始。我们将得到所有的项目，并按添加日期降序排列。然后，我们以 JSON 格式返回这些项目。

```
module.exports.get_items = (req,res) => {
    Item.find().sort({date:-1}).then(items => res.json(items));
}
```

接下来，我们将处理向购物车添加新商品。我们将使用请求体作为新条目的输入，因为我们从前端发送请求体，格式与我们的模型相同。我们可以解构请求体，然后在为用户创建新项目时提供数据，但这是一种更干净的方式。

然后，我们将项目保存在数据库中，并以 JSON 格式发送新项目作为响应。

```
module.exports.post_item = (req,res) => {
    const newItem = new Item(req.body);
    newItem.save().then(item => res.json(item));
}
```

接下来，我们将处理更新项目。我们通过请求体接收更新的信息，通过参数接收条目 id。我们将使用函数 *findByIdAndUpdate* 来搜索商品，并用新信息更新它。然后，我们发送更新的项目作为响应。

```
module.exports.update_item = (req,res) => {
    Item.findByIdAndUpdate({_id: req.params.id},req.body).then(function(item){
        Item.findOne({_id: req.params.id}).then(function(item){
            res.json(item);
        });
    });
}
```

最后，我们处理从数据库中删除项目。我们通过参数接收商品 id。接下来，我们找到该项目，并使用 *findByIdAndDelete* 函数删除它。然后我们返回一个成功的响应。

```
module.exports.delete_item = (req,res) => {
    Item.findByIdAndDelete({_id: req.params.id}).then(function(item){
        res.json({success: true});
    });
}
```

这将总结我们的项目控制器部分。这是项目控制器的完整代码。

Item Controller

接下来，我们将处理一个定制的中间件函数来验证用户是否登录。

我们首先需要文件中的配置和 jwt。然后，我们开始制作认证中间件功能。

我们从名为*‘x-auth-token’的请求头部分获得令牌。*如果没有令牌，那么我们将验证令牌，然后发送解码后的变量作为响应。

然后我们使用 *next()* 函数，它允许我们继续下一个中间件函数。

Auth middleware function

这就是关于中间件功能的全部内容。我们已经涵盖了第三部分想要涵盖的所有内容。在第四部分，我们将处理购物车和订单的路线和控制器。在本系列的下一部分中，我们将使用 Stripe Checkout 来处理支付。

[](/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 4 部分:构建购物车并订购路线和控制器

javascript.plainenglish.io](/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71) 

如果你想访问这个项目的完整代码，请访问这个项目的 [GitHub 库](https://github.com/shubham1710/MERN-E-Commerce)。

谢谢大家阅读这篇文章。希望你今天获得了一些真正的知识，学到了一些新东西。

完成本系列后，还有更多的文章可供阅读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221) [## 使用 Django 构建一个社交媒体网站——设置项目(第 1 部分)

### 在第一部分中，我们集中在设置我们的项目和安装所需的组件，并设置密码…

towardsdatascience.com](https://towardsdatascience.com/build-a-social-media-website-using-django-setup-the-project-part-1-6e1932c9f221)