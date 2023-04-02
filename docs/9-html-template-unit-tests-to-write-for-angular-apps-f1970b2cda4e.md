# Angular 应用程序的 9 个 HTML 模板单元测试

> 原文：<https://javascript.plainenglish.io/9-html-template-unit-tests-to-write-for-angular-apps-f1970b2cda4e?source=collection_archive---------2----------------------->

## 了解一些可以用 Jasmine 编写的单元测试，以覆盖 Angular 应用程序的 HTML 模板

![](img/beb16c50b78d5e4a2807c3aac1569624.png)

Photo by [**Negative Space**](https://www.pexels.com/@negativespace?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [**Pexels**](https://www.pexels.com/photo/grayscale-photo-of-computer-laptop-near-white-notebook-and-ceramic-mug-on-table-169573/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

在本文中，我将分享 9 个不同的单元测试，你可以用 Jasmine 为你的 HTML 模板编写。

**更新:如果你想了解更多关于为你的 HTML 模板编写单元测试的知识，请查看我在** [**Udemy**](https://www.udemy.com/course/unit-testing-angular-9-with-jasmine-html-templates/?couponCode=97A89C11964B3C318DAA) **上的课程。你可以在短时间内免费得到它，所以趁它还在，现在就去买吧！**

## 内容

1.  [**测试组件显示在**](#6e1b) 界面中
2.  [**测试文本显示在**](#1b68) 界面中
3.  [**测试*ngIfs**](#b9cf)
4.  [**测试*ngFors**](#6360)
5.  [**测试【ng class】**](#58f7)
6.  [**测试子组件输出**](#285c)
7.  [**测试子组件输入**](#9cec)
8.  [**测试用户输入和文本区域**](#2362)
9.  [**测试第三方组件**](#bf1c)

你可以在 [GitHub repo](https://github.com/s3nt1n3lz21/ExampleAngularApp/tree/main/example-angular-app) 上找到与本文相关的所有代码。

## 1.测试组件显示在用户界面中

您可以编写的最简单的测试是检查组件当前是否显示在 UI 中。为此，我们需要从 UI 中获取元素，有几种不同的方法可以做到这一点。这些都列在下表中。

## query()和 queryAll()

我们获取 HTML 元素的第一种方法是使用`**query()**`和`**queryAll()**`函数。`**query()**` 将返回第一个匹配元素，`**queryAll()**`将返回所有匹配元素。这些函数返回一个对元素的非静态引用，这意味着当 UI 更新时，元素也会更新。

您可以通过元素的 id、元素的类或元素的选择器来查找元素。您在`**query()**`中使用函数`**By.css()**`，然后传入您想要的元素的 id、类或选择器。

*   **选择器** : `**query(By.css('div'))**`传入你想要的元素的选择器，比如`**<div></div>**`的选择器是`**div**` **。**
*   **Id** : `**query(By.css('#title'))**` 你需要包含一个哈希`**#**`
*   **类** : `**query(By.css('.title'))**`你需要包含一个点`**.**`

这些函数返回一个类型为`**DebugElement**`的对象，您可以通过使用`**.nativeElement**`来访问 HTML 元素。

*   **HTML 元素** : `**query(By.css('#title')).nativeElement**`

您还可以使用`**.componentInstance**`获得对 Typescript 组件的引用。然后，您可以检查组件上字段的值。

*   **打字稿组件** : `**query(By.css('#title')).componentInstance**`

## 使用 query()抓取元素

## 使用 queryAll()抓取元素

## querySelector()和 querySelectorAll()

您也可以使用`**debugElement.nativeElement**`上的`**querySelector()**`和`**querySelectorAll()**`功能。这些函数返回元素的静态副本，这意味着元素不会在 UI 更新时更新。

您还可以使用这些函数通过元素的 id、元素的类或元素的选择器来搜索元素。

*   **选择器** : `**querySelector('div')**`传入你想要的元素的选择器，比如`**<div></div>**`的选择器是`**div**` **。**
*   **Id** : `**querySelector('#title')**` 你需要包含一个哈希`**#**`
*   **类** : `**querySelector('.title')**`你需要包含一个点`**.**`

这些函数返回一个类型为`**Element**`或`**NodeList**`的对象。这些就像原生元素，所以你不必使用`**.nativeInstance**`。但这也意味着您无法获得对 typescript 组件的引用。

大多数时候可以用`**querySelector()**`和`**querySelectorAll()**`。如果需要访问`**.componentInstance**`，只需使用`**query()**`和`**queryAll()**`。

## **使用 querySelector()抓取元素**

## **使用 querySelectorAll()抓取元素**

## 2.测试文本显示在用户界面中

您可以检查某些特定文本是否显示在 UI 中。假设我们有下面的 HTML 模板显示“欢迎回来！”消息。

我们可以使用任何不同的函数来获取元素内部的文本。

**query()和 queryAll()**

我们可以使用`**.nativeElement**`并检查它的`**.innerText**` 来抓取文本。这将返回该元素及其子组件中包含的所有文本。如果你想去掉所有的空格和换行符，你可以在返回的字符串上使用`**.trim()**` 。

**querySelector()和 querySelectorAll()**

我们也可以通过检查`**.innerText**`来抓取文本。同样，这将返回该元素及其子组件中包含的所有文本。可以用`**.trim()**` 去掉所有空格和换行符。

## 3.测试* ngIfs

我们还可以测试`***ngIf**`,检查正确的组件是否在应该显示的时候显示出来。我们可以编写一个测试来检查组件在条件为真时是否显示，一个测试来检查组件在条件为假时是否不显示。如果`***ngIf**`的条件语句更复杂，那么您可以编写更多的单元测试。

假设我们有一个这样的模板

我们可以编写一个单元测试，当字段`**showTitle**`为真时检查 id 为`**title**`的元素是否存在，当`**showTitle**`为假时检查该元素是否不存在。我们可以使用`**toBeTruthy()**` 和`**toBeFalsy()**` 来检查组件是否存在。

首先，我们将`**showTitle**` 的值设置为 true，然后通过调用`**detectChanges()**`更新 UI，并检查 UI 中现在是否存在组件。

有时在`***ngIf**`条件下可能会用到一个函数。在这种情况下，您可以在单元测试中更改该函数的返回值，然后更新 UI。假设我们有下面的 HTML 模板。

单元测试应该是

## 4.测试*ngFors

我们还可以测试`***ngFors**`并检查是否显示了正确数量的子组件，以及这些子组件是否传递了正确的数据。我们可以使用`**queryAll()**`或`**querySelectorAll()**`来抓取多个元素。

假设我们有下面的 HTML 模板和一些子组件，每个子组件都有一个类`**.rows**` 。从字段`**messages**` 向每个子组件传递一个字符串。

检查子组件数量是否正确以及正确的数据是否被传递到子组件的单元测试应该是

## queryAll()

## querySelectorAll()

## 5.测试[ngClass]

我们可以测试使用`**[ngClass]**`的元素是否应用了正确的类。我们可以编写一个单元测试来检查当条件为真时是否应用了该类，编写一个单元测试来检查当条件为假时是否应用了该类。

假设我们有下面的 HTML 模板，其中有一个 id 为`**title**`的 div 元素。当字段`**activeTitle**`为真时，它有类`**active**`，当字段`**activeTitle**`为假时，它没有类`**active**`。

我们获取元素并检查它的`**classList**`是否包含字符串`**'active'**`。对此的单元测试应该是

## query()和 queryAll()

## querySelector()和 querySelectorAll()

## 6.测试子组件输出

我们还可以检查当子组件的输出事件触发时是否调用了正确的函数。假设我们有下面的 HTML 模板。我们有一个子组件`**app-child-component**`，它的输出`**outputData**`在输出事件触发时调用函数`**updateData**` 。

我们先窥探`**updateData**` 函数，然后抓取 HTML 元素，用`**dispatchEvent()**`模拟一个事件。我们向该函数传递一个类型为`**outputData**`的新事件。

## query()和 queryAll()

## querySelector()和 querySelectorAll()

## 7.测试子组件输入

我们还可以检查当前组件是否通过它们的输入将正确的数据传递给了其子组件。假设我们有一个包含以下 HTML 的组件。

它包含一个带有选择器`**app-child-component**`的子组件，并有一个输入`**inputData**` ，变量`**title**`通过该输入传递下去。因为这个子组件是我们自己的定制组件，所以我们使用`**query()**`获取组件并得到`**.componentInstance**`。然后我们可以检查输入`**inputData**` 的值。

**query()和 queryAll()**

注意，这里不能使用`**querySelector()**`或`**querySelectorAll()**`，因为我们需要访问`**.componentInstance**` 上的输入。

## 8.测试用户输入和文本区域

我们还可以检查当用户在输入或文本区域元素中键入字符串时，正确的字段是否会更新。在下面的例子中，我们想要检查当用户输入一个新值时字段`**title**`是否被更新。

我们首先初始化字段`**title**`的值，然后通过 id 获取输入元素并得到`**.nativeElement**`。我们手动设置输入的新值，然后使用`**dispatchEvent()**`模拟用户输入事件，并传入类型为`**input**`的新事件。这将使用新值更新该字段。

**query()和 queryAll()**

**querySelector()和 querySelectorAll()**

## 9.测试第三方组件

我们还可以测试第三方组件在用户与它们交互时是否更新了正确的字段。

Angular 9 中引入了组件工具，当用户使用另一个库中的第三方组件时，它为用户提供了一种简单的方法来测试他们的应用程序是否正常工作。

组件线束需要由组件库(如 Angular Material)的作者创建，因此可能不适用于所有库。

在使用组件之前，您必须知道组件的具体实现和结构，以便模拟用户在下拉列表中选择一个选项，或者找到并抓取组件显示的标签，并通过使用大量查询来检查它的设置是否正确。例如`**fixture.debugElement.query()**`

您可以使用`**HarnessLoader**`来获取组件的线束，然后您可以通过线束上的属性轻松地获取组件上的标签，或者通过简单地调用一个方法来模拟用户交互，比如用户单击并选择下拉菜单中的选项。

但是如果没有组件的控制，我们首先需要找出如何模拟用户交互。我们可以通过检查他们组件的文档和查看他们如何编写单元测试来找到这些信息。通常他们的组件会有一个 GitHub 页面。

**ng-选择组件**

例如，让我们看一下 ng-select 组件，它被用作下拉选择器。如果我们去他们的 [GitHub](https://github.com/ng-select/ng-select/blob/master/src/ng-select/lib/ng-select.component.spec.ts) 页面看看他们的单元测试，我们可以看到他们使用一个助手函数`**selectOption()**`来模拟用户点击下拉菜单中的一个选项。

我们可以使用类似的辅助函数`**triggerKeyDownEvent()**`来模拟用户选择不同的键。

假设我们有下面的 HTML 模板，带有一个 id 为`**optionDropdown**`的 ng-select 组件。可能选项的列表来自字段`**options**`，我们可以将下拉列表中的选定值绑定到字段`**option**`。当用户选择一个新值时，我们也可以调用函数`**selectOption()**`。

我们可以编写一个单元测试来检查`**selectOption()**`函数是否被调用

并且另一个单元测试检查字段`**option**`被更新

*更多内容看* [***说白了. io***](http://plainenglish.io)