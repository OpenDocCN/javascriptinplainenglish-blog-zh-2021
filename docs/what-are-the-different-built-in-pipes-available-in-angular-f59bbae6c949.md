# Angular 有哪些不同的内置管道？

> 原文：<https://javascript.plainenglish.io/what-are-the-different-built-in-pipes-available-in-angular-f59bbae6c949?source=collection_archive---------15----------------------->

## 从基础到高级面试你必须准备的最新面试问题

## 你必须为下一次面试准备的 100 个问题。

![](img/6fda40f85f2359b1f203d3c73c2802c6.png)

Photo by [Nate Grant](https://unsplash.com/@nateggrant?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我之前的两篇关于角度面试问题的帖子中得到了很多反馈后，我现在来完成剩余问题的答案。

***今天我们将讨论 Angular 中可用的不同内置管道。***

管道是简单的函数，您可以在[模板表达式](https://angular.io/guide/glossary#template-expression)中使用，以接受输入值并返回转换后的值。

管道非常有用，因为您可以在整个应用程序中使用它们，而每个管道只需声明一次。

Angular 为典型的数据转换提供了内置管道，包括国际化转换(i18n)，它使用地区信息来格式化数据。以下是用于数据格式化的常用内置管道:

## `[DatePipe](https://angular.io/api/common/DatePipe)`:根据区域设置规则格式化日期值。

我们可以简单地用管道传递参数来获得转换后的值。

```
<h3>{{ name }} examples:</h3><p>{{date | date:'mediumDate'}}<br>{{date | date:'short'}}<br>{{date | date:'long'}}<br>{{date | date:'full'}}<br>{{date | date:'shortDate'}}<br>{{date | date:'mediumDate'}}<br>{{date | date:'longDate'}}<br>{{date | date:'fullDate'}}<br>{{date | date:'shortTime'}}<br>{{date | date:'mediumTime'}}<br>{{date | date:'longTime'}}<br>{{date | date:'fullTime'}}<br>{{date | date:'h:m:s '}}<br>{{date | date:'hh:mm:ss '}}<br></p>
```

你可以在这里查看实例。

## `[UpperCasePipe](https://angular.io/api/common/UpperCasePipe)`:将文本转换为全部大写。

```
<div>{{ 'this is a BANANA.' | uppercase }}</div>
```

你可以在这里查看实例。

## `[LowerCasePipe](https://angular.io/api/common/LowerCasePipe)`:将文本全部转换为小写。

```
<div>{{ 'this is a BANANA.' | lowercase}}</div>
```

## `[CurrencyPipe](https://angular.io/api/common/CurrencyPipe)`:将一个数字转换为货币字符串，根据地区规则进行格式化。

我们可以通过相应国家的 3 位数代码来获得转换后的值。

```
<p>Euro: {{ 1 | currency:'EUR' }}</p><p>Brazilian Real: {{ 1 | currency:'BRL' }}</p><p>Turkish Lira: {{ 1 | currency:'TRY' }}</p><p>Georgian Lari: {{ 1 | currency:'GEL' }}</p>
```

## `[DecimalPipe](https://angular.io/api/common/DecimalPipe)`:将一个数字转换成带小数点的字符串，根据区域设置规则格式化。

此管道支持小数前和小数后的多个范围。

```
<div><p> {{num1 | number}} </p><p> {{num1 | number:'3.2-5'}} </p><p> {{num2 | number:'3.2-5'}} </p><p> {{num1 * num2 | number:'1.3-6'}} </p></div>
```

你可以在这里查看实例[。](https://stackblitz.com/edit/decimal-pipe-example)

## `[PercentPipe](https://angular.io/api/common/PercentPipe)`:将一个数字转换成一个百分比字符串，根据语言环境规则进行格式化。

这个管道可以将任何值转换成百分比。

```
<hello name="{{ name }}"></hello><p>My Value is {{value}}<br>Its percent is {{value | percent }}<br>Its percent is without the % sign is {{ value * 100 | number }}</p>
```

你可以查看[这里的](https://stackblitz.com/edit/angular-percent-pipe)的实际例子。

# 延伸阅读:

[](/a-guide-to-the-20-best-vscode-extensions-for-frontend-developers-f75a5d716091) [## 面向前端开发人员的 20 个最佳 VSCode 扩展指南

### 面向前端开发的 VSCode 最有用扩展的综合指南

javascript.plainenglish.io](/a-guide-to-the-20-best-vscode-extensions-for-frontend-developers-f75a5d716091) [](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 33 JavaScript 有用的速记作弊清单:2021

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)