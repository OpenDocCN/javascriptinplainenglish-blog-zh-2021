# 管道:你不知道你需要的棱角特征

> 原文：<https://javascript.plainenglish.io/pipes-the-angular-feature-that-you-didnt-know-you-needed-e2ea7ba69fc9?source=collection_archive---------14----------------------->

## 在 Angular 中开发时，您有时会发现需要在将值呈现在模板中之前对其进行转换。为了实现这一点，Angular 内置了称为管道的功能。

![](img/65842a12191f90703f8fead15cacbfb0.png)

# 什么是有角的管道？

正如在 [angular 官方文档](https://angular.io/guide/pipes)中所解释的，在 angular 中，管道用于转换显示数据。管道是简单的函数，您可以在模板表达式中使用它来接受输入值并返回转换后的值。示例:

```
<p> My name is {{ name | uppercase }}</p>
```

# 为什么要用有棱角的管子？

要理解为什么管道在 Angular 中很重要，我们必须经历两件事；问题和坚实的软件设计原则。

**问题:**

假设你想在你的角组件中显示一个名字。通常，这可以通过在组件中创建一个函数来实现，该函数将首先执行更改，然后将值添加到变量中。

在`app.component.html`文件中:

```
export class AppComponent { 
 name = 'JOhn DoE'; 
 ngOnInit(): void { 
  name = this.titleCase(name) 
 }  titleCase(value: string) { 
  return value.replace( unicodeWordMatch, (txt => txt[0].toUpperCase() + txt.substr(1).toLowerCase())); 
  } 
 }
```

并且在`app.component.ts`文件中:

输出将是:

![](img/f26230df3a95590ce8575b957d277057.png)

这种方法带来了所需的结果，但反过来，它会有几个问题。仅举几个例子:

1.  该函数不可测试。如果我们要测试 **titleCase** 方法，我们必须首先初始化整个组件及其依赖项。
2.  这违反了实体设计模式中的单一责任原则。这意味着，每个需要将文本转换为标题大小写的组件，都必须定义这个方法，然后用它来改变大小写。 **titleCase** 方法将被重复重新定义。代码中的任何重复都有从长远角度消除维护和扩展代码的能力的风险。

**备选方案:**

这两种情况的替代解决方案是在一个单独的`.ts`文件中创建 **titleCase** 方法，然后将其导出并导入到您希望使用它的每个组件中。在`utils.ts`中:

```
function titleCase(value: string){ 
 return value.replace( unicodeWordMatch, (txt => txt[0].toUpperCase() + txt.substr(1).toLowerCase())); 
} export default titleCase
```

然后在`app.component.ts`中再次修改，首先导入 **titleCase** 方法，然后像我们之前做的那样使用它，但是去掉了 this 关键字。

```
... 
import titleCase from './utils'; .... 
export class AppComponent { 

 name = 'JOhn DoE'; 

 ngOnInit(): void { 
  this.name = titleCase(this.name) 
 } 
}
```

而`app.component.html`保持不变。这个方法管用。但是它有一个或多个缺点。

1.  您必须在使用该方法的每个组件中导入该文件。这在重构过程中会变得非常乏味。对于那些主要需要改变模板的方法，组件不应该知道它。这就是为什么 angular 有自己的[依赖注入机制](https://angular.io/guide/dependency-injection)
2.  您将不得不手动有策略地调用此方法来对更改做出反应，并将它们应用到模板。在上面的示例代码中，它被放在 **ngOnInit** 方法中，该方法在组件初始化时应用大小写变化。它不知道变化检测。

# 管道救援，如何使用角形管道

管道旨在解决上述所有挑战。总之，您创建了一个扩展 Angular **PipeTransform** 类的管道类，您在 **Transform** 方法中定义了您的逻辑，transform 方法的返回值是将传递给模板的值。然后将管道导入到模块中，并使用它作为模板。

要创建管道，请使用 Angular CLI 生成管道。

```
ng g pipe title-case
```

该命令将创建一个带有 **TitleCasePipe** 类样板文件的`title-case.pipe.ts`文件。

```
import { Pipe, PipeTransform } from '@angular/core'; 
@Pipe({ 
 name: 'titleCase' 
}) 
export class TitleCasePipe implements PipeTransform{ transform(value: unknown, ...args: unknown[]): unknown { 
  return null; 
 } 
}
```

Angular 将调用 transform 方法来执行转换。这就是我们的逻辑。该类将变成:

```
... 
export class TitleCasePipe implements PipeTransform {
 transform(value: string, ...args: unknown[]): string { 
  const unicodeWordMatch = /\w\S*/g; 
  return value.replace( unicodeWordMatch, (txt => txt[0].toUpperCase() + txt.substr(1).toLowerCase())); 
 } 
}
```

CLI generate 命令还将对 app 模块进行修改，以便在声明中包含管道。在声明中包含管道将告诉 angular 在运行时加载它，这意味着不需要在同一个模块的组件中导入它。

```
... 
@NgModule({ 
 declarations: [ 
  AppComponent, 
  TitleCasePipe 
 ], 
 imports: [ 
  BrowserModule 
 ], 
 providers: [], 
 bootstrap: [
  AppComponent
 ]}) export class AppModule { }
```

对于 app 模块内的所有组件，titleCase 管道都是可用的。

**管道语法**

管道用在模板内部，直接转换数据。管道语法可以写成:

```
{{ variable | pipe1: argument1 : ... : argumentn | pipe2: arguments...}}
```

*   **变量** —要转换其值的变量的名称。在前面的例子中，变量是 name。
*   **pipe1** —变量将通过的管道的第一个名称。
*   **argument1 到 argumentn** —应该传递给管道以帮助转换的值的列表。参数可以是多个，用分号分隔。
*   **pipe2** —第一个返回值应该传递到的第二个管道。该值从左到右依次通过管道传递。

继续前面的例子，`app.component.html`中的代码变成了:

```
<h1>hello {{name | titleCase}}</h1>
```

恭喜你，现在你已经成功制造了一个功能齐全的管道。

# 管道和变化检测

当由管道转换的变量的值通过任何 DOM 事件或角度变化检测系统识别的其他事件而改变时，角度将通过管道传递新值，并且转换后的值将被返回并相应地分配给 HTML 模板。

这直接解决了我们试图自己编写函数时所面临的问题。而且它们本质上是可测试的，事实上，当您运行生成管道的命令时，它将生成两个类，其中一个是对管道的测试。

# 何时使用角形管

正如所定义、解释和演示的，Angular 中的管道是在模板中转换数据的函数。每当你想在模板渲染前改变一些值时，管道是你的首选工具。

此外，管道的广泛可重复使用性使其甚至适用于最大的应用。角船与伟大的管道开箱，您可以立即在您的项目中使用。对于核心库中没有的管道，Angular 提供了非常简单的机制，可以使用 Angular CLI 生成您自己的定制管道。下面将演示其中一些管道。

# 开箱后装运的角形管道示例

## 标题案例管道

将文本转换为标题大小写。其中每个单词的第一个字母大写，其余字母小写。单词由空格字符分隔，如空格、制表符或换行符。

```
@Component({ 
 selector: 'titlecase-pipe', 
 template: `<div> 
  <p>{{'some string' | titlecase}}</p> <!-- output: "Some String"->
  <p>{{'one,two,three' | titlecase}}</p> <!-- output: "One,two,three" -> 
  <p>{{'true|false' | titlecase}}</p> <!-- output: "True|false" ->
  <p>{{'foo-vs-bar' | titlecase}}</p> <!-- output: "Foo-vs-bar" ->
  </div>` 
}) 
export class TitleCasePipeComponent { }
```

## 上下套管

将任何文本/单词全部转换为小写。

```
@Component({ 
 selector: 'lowerupper-pipe', 
 template: `<div> 
  <p>In lowercase: <pre>'{{"I will be loWERed" | lowercase}}'</pre>
  <p>In uppercase: <pre>'{{"I will be capitalized" | uppercase}}'</pre> </div>` }) 
export class LowerUpperPipeComponent { }
```

## 百分比管道

百分比管道会将百分比管道附加到任何数字，并返回一个字符串。

```
@Component({ 
 selector: 'percent-pipe', 
 template: `<div> 
  <!--output '26%'--> 
  <p>A: {{a | percent}}</p> <!--output '0,134.950%'--> 
  <p>B: {{b | percent:'4.3-5'}}</p> <!--output '0 134,950 %'-->
  <p>B: {{b | percent:'4.3-5':'fr'}}</p> </div>` 
}) 
export class PercentPipeComponent { 
  a: number = 0.259; 
  b: number = 1.3495; 
}
```

# 结论

通过深入研究角形管道，您可以轻松地将它们应用到您的应用或项目中，并充分受益。Angular 管道是使用 Angular 的额外好处之一，因为你很难在其他前端框架中找到相同的构造。

*原载于 2021 年 2 月 13 日*[*【https://whenprogramming.com】*](https://whenprogramming.com/angular-feature-you-didnt-know-you-needed-pipes/)*。*