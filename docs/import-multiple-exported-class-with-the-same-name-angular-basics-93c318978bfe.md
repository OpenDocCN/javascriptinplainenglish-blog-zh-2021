# 导入多个同名的导出类-角度基础

> 原文：<https://javascript.plainenglish.io/import-multiple-exported-class-with-the-same-name-angular-basics-93c318978bfe?source=collection_archive---------8----------------------->

## 一个简单的技巧来导入两个或更多的类，如果它们在 Angular 中共享相同的名字。

![](img/fb4182d91619265294550cb6d06094cd.png)

Cover Image by Author | Learn angular basics for free

## 要求:

假设我有两个类，它们共享同一个名字，如下例所示。

```
import {CommonClassName} from '../module1/CommonClassName';
import {CommonClassName} from '../module2/CommonClassName';
```

在这种情况下，您可以使用下面给出的别名`as`。您可以在方便的时候更改别名。

```
import {CommonClassName} from '../module1/CommonClassName';
import {CommonClassName as AliasName} from '../module2/CommonClassName';...
//You can call particular class with AliasName, as given below.this.modelClass = new AliasName();
```

如果您的项目有很长的类名，您可以使用别名`as`来缩短它。

**宾果！👏👏👏**

你做到了！您可以在别名中给出任何名称，并且如果它们共享相同的名称，可以使用任何类！

# 好奇想了解更多 Angular/Javascript 的“导入语句”？

`Import` 是静态的，所以静态的`import` 语句被用来导入只读的活动绑定，这些绑定被另一个模块`exported` 了。

无论您是否声明导入的模块，它们都在`strict mode`中。在嵌入式脚本中不能使用`import`语句，除非这样的脚本有一个`type="module"`。导入的绑定称为活动绑定，因为它们是由导出绑定的模块更新的。

还有一个类似函数的动态`**import()**`，它不需要`type="module"`的脚本，可以使用`<script>`标签上的属性`nomodule`来确保向后兼容性。

# 导入语法有很多种。

```
import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { foo , bar } from "module-name/path/to/specific/un-exported/file";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
var promise = import("module-name");
```

## 说明

*   **defaultExport**
    将引用模块默认导出的名称。
*   **模块名**
    要导入的模块。这通常是的相对或绝对路径名。包含模块的 js 文件。某些捆绑商可能允许或要求使用扩展；检查你的环境。只允许单引号和双引号字符串。
*   **name**
    模块对象的名称，在引用导入时将用作一种命名空间。
*   **exportN**
    要导入的出口的名称。
*   **aliasN**

简化语法——这样你就能容易地记住它。

**1。从模块**导入单个导出

```
import {myExport} from '/modules/my-module.ts';
```

**2。导入整个模块的内容**

```
import * as myModule from '/modules/my-module.d.ts';
```

**3。从模块**导入多个导出

```
import {foo, bar} from '/modules/my-module.ts';
```

**4。用更方便的别名**导入导出

```
import {reallyReallyLongModuleExportName as shortName}
  from '/modules/my-module.js';
```

**5。在导入过程中重命名多个导出**

```
import {
  reallyReallyLongModuleExportName as shortName,
  anotherLongModuleName as short
} from '/modules/my-module.js';
```

**6。只为它的副作用导入一个模块**

```
import '/modules/my-module.js';
```

希望你能找到一个好的解释和更多关于进口的知识。如果它对你有用或者你觉得这篇文章有帮助，请评论。

**参考:**

*【1】导入语句详情—* [*Mozilla 开发者*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

> 最初由 Rakshit Shah (Me)在 Angular 的[Import Multiple Exported class 中发布](http://www.9mood.com/angular-basics-import-multiple-exported-class-with-same-name/)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)