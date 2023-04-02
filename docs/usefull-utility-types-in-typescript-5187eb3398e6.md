# TypeScript 中的 3 个实用程序类型

> 原文：<https://javascript.plainenglish.io/usefull-utility-types-in-typescript-5187eb3398e6?source=collection_archive---------12----------------------->

## 利用使用类型和静态分析的能力

TypeScript 就像服用了类固醇的 JavaScript。这主要归功于使用类型和静态分析的能力。所以我们来谈谈 TypeScript 中一些有用的实用工具类型。

![](img/6505966f7b144d937c616dbb676e6c83.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nubelsondev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.部分

***Partial<T>***是一个实用程序类型，它接受一个给定的类型并返回一个新类型，其中所有属性都是可选的。如果您需要在几个地方使用同一个接口，有些地方需要所有属性都是可选的，而有些地方不需要，那么这是非常有用的。例如，如果您有一个表示表单数据模型的界面，并且您在两个地方使用该表单，在一个地方它有必填字段，而在另一个地方所有字段都是可选的。为了便于阅读，我将使用简化的示例。

```
interface FormModel {
  email: string;
  name: string;
  surname: string;
} class FormWithRequiredFields {
  ... setFormValue(value: FormModel): void {
    ...
  } ...
}class FormWithOptionalField {
  ... setFormValue(value: Partial<FormModel>): void {
    ...
  } ...
}
```

所以在第一个类***FormWithRequiredFields***方法***【set form value】***中我们使用原来的 ***FormModel*** 接口，其中有****姓氏*** 作为可选属性， ***email*** 作为必需属性。对于第二类***FormWithOptionalFields***方法 ***setFormValue、*** 我们使用 ***FormModel*** 接口连同***Partial<T>***实用程序类型使其成为***Partial<form model>***。这使得接口 ***表单模型*** 的所有属性都是可选的。*

****局部< T >*** 在制作*补丁*请求时也非常有用。在这种情况下，我们可以采用原始接口，用于 *GET* 或 *POST* 请求，并使其所有属性可选。*

# *2.选择*

****Pick<T>***使我们能够指定给定类型的属性子集，通过声明我们想要的父类型的键。当我们知道我们需要来自父类型的一些键，而不需要其他键时，这可能是有用的。让我们回到我们的表单示例，如果我们有一个包含更多字段的更大的表单和另一个包含来自更大表单的字段子集的更小的表单，我们可以使用***Pick<T>***来只将该字段子集放入我们的表单数据模型。*

```
*interface FormModel {
  email: string;
  name: string;
  surname: string;
}class FormWithAllFields {
  ...setFormValue(value: FormModel): void {
    ...
  }...
}class FormWithNameAndSurnameFields {
  ...setFormValue(value: Pick<FormModel, 'name' | 'surname'>): void {
    ...
  }...
}*
```

*所以在第一个类***form with all fields***method***【set form value】***中我们使用了原来的 ***FormMode*** 接口，其中有一个 ***【姓名】*** 和 ***email*** 属性。对于第二类***formwithnameandsunamefields***方法 ***setFormValue*** 我们使用 ***FormModel*** 接口连同***Pick<T>***实用程序类型将其制作成 ***Pick < FormModel、【姓名】|>***。这使得一个新类型只带有 ***名*** 和 ***姓*** 属性的接口 ***FormModel*** 。*

*您可以通过编写 ***Pick < T、>*** 来获取一个属性，或者通过使用 union ***Pick < T、【prop 1】|【prop 2】|【prop 3】'>***来获取多个属性，就像我们在上面的示例中所做的那样。*

# *3.省略*

****省略< T >*** 行为方式与 ***挑< T >*** 相似，但相反。我们提供了不想在新类型中出现的父类型的键。这样，我们可以从示例表单类型中删除一些键。*

```
*interface FormModel {
  email: string;
  name: string;
  surname: string;
}class FormWithAllFields {
  ...setFormValue(value: FormModel): void {
    ...
  }...
}class FormWithNameAndSurnameFields {
  ...setFormValue(value: Omit<FormModel, 'email'>): void {
    ...
  }...
}*
```

*所以在第一个类***form with all fields***method***set form value、*** 中我们使用了原来的 ***FormMode*** 接口，其中有 ***name、*** 和 ***email*** 属性。对于第二类***formwithnameandsunamefields***方法 ***setFormValue*** 我们使用 ***FormModel*** 接口连同 ***省略< T >*** 实用程序类型使其成为 ***省略< FormModel、>* 这使得一个新的类型只有 ***名*** 和 ***姓*** 属性的接口***form model***。***

*定义属性名称与使用 ***Pick < T >*** 相同，您可以通过编写 ***省略< T、【prop’>***或使用 union ***Pick < T、【prop 1】|【prop 2】|【prop 3】>***来获取一个属性或多个属性。*

*如果你只需要从更大的集合中提取几个属性，你应该使用 ***选择< T >*** ，或者如果你需要保留其中的大部分，只移除一部分，你可以反过来省略< T > 。*

# *摘要*

*通过在代码中使用 TypeScript 实用工具类型，您可以获得更干净、更易于维护的类型。此外，对一个父类型所做的更改将反映在所有继承的父类型中，这些父类型使用实用程序类型。*

*喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！***

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*