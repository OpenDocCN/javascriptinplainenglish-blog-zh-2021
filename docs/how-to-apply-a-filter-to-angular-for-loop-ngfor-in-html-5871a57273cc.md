# 如何在 HTML 中对角度 for 循环(*ngFor)应用过滤器

> 原文：<https://javascript.plainenglish.io/how-to-apply-a-filter-to-angular-for-loop-ngfor-in-html-5871a57273cc?source=collection_archive---------2----------------------->

## 用小技巧和窍门学习角度发育 2021

## 可以过滤整个对象数组的过滤管道

![](img/60c49eab3d0406c7826b8af4f2b17628.png)

Photo by [Marc Babin](https://unsplash.com/@marcbabin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们通常会处理大量的数据。基于搜索标准过滤对象数组或基于给定输入过滤整个对象数组总是有一些要求。

Angular 确实提供了一些经典的特性，使得代码可以在整个应用程序中重用。让我们讨论一下如何对*ngFor 循环应用过滤器

我们先来了解一下什么是有角的管子？

该管道在 Angular 1 中称为过滤器，在以后的版本中名称有所改变。

它有一个“@Pipe”装饰器，并实现了一个转换方法，可以处理所有的变更检测。

```
import {Pipe, PipeTransform} from '@angular/core';
@Pipe ({
   name : 'test'
})
export class TestPipe implements PipeTransform {
   transform(args : any) : any{

   }
}
```

我们可以稍后对此进行更深入的讨论。

## 让我们来创建一个可以过滤对象数组的管道。

如果我们有一个对象数组，我们想根据属性名进行过滤。

```
const data = [{
        name: 'atit',
        surname: 'patel'
    },
    {
        name: 'vinay',
        surname: 'panchal'
    },
    {
        name: 'ramesh',
        surname: 'shah'
    }
];
```

模板可以是这样的，

```
<input [(ngModel)] = searchTerm> Search<li *ngFor="let value of data| testFilter:"name":"searchTerm" ">
```

现在让我们创建管道。

```
import { Pipe, PipeTransform } from '@angular/core';[@Pipe](http://twitter.com/Pipe)({
    name: 'testFilter'
})export class TestFilterPipe implements PipeTransform {
    transform(data: any[], filterType: Object): any {
        if (!data || !filter) {
            return data;
        }return data.filter(item => item[filterType].indexOf(val) !== -1);
    }
}
}
```

您需要将它添加到模块中。

```
@NgModule({
    imports: [
        ..
    ],
    declarations: [
        TestFilterPipe,
    ],
    providers: [
        ..
    ],
    bootstrap: [AppComponent]
})
export class AppModule { }
```

## 如果我想搜索所有属性的所有值，该怎么办？

我们可以像这样修改过滤器。

```
data.filter(obj => {
    return Object.keys(obj).reduce((acc, curr) => {
        return acc || obj[curr].toLowerCase().includes(val);
    }, false);
});
```

## 你也可以去 npm 图书馆。

[](https://www.npmjs.com/package/ng2-search-filter) [## ng2-搜索-过滤器

### 过滤搜索项目角度 2 过滤器进行自定义搜索。也适用于角度 4 和角度 5。npm 我…

www.npmjs.com](https://www.npmjs.com/package/ng2-search-filter) 

**参考文献:**

# 准备面试？查看角度面试问题 2021

[](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) 

## *更多内容尽在*[***plain English . io***](http://plainenglish.io)