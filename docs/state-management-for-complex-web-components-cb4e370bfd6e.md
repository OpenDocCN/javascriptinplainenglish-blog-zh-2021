# 复杂 Web 组件的状态管理

> 原文：<https://javascript.plainenglish.io/state-management-for-complex-web-components-cb4e370bfd6e?source=collection_archive---------3----------------------->

## 如何在 LitElement 组件中使用 Redux

![](img/5528a3e340dece049aeec4a18ee4d0da.png)

Web 组件可能是构建与几乎所有 JavaScript 框架兼容的独立小部件的最佳选择。为什么？因为它们体积小、速度快、封装好，并且可以完全没有依赖性。

现在想象构建一个包含复杂配置、控件、事件甚至公共 API 的丰富小部件。当用户与您的组件交互时，我们需要保留更改。它称之为国家。放在内存中，在那里我们存储小部件配置，当这个配置改变时，我们重新呈现视图。

当 web 组件很简单时，我们可以将状态存储在元素实例中，并通过属性和事件传递数据。但是对于更复杂的小部件，您可能会面临跨深度嵌套元素传递数据的副作用和复杂性问题。

一个可能的解决方案是 Redux。这是一个小库，用于存储状态并通知其变化。对于构建 web 组件，我们可以使用 LitElement 库。

## 发展

首先，我们需要初始化项目。最快的方法之一是使用@open-ws 生成器来设置初始结构、依赖项和开发服务器。

需要回答一些问题的引导方式:`npm init @open-wc`

没有问题的单一命令:

```
npm init @open-wc — type scaffold — scaffoldType wc — features linting — typescript true — tagName todo-list — writeToDisk true — installDependencies npm
```

生成器将创建一个非常通用的组件结构。出于教程目的，让我们稍微简化一下。

*   从 src 文件夹中删除 todo-list.ts 和 index.ts。
*   将第 16 行替换为“导入”../dist/src/todo list . js '；在 demo/index.html 中。
*   移除 const title = 'Hello owc World！'；
*   并删除第 21 行的 title 属性。

`TodoList.ts`一开始我们也简化一下。

> 我们使用了@ custom element(' todo-list ')decorator，而不是使用 window . custom elements . define(' todo-list '，todo list)；

如您所见，我们有两个奇怪的标记和两个 js 导入。这些标签也是具有其职责的 web 组件。一个将包含输入和添加任务的逻辑，第二个将显示列表。让我们执行它们。

首先在 src 中创建一个名为`components`的文件夹，然后创建两个 ts 文件:

要提交表单，用户需要在输入中键入一些内容，然后按回车键。具有相应名称`submit`的回调只是在这个阶段清除输入，但稍后我们将处理值。

接下来，我们需要第二个组件来显示已创建任务的列表。

现在，我们可以运行 npm start，开发服务器应该会启动，我们会看到一个到演示服务器的链接。

```
Web Dev Server started…
Root dir: /Users/user_name/Dev/lit-redux/todo-list
Local: [http://localhost:8000/demo/](http://localhost:8000/demo/)
Network: [http://192.168.1.179:8000/demo/](http://192.168.1.179:8000/demo/)
```

我们可以看到浏览器 h2 标题，输入，在这一步总是清空任务列表。因此，我们需要保存任务列表、用于修改该状态的函数以及事件，以便知道状态何时被更改。

## 添加商店

我们创建了两个组件，但它们是独立的组件，目前互不影响。当然，我们可以将输入值传递给父组件，然后将其提供给列表组件。但是我们在这里看到的是商店模式的实现。

这种模式意味着我们有一个对象。这个对象是我们的状态，我们在其中保存设置、输入值、建议选项以及我们需要的一切。然后，我们订阅该对象的更改，并像使用初始状态一样重新呈现我们的视图。这意味着我们总是单向流动。当用户提交输入值时，我们分派一个动作“将值放入任务列表”并将其保存到存储中。然后，列表从存储中接收更新后的列表，并重新呈现带有任务列表的视图。

让我们安装库:`npm install redux`

现在我们需要创建一个函数，根据调用的动作修改当前的存储。首先，在 src 文件夹中创建一个新的文件夹存储，然后创建一个新的文件 reducers.ts。

对于这个演示，我们只实现了两个动作。首先将新任务推送到数组`state.tasks`。第二种方法通过索引找到一个任务，并将其标记为完成或未完成。

您可以提到，我们有从 actions.js 导入的 ACTION_LIST。该文件定义了动作调用时的动作列表和所需参数。

现在我们只需要用这个 reducer 和 actions 创建一个 store。

商店对行动一无所知。它只有一个初始状态和一个缩减器。缩减器将根据所提供的操作名称对每个更改进行操作。这就是为什么将动作名称导出为枚举是一个好的做法。

您可以创建任意数量的减速器。在创建 store 实例时，只需用 combineReducers 将它们组合起来。

我们添加了`(window as any).__REDUX_DEVTOOLS_EXTENSION__?.()`奇怪的代码。这一行不是必需的，但是它让我们能够使用 [Redux DevTools chrome 扩展](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)来调试存储更改。

此外，我还添加了一个注释，即创建商店的实例不是最佳选择。通常情况下，这是可以的，但是对于 web 组件来说就不行了，因为我们可能在一个页面上有多个组件实例。因此，当我们从单个文件导入 const 时，webpack 或任何其他捆绑器会将它作为单个代码用于多个 web 组件，以便小部件共享同一个 store 对象。

我们需要在根类中创建一个实例，并通过属性在子类之间共享它，以避免这个问题。

然后为将使用该存储的组件创建一个基类。你可能已经在`TaskList.ts`中找到了它的用法。

现在在根`TodoList.ts`类中创建 store 实例，并将其作为属性传递给子组件。

`AddTask.ts`和`TaskList.ts`组件将正确地接收一个 store 实例，因为它们是从声明该属性的`base-element.ts`继承的。

## 结论

使用 redux，我们将在扩展 web 组件时简化复杂性增长。此外，我们可以根据自己的意愿，用任意数量的减少器和动作来组织商店。

您可以创建一个带有存储订阅回调的基类，并在使用该存储的组件中从该基类继承。

如果您知道小部件在同一个页面上被多次使用，不要忘记通过属性传递 store 实例。

完整演示可在 [GitHub](https://github.com/Golosay/lit-redux-tutorial) 上获得。

**感谢阅读！请关注我，不要错过我的下一篇关于使用 Redux 的承诺和 HTTP 请求的文章。**

*更多内容请看*[***plain English . io***](http://plainenglish.io/)