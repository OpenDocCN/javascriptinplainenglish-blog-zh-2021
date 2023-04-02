# 使用角度模板的另一种方法

> 原文：<https://javascript.plainenglish.io/an-alternative-way-to-use-angular-templates-97becc84e109?source=collection_archive---------9----------------------->

![](img/4c57cb51426451bb1839068f9a39a12f.png)

Image by [Free-Photos](https://pixabay.com/photos/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=768432) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=768432)

## **我寻找替代方式的动机**

当我第一次看 **ViewRef** 和 **NgTemplate** 的文档时，我有点困惑。这些工具允许您在 HTML 文件中使用回调机制。它很强大，但感觉很奇怪。

假设您有一个在自定义模板中列出给定数组的组件。

如果你用 JavaScript 思考，你的脑海中会出现以下几行。

但是当我在 HTML 中使用这个机制的时候，我感觉我做错了。因为 HTML 输出越来越难预测了。

来源可能是这样的。

```
<my-comp [template]="myTemplate"></my-comp>
  <p>
    Lorem ipsum dolar si amet...
  </p>
<ng-template #myTemplate>
 <div> This content will be bind in to my-comp.</div>
</ng-template>
```

输出变成这样。

```
<my-comp>
  <div> This content will be bind into my-comp.</div>
</my-comp>
<p>
   Lorem ipsum dolar si amet...
</p>
```

> 您可以在“我的合作伙伴”节点中定义模板，但您不能一直检查您的合作者。

## 这个想法来自 PrimeNG

PrimeNG 有一个很好的 API 来管理表格模板。

[PrimeNG 使用 ContentChildren decorator 获取 PrimeTemplate(pTemplate)指令，并将其映射到 NgAfterContentInit 函数中的属性。](https://github.com/primefaces/primeng/blob/7e61450022a5ab155167715cdc943125a5e34fbf/src/app/components/table/table.ts#L450)

这是一个很好的解决方案，但是没有提供一种方法来开发应该实现相同逻辑的其他组件。开发人员必须查看源代码，并且应该为每个组件实现相同的逻辑。

## 令我满意的解决方案

我决定用 PrimeNG 创建相同的 API，我只需要一种机制来确保所有团队成员以相同的方式实现使用模板的组件。我决定使用 Angular 用于表单管理的类似机制。

*   我创建了一个接口和注入标记来对每个使用模板的组件进行分组。
*   我创建了一个注入接口并调用所需函数来设置给定模板的指令。
*   我在使用模板的组件中实现并提供接口。

实现后，组件的用法如下。

```
<app-my-alternate-list [data]="employeeList">
 <ng-template appTemplate="item" let-employee="item">
  <img [src]="employee.image" width="200" height="200">           {{employee.name}} {{employee.lastName}}
 </ng-template>
 <ng-template appTemplate="empty">
  <div class="warning">No records found.</div>
 </ng-template>
</app-my-alternate-list>
```

**优点**

*   推动所有开发人员在组件节点中使用模板。
*   提供更可读的 HTML(至少对我来说)
*   也可以支持动态模板名。

**缺点**

*   **它不是棱角分明的方式**，需要编写文档，一些开发者可能会对此感到奇怪。
*   需要为使用模板的组件编写更多的代码(和更多的测试)。
*   可以认为是过度工程化。
*   防止(或使其难以)对不同的组件使用相同的模板。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)