# 让我们建立一个 MERN 堆栈电子商务网络应用程序

> 原文：<https://javascript.plainenglish.io/lets-build-a-mern-stack-e-commerce-web-app-accb4c14ce71?source=collection_archive---------1----------------------->

## 第 4 部分:构建购物车并订购路线和控制器

## 在第四部分中，我们将构建这个项目中处理购物车和订单所需的 REST APIs。我们将使用条纹结帐来处理支付。

![](img/2708c4abe9fe97f32cf576a75bcca98b.png)

Photo by [Roberto Cortese](https://unsplash.com/@robertocortese?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

朋友们好！这是我们最近开始的 MERN 堆栈系列的第四部分。在第一部分中，我们都学习了如何建立项目，并对项目中使用的各种东西进行了解释，在第二部分中，我们在 Mongoose 和 MongoDB 的帮助下开发了项目的所有模型。

在第三部分中，我们开始构建 REST APIs，它处理项目中的认证和项目。现在，在第四部分中，我们将通过构建 REST APIs 来处理 web 应用程序的购物车和订单方面，并使用 Stripe Checkout 来处理支付，从而结束我们的后端部分。

如果你还没有阅读前三部分，这里有前三部分的链接

[](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 1 部分:设置项目

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-1-setting-up-the-project-eecd710e2696) [](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 2 部分:设计模型

medium.com](https://medium.com/javascript-in-plain-english/build-an-e-commerce-website-with-mern-stack-part-2-designing-the-models-e231b2454aba) [](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 3 部分:构建身份验证和项目路由和控制器

medium.com](https://medium.com/javascript-in-plain-english/lets-build-a-mern-stack-e-commerce-web-app-d619f3374d73) 

因此，正如我们在上一部分中看到的，我们在根目录中创建了名为 *routes* 和 *controllers* 的文件夹。

我们还在这两个文件夹中创建了四个文件——分别代表**授权、商品、购物车**和**订单、**。

***注*** *:我们将在本教程中只处理与购物车和订单相关的路线和控制器，因为我们已经在前面的教程中处理了认证和项目。*

# 路线

## 购物车路线

该文件处理与我们的应用程序中的购物车相关的所有路线。它有三条路线——获取购物车商品、向购物车添加商品和从购物车中删除商品。

Cart Routes

因此，让我们逐一处理每一条路线

1.  **get_cart_items** —这个路由发出一个 *get* 请求，获取特定用户购物车中的所有商品。请求购物车的用户 id 作为参数传递。因此，我们找到用户的购物车并返回所有购物车商品。
2.  **add_cart_item** —这个路由发出一个 *post* 请求，向购物车中添加一个商品。它还有一个 param *id* 来标识哪个用户正在将商品添加到购物车中，因此我们可以找到他的购物车，并将商品添加到购物车中，或者为他创建一个新的购物车。
3.  **delete_item** —这是一个*删除*请求，它从购物车中删除一个商品。它接受两个参数——userId 和 itemId。userId 用于获取特定用户的购物车，itemId 用于搜索该商品并将其从购物车中删除。

## 订购路线

这个文件将处理我们处理订单所需的所有路线。它有两条路线——获取我们所有的订单和下订单(结账)。

所以，让我们逐一检查这两条路线

1.  **get_orders** —这是一个 *get* 请求，获取我们的应用程序中到目前为止所有的订单。它接受一个参数 *id* ，这是帮助我们返回正确的用户订单的用户 id。
2.  **checkout** —这是一个 *post* 请求，它还有一个用于查找用户的参数 *id* 。它的功能是创造一种新的秩序。这条路线处理所有的付款部分。我们将在它的控制器中看到这些。

# 控制器

## 推车控制器

这个控制器文件将处理购物车的所有逻辑。它将处理向购物车中添加商品，从购物车中删除商品，并使购物车商品与总费用一起显示。

这将由三个函数组成，每个函数对应我们拥有的三条路线，每条路线处理一个特定的目的。

因此，我们将详细讨论这三个功能。但是在此之前，我们需要这个文件中的购物车和商品模型。

```
const Cart = require('../models/Cart');
const Item = require('../models/Item');
```

我们的第一个任务是创建一个函数来获取购物车中的所有商品，并显示在应用程序的前端。

我们将获得想要访问其购物车的用户的用户 id。接下来，我们将尝试搜索具有该用户名的购物车。如果我们找到一个具有该用户名的购物车，并且购物车中有非零商品，*即*购物车非空，那么我们将返回购物车；否则，我们将返回 null。

*如果我们发送一个空值，我们也将在前端通过检查并通知用户购物车是空的来处理同样的问题。*

```
module.exports.get_cart_items = async (req,res) => {
    const userId = req.params.id;
    try{
        let cart = await Cart.findOne({userId});
        if(cart && cart.items.length>0){
            res.send(cart);
        }
        else{
            res.send(null);
        }
    }
    catch(err){
        console.log(err);
        res.status(500).send("Something went wrong");
    }
}
```

接下来，我们将处理向购物车添加商品。由于我们需要处理不止一个场景，这可能会更复杂一些。

在这个函数中，我们通过 params 接收 userId，还通过请求体接收 productId 和 quantity。这里，我们需要 userId 来访问相应用户的购物车，我们需要 productId 来查找要添加到购物车中的商品。

因此，我们将首先尝试使用我们获得的用户 Id 来查找购物车。现在，有两种情况——用户可能有购物车，也可能没有。

此外，我们在收到的 productId 的帮助下找到商品。如果找不到该项目，我们会发送一个声明相同的响应。

如果用户已经有一个购物车，那么我们搜索需要添加到购物车的商品中的商品，*，即*，如果该商品已经存在于购物车中。在这种情况下，我们从购物车中取出商品，按照我们收到的数量增加其数量，然后将更新后的商品分配给购物车。

如果商品不在购物车中，我们将它推入购物车的商品数组中。然后，我们在两种情况下更新购物车的账单，然后保存购物车。然后我们发送购物车作为响应。

在第二种情况下，如果用户还没有购物车，我们为用户创建一个新的购物车，包含用户 Id、需要添加的商品和账单。然后我们返回新的购物车作为响应。

```
module.exports.add_cart_item = async (req,res) => {
    const userId = req.params.id;
    const { productId, quantity } = req.body;

    try{
        let cart = await Cart.findOne({userId});
        let item = await Item.findOne({_id: productId});
        if(!item){
            res.status(404).send('Item not found!')
        }
        const price = item.price;
        const name = item.title;

        if(cart){
            // if cart exists for the user
            let itemIndex = cart.items.findIndex(p => p.productId == productId);

            // Check if product exists or not
            if(itemIndex > -1)
            {
                let productItem = cart.items[itemIndex];
                productItem.quantity += quantity;
                cart.items[itemIndex] = productItem;
            }
            else {
                cart.items.push({ productId, name, quantity, price });
            }
            cart.bill += quantity*price;
            cart = await cart.save();
            return res.status(201).send(cart);
        }
        else{
            // no cart exists, create one
            const newCart = await Cart.create({
                userId,
                items: [{ productId, name, quantity, price }],
                bill: quantity*price
            });
            return res.status(201).send(newCart);
        }       
    }
    catch (err) {
        console.log(err);
        res.status(500).send("Something went wrong");
    }
}
```

最后，我们转到与购物车相关的最后一个功能——从购物车中删除商品。

在这里，我们接收两个参数——userId 和 productId。我们尝试使用用户 Id 搜索购物车。我们还使用收到的 productId 搜索商品。

如果购物车中有商品，我们从购物车中取出该商品，并根据其价格和数量相应地减少账单。然后我们使用 *splice()* 函数从购物车中删除该商品。

接下来，我们保存购物车并将购物车作为响应返回给用户。

```
module.exports.delete_item = async (req,res) => {
    const userId = req.params.userId;
    const productId = req.params.itemId;
    try{
        let cart = await Cart.findOne({userId});
        let itemIndex = cart.items.findIndex(p => p.productId == productId);
        if(itemIndex > -1)
        {
            let productItem = cart.items[itemIndex];
            cart.bill -= productItem.quantity*productItem.price;
            cart.items.splice(itemIndex,1);
        }
        cart = await cart.save();
        return res.status(201).send(cart);
    }
    catch (err) {
        console.log(err);
        res.status(500).send("Something went wrong");
    }
}
```

因此，最后，我们已经构建了购物车路线所需的所有功能。我们已经准备好处理所有与购物车相关的请求。

Cart Controller

## 订单控制器

这个控制器文件将处理订单的所有逻辑。它将处理查看我们所有的订单，也将允许我们从我们的购物车中的项目下一个新订单，我们将通过条纹结帐处理付款。

这将由两个功能组成，一个用于我们拥有的两条路线，每个处理一个特定的目的。

在继续之前，我们需要将条带库安装到我们的应用程序中。

因此，为此，我们将使用`npm install stripe`来安装 stripe。它会将它作为一个依赖项保存在我们的 *package.json* 文件中。

此外，我们需要在配置文件中添加 *StripeAPIKey* 。因此，config 文件夹中更新后的 *default.json* 文件应该是:

```
{
    "dbURI": "YOUR DB URI",
    "jwtsecret": "your jwt secret",
    "StripeAPIKey": "YOUR STRIPE SECRET API KEY"
}
```

现在，我们需要在 orderControllers 文件中添加一些。我们需要导入订单、购物车和用户模型。我们还需要配置包来访问条带密钥。我们还需要在我们的函数中加入 Stripe，它将处理支付。

```
const Order = require('../models/order');
const Cart = require('../models/Cart');
const User = require('../models/User');
const config = require('config');
const stripe = require('stripe')(config.get('StripeAPIKey'));
```

因此，我们将从获取特定用户的所有订单所需的函数开始。这相当简单，我们需要使用参数提供的 userId 来查找订单。我们按照订购日期对它们进行降序排序，然后在 JSON 中将订单作为响应返回。

```
module.exports.get_orders = async (req,res) => {
    const userId = req.params.id;
    Order.find({userId}).sort({date:-1}).then(orders => res.json(orders));
}
```

接下来，我们有结帐功能。我们接收用户 Id 作为这个请求的参数。我们还从前端接收一个*源*作为请求体。这是通过 Stripe 处理支付。

现在，我们通过使用提供的 userId 找到购物车和用户。我们得到用户的电子邮件。

然后，我们检查购物车是否存在。如果没有购物车，我们发送一个响应，声明购物车是空的。

现在，我们使用条带创建一个*电荷*。我们传入金额、接收付款的货币、从前端接收的源对象和 receipt_email。

如果费用没有成功创建，我们会抛出一个错误，说明支付失败。

如果收费成功，我们将创建一个新的订单 userId、使用购物车的商品的商品和使用购物车的账单的账单。

然后，我们使用购物车的 id 删除购物车，然后将订单作为响应发送给前端。

```
module.exports.checkout = async (req,res) => {
    try{
        const userId = req.params.id;
        const {source} = req.body;
        let cart = await Cart.findOne({userId});
        let user = await User.findOne({_id: userId});
        const email = user.email;
        if(cart){
            const charge = await stripe.charges.create({
                amount: cart.bill,
                currency: 'inr',
                source: source,
                receipt_email: email
            })
            if(!charge) throw Error('Payment failed');
            if(charge){
                const order = await Order.create({
                    userId,
                    items: cart.items,
                    bill: cart.bill
                });
                const data = await Cart.findByIdAndDelete({_id:cart.id});
                return res.status(201).send(order);
            }
        }
        else{
            res.status(500).send("You do not have items in cart");
        }
    }
    catch(err){
        console.log(err);
        res.status(500).send("Something went wrong");
    }
}
```

Order Controller

# 结论

这就是第四部分的全部内容。我们最终总结了本系列的后端部分，现在将从下一篇教程开始，继续讨论客户端，即 React 和 Redux 代码。

[](/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd) [## 让我们建立一个 MERN 堆栈电子商务网络应用程序

### 第 5 部分:设置客户机和 Redux

javascript.plainenglish.io](/lets-build-a-mern-stack-e-commerce-web-app-444082ae81bd) 

如果你想访问这个项目的完整代码，请访问这个项目的 [GitHub 库](https://github.com/shubham1710/MERN-E-Commerce)。

我希望你今天学到了新的令人兴奋的东西。我希望你现在对深入研究项目的客户端部分感到兴奋。

完成本系列后，还有更多的文章可供阅读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e) [## 用 Django 构建求职门户——概述(第 1 部分)

### 让我们使用 Django 建立一个工作搜索门户，它允许招聘人员发布工作并接受候选人，同时…

towardsdatascience.com](https://towardsdatascience.com/build-a-job-search-portal-with-django-overview-part-1-bec74d3b6f4e)