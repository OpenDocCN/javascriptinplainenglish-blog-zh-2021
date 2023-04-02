# TypeScript:使用“as 子句”的条件子类型

> 原文：<https://javascript.plainenglish.io/typescript-conditional-subtypes-using-as-clause-2dd9896d67dc?source=collection_archive---------11----------------------->

使用 Typescript 的映射类型和" *as 子句"*,有条件地创建子类型。

![](img/7ea2e56fa1e62720863374ef4af74f31.png)

Photo by [cottonbro](https://www.pexels.com/@cottonbro?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/boy-in-white-t-shirt-sitting-on-chair-in-front-of-computer-4709285/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

# 问题陈述

在一个项目中，我遇到了一个用例，我需要从一个父类型中派生出一个子类型，只包含预定义类型的键。

我们举个例子，假设我有一个名为 **Address 的类型。**

```
type **Address** = {
id: string,
name: string,
surname: string,
country: string,
state: string,
landmark: string,
pincode: number,
isHomeAddress: boolean,
isRentedAddress: boolean
}
```

所以，现在我想从上面的地址类型中创建一个子类型，它应该只包含 boolean 类型的键。

```
type **AddressBoolean** ={
isHomeAddress: boolean,
isRentedAddress: boolean
}
```

# **解决方案**

TypeScript *映射的类型*在解决这类问题时很方便，您可以通过转换给定的类型来创建新的类型。

现在回到解决我们的问题。

因此，我们的父类型为:

```
type **Address** = {
id: string,
name: string,
surname: string,
country: string,
state: string,
landmark: string,
pincode: number,
isHomeAddress: boolean,
isRentedAddress: boolean,
}
```

我们的预期结果应该是

```
type **AddressBoolean** = {
isHomeAddress: boolean,
isRentedAddress: boolean,
}
```

让我们一步一步解决这个问题。

## **1)移除不需要的类型**

首先，我们会将地址中不需要的类型标记为 *never* type。

我们对它使用条件类型。

```
type **RequiredTypes<T, C>** = {
[Key in keyof T]: T[Key] extends C ? T[Key] : never
}
```

上面的代码将检查地址类型中的哪种类型扩展了条件(C)。它会将 *never* 类型分配给所有其他不符合我们条件的键。

> 永不*类型是永不不能有任何值的类型。与 typescript 的任何类型*相反，这意味着不能给它赋值。**

**用法**

```
type **MarkAsNever** = RequiredTypes<Address, boolean>
```

`MarkAsNever`类型看起来像这样

```
type **MarkAsNever** = {
Id: never,     
name: never,     
surname: never,     
country: never,     
state: never,     
landmark: never,     
pincode: never,     
isHomeAddress: boolean,     
isRentedAddress: boolean, 
}
```

如您所见，除了`isHomeAddress`和`isRentedAddress`之外，RequiredTypes 类型已经将“从不”分配给了地址的所有其他键。

## 2)删除 never 类型的键

现在我们到了最后一步，那就是移除没有*的类型。为此，我们将使用*作为 typescript 4.1 中引入的子句*。*

由于子句有一个很好的特性，你可以通过条件属性产生 never 来过滤掉密钥。

```
type **RemoveNeverField<T>** = { 
  [P in keyof T as T[P] extends never ? never : P]: T[P] 
};
```

在上面的代码中，我们循环遍历 T 的所有键，如果键的类型是 *never* ，我们的条件将返回 never，这将被 *as 子句自动忽略。*所以，到最后，我们只会拥有非 never 键。

**用法**

```
type **OnlyBoolean** = RemoveNeverField<onlyBoolean>
```

现在`OnlyBoolean`型会是下面这个样子。就像我们想要的那样。👌

```
type **OnlyBoolean** = {     
  isHomeAddress: boolean,     
  isRentedAddress: boolean, 
}
```

## 让我们总结一下所有需要的步骤

1

```
type **RequiredTypes<T, C>** = {   
   [Key in keyof T]: T[Key] extends C ? T[Key] : never 
}
```

2

```
type **RemoveNeverField<T>** = { 
  [P in keyof T as T[P] extends never ? never : P]: T[P] 
};
```

您可以进一步缩短语法。通过直接使用`RemoveNeverField`中的`RequiredTypes`代码，创建一个新的类型，比如说`PickByType`。

```
type **PickByType<T, C>** = RemoveNeverField<{ 
    [Key in keyof T]: T[Key] extends C ? T[Key] : never 
}>
```

**用法**

```
PickByType<Address, boolean>
```

此外，您可以利用联合(|)类型并忽略父类型地址中的多个类型。

```
type **PickTwo** = PickByType<Address, boolean | number>
```

在这种情况下，输出将是

```
type **PickTwo** = {
    pincode: number;
    isHomeAddress: boolean;
    isRentedAddress: boolean;
}
```

恭喜🎉我们已经创建了我们的类型，它可以基于作为条件提供的类型生成一个子类型。

我希望你今天学到了一些新东西。

*最初发表于*[https://async await . co/typescript-conditional-subtype-using-as-clause](https://asyncawait.co/typescript-conditional-subtypes-using-as-clause)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)