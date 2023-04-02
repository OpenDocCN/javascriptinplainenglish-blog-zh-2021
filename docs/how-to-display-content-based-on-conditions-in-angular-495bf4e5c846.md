# 如何根据角度中的条件显示内容

> 原文：<https://javascript.plainenglish.io/how-to-display-content-based-on-conditions-in-angular-495bf4e5c846?source=collection_archive---------4----------------------->

## 角度基础备忘单 2021

## 根据条件以 HTML 呈现内容

![](img/0f980b7edd910902d3db9346632c1a62.png)

Photo by [Firos nv](https://unsplash.com/@firosnv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每个前端开发人员在工作中做的一个常见任务是根据简单的条件显示和隐藏模板，如果条件匹配。

是的，你可能会认为这是一件很平常的事情，每个人都知道，但有时对于一个新手来说，最好在备忘单中添加一些内容，这样他们就可以在需要的时候复习了。

> 让我们讨论一下 Angular 提供了什么。

Angular 确实提供了一个结构指令，用于检查布尔条件并基于此呈现特定元素。

## 1.*ngIf

这个指令的简写是`*ngIf= “conditions”`它可以和任何标签一起使用。(注意:不要忘记在组件中包含一个变量)

```
<div *ngIf="testcondition">
      I can be viewable if condition true
 </div>
```

同样的方法，我们可以写，如果条件不匹配，该怎么做。

```
<div *ngIf="!testcondition">
     I can be viewable if condition false
 </div>
```

## 2.*ngIf 和 Else

当我们不想写`*ngIf= “negativelogic”`时，我们可以使用 ngIf else 方法。这里我们必须定义`ng-template`中的 else 部分

```
<ng-container *ngIf="testcondition; else elseTemplate>
      I can be viewable if condition true
    </ng-container><ng-template #elseTemplate>
     I can be viewable if condition false
 </ng-template>
```

## **3。*ngIf，Then and Else**

如果我们想处理 3 个嵌套条件呢？也可以处理。

```
<ng-container *ngIf="testcondition;  then OneCondition; else elseTemplate">
 I can be viewable if condition true
</ng-container><ng-template #OneCondition>
     I can be viewable if other condition gets true
 </ng-template><ng-template #elseTemplate>
       I can be viewable if condition false
    </ng-template>
```

## 4.*ngSwitch

如果我在 HTML 中有 3 个以上的条件需要处理并相应地呈现内容，该怎么办？不用担心，angular 提供了一个 switch 语句。

```
<ul *ngFor="let data of testData"
    [ngSwitch]="data.name"> 

  <li *ngSwitchCase="'Atit'">{{ data.name }} 
  </li>
  <li *ngSwitchCase="'Ramesh'">{{ data.name }} 
  </li>
  <li *ngSwitchCase="'Mahesh'">{{ data.name }} 
  </li>
  <li *ngSwitchDefault >{{ data.name }} 
  </li>
</ul
```

**参考文献:**

# 你可以看看我以前的文章

*更多内容请看*[*plain English . io*](http://plainenglish.io/)