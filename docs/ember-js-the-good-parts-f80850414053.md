# 好的部分

> 原文：<https://javascript.plainenglish.io/ember-js-the-good-parts-f80850414053?source=collection_archive---------7----------------------->

## 辛烷真的很好

从 2017 年年中开始，我就一直在使用 Ember.js，一开始，它相当具有挑战性。我在这个帖子中记录了我的挑战，我用 Ember.js 记录了我面临的挑战。自从我发表我的挑战已经两年多了，随着时间的推移，它们中的大部分都消失了，相反，我发现用 Ember.js 进行开发是令人愉快的。

在本帖中，我将分享 Ember.js 的好的部分，以我的拙见。

![](img/58ab624083ed4ff6003e71773175a49e.png)

*   本机类而不是 Ember 对象模型
*   `@decorators`
*   `@tracked`和本土的`get` ters 而不是`@computed`属性。
*   `this.property`而不是`get()`和`set()`
*   `Component`世界的大变革

1.  模板协同定位
2.  `<AngleBracket/>`组件的语法超过`{{handle-bar}}`
3.  `@named`元件中的自变量
4.  `{{this.property}}`在模板中
5.  如`on`、`fn`、`did-insert`、`on-destroy`等修饰词

# 本地班级

在原生类的支持下，它只是 JavaScript，没有 Ember 对象模型的任何负担。Ember 对象模型对我来说极具挑战性，主要是因为嵌套的抽象。随着对原生类支持的引入，我的 JavaScript 知识已经足够了，我不需要理解内部原理就能高效工作。

快速对比:

```
// pre Octane
export default Component.extend({
 init() {
   this._super(...arguments);
   this.set('answer', 42);
 }
});//Octane
export default class MyComponent extends Component {
 constructor(owner, args) {
   super(owner, args);
   this.answer = 42;
 }
}
```

注意标准的`class`定义、`extends`、`constructor`、`super`语法代替了`extend`、`init`、`this._super`语法。

你可以在 Ember Guide 阅读更多关于本地类及其好处的内容。

# `@decorators`

> 装饰器是在定义期间在类、类元素或其他 JavaScript 语法形式上调用的*函数*。

`@decorators`的引入进一步简化了语法。

例如:

```
@service('some-service')
someService;// instead ofsomeService: service('some-service')...@action
someAction() {}//instead ofactions {
  someAction() {}
}
```

`@service`、`@action`等。不仅简化和统一了用法，而且减少了认知负荷。

然而，我不确定我们是否需要`@action`装潢师。我发现箭头函数`() => {}`也是为了同样的目的，在下面的例子中，`someArrowFunction`和`someAction` [达到了同样的结果](https://codesandbox.io/s/thirsty-shape-zo8t4?file=/app/services/foo.js)。

```
export default class MyComponent extends Component {
  someArrowFunction = () => {}, @action
  someAction() {}
}
```

在这些装修工中，我最喜欢的是`@tracked`。

# `@tracked and native getter`

`@tracked`很明显，相应的属性正在被跟踪，并且每当它被更新时，变化都会反映在 UI 中。

在辛烷前版本中，这是通过以下方式实现的:

*   `computed property`
*   `this.set()`
*   `set()`

不清楚观察到哪个属性发生了变化，需要在`.js`文件中查找`this.set()`、`set`或`computed property`。

例如:

```
// pre Octane
import Component from '[@ember/component](http://twitter.com/ember/component)';export default Component.extend({
  count: 0,

  suffixedValue: computed('count', function() {
    return foo + this.get('count')
  }), actions: {
    increase() {
      this.set('count', this.get('count') + 1);
    }, 
    decrease() {
      this.set('count', this.get('count') - 1);
    }
  }
});// Octane
import Component from '[@glimmer/component](http://twitter.com/glimmer/component)';
import { tracked } from '[@glimmer/tracking](http://twitter.com/glimmer/tracking)';export default class MyComponent extends Component {
  [@tracked](http://twitter.com/tracked) count = 0;

  get suffixedValue() { 
    return 'foo' + this.count
  } increase = () => {
    this.count = this.count + 1;
  }; decrease = () => {
    this.count = this.count + 1;
  };
}
```

注意，Octane 语法是普通的 JavaScript，没有任何 Ember 抽象，不像 pre Octane 语法。不需要使用`set`来获得反映在模板中的变化。通过使用`@tracked`装饰器，我们已经明确地确保了反应性，并且剥夺了未来维护者追踪反应性来源的乐趣。

# `Component`世界的大变革

组件世界已经有了一些改进，我最喜欢的是这样的:

1.  模板协同定位
2.  `<AngleBracket/>`超过`{{handle-bar}}`的组件的语法
3.  `@named`论据中的成分
4.  `{{this.property}}`在模板中
5.  如`on`、`fn`、`did-insert`、`on-destroy`等修饰语

## 模板协同定位

技术上，模板协同定位在前辛烷时代也是可能的，[通过](https://cli.emberjs.com/release/advanced-use/project-layouts/#podslayout) `[pod](https://cli.emberjs.com/release/advanced-use/project-layouts/#podslayout)`，然而，它不是主流。对我来说，这真的是一件大事，让`.js`和它对应的`.hbs`共处一地，当我在编辑器浏览器中看到对应的文件时，访问对应的文件会容易得多。当然，我可以使用模糊搜索或类似于[相关文件 Hopper](https://marketplace.visualstudio.com/items?itemName=suchitadoshi1987.file-hopper) 的扩展，但是没有什么比协同定位更好的了，至少对我来说是这样。

我希望有一天，甚至测试文件也能放在一起。

## `<AngleBracket/>`

再次，<anglebracket>在辛烷之前的版本中受到支持，但在辛烷中成为主流。</anglebracket>

对我来说，最直接的好处是在。hbs 文件。早些时候这是一个巨大的挑战。

哦，等等，还有一个缺点。在<anglebracket>之前的日子里，组件的使用与`file-name`非常相似，并且经常很容易在代码库中搜索相同的`file-name`。然而，随着`<AngleBracket/>`的出现，我的工作流程发生了变化。我不能再简单的搜索`file-name`，而是转换成`PascalCase` ( `FileName`)再搜索。嗯，考虑到它带来的其他好处，这不是一个交易破坏者。</anglebracket>

## @命名参数

又一个善良！只要看一下语法，我就能确切地知道该属性是自己的属性还是作为参数传递的。`@named`语法用于将参数传递给组件。

```
//pre Octane
{{some-component someProperty="some-value"/}}// Octane
<SomeComponent @someProperty="some-value"/>
```

最好的部分是如何访问这些`@named`参数。

```
// pre Octane
// not easy to identify from the usage, 
// if someProperty is a own property
// or passed as an argumemnt
this.get('someProperty'); //in .js, {{someProperty}} // in .hbs// Octane
// the presense of `args` in .js and `@` in .hbs
// cleaarly identifes it to be
// passed as an argumemnt
this.args.someProperty; //in .js{{@someProperty}} // in .hbs
```

## `{{this.property}}`在模板中

`{{this.property}}`补充了`{{@namedArgument}}`在模板中访问其相应值的功能。通过查看语法，我可以很容易地识别出哪个是自己的属性，哪个是作为参数传递的。

```
// pre Octane
{{somePropertyOrArgument}}// Octane
{{this.property}} {{!-- own property --}}
{{@namedArgument}} {{!-- passed argument --}}
```

## 像`on`、`fn`这样的修饰词

我发现像`{{on}}`、`{{fn}}`这样的修饰符比`{{action}}`更直观，`{{action}}`很神奇，它从`.js`中查找相应的函数，默认情况下将它附加到`click`事件，并负责传递相应函数的参数，等等。

相反，这些修改器的功能更直观。例如，`on`用于处理事件，`fn`用于创建包装函数。

```
//pre Octane
<button
  type="button"
  {{action "someAction"}}
><button
  type="button"
  onclick={{action "someAction" "someArgument"}}
>// Octane
<button
  type="button"
  {{on "click" this.someAction }}
><button
  type="button"
  {{on "click" (fn this.someAction "someArgument"}}
>
```

# 结论

最近和 Ember.js 一起工作真的很愉快。我希望它继续提高和增强开发人员的生产力和幸福感。

一些重要的东西将会很棒:

*   测试文件与源文件在同一位置
*   能够使用自定义目录布局
*   能够在不创建 ember 应用程序的情况下，在 CodePen、JSFiddle 等中渲染 Ember 组件
*   能够通过标准节点模块共享和消费成员组件，而无需使用`addon`格式。

非常感谢所有 Ember.js 贡献者的辛勤工作，感谢他们让这成为一次令人愉快的开发体验。

最后但同样重要的是，我感谢 [Chris Krycho](https://www.linkedin.com/in/chriskrycho/) 、 [Gopal Venkatesan](https://www.linkedin.com/in/gopalvenkatesan/) 的宝贵见解和评论。🙏

*更多内容请看*[***plain English . io***](http://plainenglish.io)