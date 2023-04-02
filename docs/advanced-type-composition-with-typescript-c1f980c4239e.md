# 带打字稿的高级排版

> 原文：<https://javascript.plainenglish.io/advanced-type-composition-with-typescript-c1f980c4239e?source=collection_archive---------5----------------------->

使用泛型扩展 TypeScript 类型很容易，这是非常动态的，但是它是不可重用的，并且我们经常以代码重复而告终。让我们探索如何用 TypeScript 动态扩展类型来避免这种情况。

![](img/63a252732751deb92bc58679bf556164.png)

我们先定义一些实体及其关系。

我们有一个令牌实体，它有一个要约实体数组，要约实体有一个出价实体数组。

所以让我们为它们创建类型:

// *Token.ts*

```
*import* { TokenStatus } *from* '../enums/TokenStatus';

*export type Token* = {
  id: *string*;
  name: *string*;
  amount: *string*;
  metadata: *Record*<*string*, *string*>;
  status: TokenStatus;
  created_at: *string*;
};
```

// *Offer.ts*

```
*export type Offer* = {
  id: *string*;
  is_active: *boolean*;
  ends_at: *string*;
  created_at: *string*;
  is_auction: *boolean*;
};
```

// *投标文件*

```
*export type Bid* = {
  id: *string*;
  bided_on: *string*;
  amount: number;
  refunded: *boolean*;
  bid_is_highest: *boolean*;
};
```

将它们分开的原因是为了保持代码的整洁，但也是必要的，因为如果我们创建一个令牌，例如，该类型不包含 offers，一般来说，作为复杂类型的 offers 不应该是令牌实体的基本类型的一部分。

# **从基本类型中省略属性**

例如，如果我们想在代码中创建一个 CreateTokenPayload 类型，我们知道该类型没有令牌类型的 *id* 和 *created_at* 属性。所以姑且将 ***省略*** 它们*。*

```
*export type* CreateTokenPayload= Omit<Token, 'id'|'created_at'>
```

就是这样。🚀

# 从基本类型中选取属性

现在，如果创建令牌调用的响应只有 *id* 和*状态*字段，那也很容易，让我们只需**选择**字段。

```
*export type* CreateTokenResponse= Omit<Token, 'id'|'status'>
```

就是这样。🚀

但这不是这篇文章要讲的🤷‍♂️，这只是为了解释为什么我们要分开装箱。所以，让我们深入到作文。

为了向令牌类型添加“优惠”,我们需要扩展令牌类型。

```
export type TokenWithOffers = Token & { offers: Offer[] }
```

简单，但是…我们还需要报价类型中的“出价”。

```
export type OfferWithBids = Offer & { bids: Bid[] }
export type TokenWithOffers = Token & { offers: OfferWithBids[] }
```

简单，但是…有了这三种类型的事件，你可以注意到我们逻辑中的重复，它毕竟不是那么动态的。

# 用输入类型组合 util —

*目标是使接受**类型的 **util 类型**扩展，属性名**保存添加的类型，组合**类型。***

```
**export type With*<BaseType, ObjectKey *extends string*, ComposedType> = BaseType & { [k *in* ObjectKey]: ComposedType };*
```

*简单又好。😌*

*现在让我们来探索如何改善我们的`TokenWithOffers`类型。*

```
**export type TokenWithOffers* =
  *With*<*Token*, 'offers', *With*<*Offer*, 'bids', *Bid*>[]>[]; // 😳* 
```

*它的伟大之处在于它可以用于多种用例。假设我们想在使用`TokenWithOffers`类型时只给`Token`类型添加一个名为`isActive`的道具。*

```
**export type TokenWithOffers* =
  *With*<
    With<*Token, 'isActive', boolean>*,
    'offers', 
    *With*<*Offer*, 'bids', *Bid*>[]
  >[]; // 🤩* 
```

*因此，正如你所注意到的，我们使我们的代码可伸缩，并准备在未来扩展。👏*

**快乐编码！**

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*