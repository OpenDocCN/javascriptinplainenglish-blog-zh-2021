# 停止包装角形组件

> 原文：<https://javascript.plainenglish.io/stop-wrapping-angular-components-7d397c23a84c?source=collection_archive---------1----------------------->

![](img/166fa5ee5226fc4c38d8d66d8aff1922.png)

Image by [jacqueline macou](https://pixabay.com/users/jackmac34-483877/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=970943) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=970943)

*“我会反复使用这个配置相同的三十件组件，所以我应该包装它。”*

乍一看似乎是个好主意，但这是不必要的，需要大量的工作。

那么我们能做什么来代替包装呢？

**简单的答案是分层注入指令。**

我在 PrimeNG 上做例子(因为它是开源的、流行的和免费的)，但是下面的例子可以应用于通过组件和指令开发的每个 angular 组件集。

假设您有一个 employee 集合，您想将它绑定到一个选择输入中，并且您在多个组件/页面中使用这个输入。

如果你想在多个页面上使用员工下拉菜单，你有一些选择。

1.  **为每个有雇员下拉菜单的组件编写相同的代码。**

如果您将它用于两到三个页面，这不是一个大问题，但是在更多页面上使用它会导致将来可能遇到的简单逻辑需求的高成本。

**2。编写一个服务，为选择列表获取& maps 雇员。**

这可能是一个很好的解决方案，现在我们可以在一个文件中更改 get data 逻辑，这一更改可以应用于所有员工下拉列表。但是我们仍然需要为每次使用设置 p-dropdown 的配置。

```
<p-dropdown
  [options]="employees"
  placeholder="Choose an employee"
  [showClear]="true"
  [filter]="true"
 ></p-dropdown>
```

如果您编写测试，那么您必须创建 EmployeeService 的模拟/间谍，并为每种用法编写测试。

**3。用自定义组件包装组件(请不要这样做)**

这看起来像是完美的解决方案，但是需要做很多工作。您需要为其他开发人员创建文档，您应该支持您正在包装的组件的所有输入和输出。同样，如果你包装一个表单组件(就像例子一样)，你必须实现**ControlValueAccessor**接口。

**4。创建一个操作组件属性的指令**

通过这种方式，您可以多次使用 employee dropdown，无需重新编写相同的代码/参数，您可以更改默认配置值，并且如果您更新了 PrimeNG 库，您无需做任何事情即可支持<p-dropdown>的新输入/输出。</p-dropdown>

*更多内容看* [***说白了. io***](http://plainenglish.io/)