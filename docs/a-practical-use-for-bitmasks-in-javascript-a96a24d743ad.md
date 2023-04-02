# JavaScript 中位掩码的实际应用

> 原文：<https://javascript.plainenglish.io/a-practical-use-for-bitmasks-in-javascript-a96a24d743ad?source=collection_archive---------3----------------------->

![](img/0406f2d551aac87ca42fc07c3c6f113a.png)

位掩码非常适合将多个真/假标志组合成一个值。

*在计算机科学中，掩码或位掩码是用于按位操作的数据，尤其是在位字段中。使用掩码，一个字节中的多个位可以在一次按位操作中设置为开、关或从开反转为关。*

在本文中，我将重点介绍如何使用位掩码来减少数据库中条目的大小。

使用[位操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#binary_bitwise_operators)来管理位掩码，这种操作符很少见，可能会让经验不足的开发人员感到困惑。ESLint 甚至有一个[默认设置](https://eslint.org/docs/rules/no-bitwise)来阻止你使用它们。使用的基本原理是位运算符看起来更像是错别字而不是实际特征。

但是，如果使用正确，它们会对数据库的大小、速度和可伸缩性产生巨大的影响，从长远来看，这可以为您节省大量资金。

我将展示一种使用位掩码来存储和管理用户状态的常用方法。

**型号**

状态中的每个值(除了 0)都是 2 的递增幂。2 的幂非常重要，因为每个值都代表二进制数中的一位。

您可以将状态值水平放置，最高值放在开始处，这样就可以直观地看到这一点。

```
TFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   0        |        0         |      0         |   0   |   0 
```

随着用户状态的改变，打开或关闭每个相应的位，并存储整数值。

**示例:仅启用双因素身份认证的活跃用户**

```
Bianry Visual LayoutTFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   1        |        0         |      0         |   0   |   1Users Tableid               status   
----------------|-----------1                17 -> 10001
```

我们在数据库中将状态存储为整数，但在应用程序中将其视为二进制数。

一个位掩码中最多可以存储 32 个真/假标志。如果需要添加另一个状态值，只需将其添加到枚举的末尾。您不必在数据库中添加另一列。

接下来，我将通过一些例子来说明如何管理位掩码值。

**创建用户**

首次创建用户时，只需设置活动状态。

```
const user: IUser = { status: Status.ACTIVE ...other user stuff
}db.set(user)
```

**存储值**

```
Bianry Visual LayoutTFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   0        |        0         |      0         |   0   |   1Users Tableid               status   
----------------|-----------1                1 -> 00001
```

**打开支付标志**

用户已经提供了他们的支付信息。要将一个位翻转到其开状态，使用`|=`操作符。

```
db.update({ status: (user.status |= Status.PAYMENT_VERIFIED) })
```

**存储值**

```
Bianry Visual LayoutTFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   0        |        1         |      0         |   0   |   1Users Tableid               status   
----------------|-----------1                9 -> 01001
```

**打开电子邮件验证标志**

用户已经验证了他们的电子邮件。使用与之前相同的`|=`操作符，只是改变状态值。

```
db.update({ status: (user.status |= Status.EMAIL_VERIFIED) })
```

**存储值**

```
Bianry Visual LayoutTFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   0        |        1         |      1         |   0   |   1Users Tableid               status   
----------------|-----------1                13 -> 01101
```

**关闭标志**

用户的付款方式已被删除。要翻转一点回到关闭状态，使用`&= ~`操作符。

```
db.update({ status: (user.status &= ~Status.PAYMENT_VERIFIED) })
```

**存储值**

```
Bianry Visual LayoutTFA_ENABLED | PAYMENT_VERIFIED | EMAIL_VERIFIED | ADMIN | ACTIVE 
-----------------------------------------------------------------
   0        |        0         |      1         |   0   |   1Users Tableid               status   
----------------|-----------1                5 -> 00101
```

**切换标志开/关**

或者，您可以用`^=`操作符打开或关闭一点

```
db.update({ status: (user.status ^= Status.PAYMENT_VERIFIED) })
```

**检查标志**

用户请求了一个只付费的功能。要检查它们的状态是否设置了 PAYMENT_VERIFIED 标志，请使用`&`操作符。

```
// helper function to check any flag
const isFlagSet = (actual: number, expected: number): boolean = { const flag = actual & expected; return flag === expected;};const user = db.users.find(id)const hasPayment = isFlagSet(user.status, Status.PAYMENT_VERIFIED)
```

我希望这些例子能帮助那些对在自己的应用程序中使用位掩码感兴趣的人。他们可能需要一点时间来适应，但好处是显而易见的。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。****