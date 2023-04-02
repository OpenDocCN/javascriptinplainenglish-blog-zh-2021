# 使用 Zustand 和 TypeScript 在 React 中制作待办事项列表

> 原文：<https://javascript.plainenglish.io/using-zustand-and-typescript-to-make-a-to-do-list-in-react-fe4a41e76748?source=collection_archive---------1----------------------->

今天，让我们来了解一下 Zustand 如何通过制作待办事项列表来轻松管理 React 中的全局客户端状态。

![](img/80c4f5b50afc400a32258a26f9b7a22d.png)

当我第一次遇到 Zustand 时，我无法相信它是如此容易使用。学习曲线薄得令人难以置信。如果你熟悉不可变状态在 React 中是如何工作的，那么你会觉得使用 Zustand 很舒服。所以，事不宜迟，让我们给自己列一个待办事项清单。

# 步骤 1:设置我们的项目

我们需要做的第一件事是获得一个基础项目设置，我们可以通过在终端/Powershell 中使用下面的命令来完成。

```
npx create-react-app zustand-todo-demo --template typescript
```

运行此命令后，这将在 React 中为我们创建一个基本的 starter typescript 项目。接下来，导航到新创建的目录。

```
cd zustand-todo-demo
```

并运行这些命令来安装我们将使用的包。

```
npm install zustand @material-ui/core @material-ui/icons uuidnpm install --save-dev @types/uuid
```

接下来我们需要做的是删除`src`文件夹中所有不必要的文件，并添加一些我们自己的文件。完成后，我们的`src`文件夹应该是这样的。

```
src
├── model
│   └── Todo.ts
├── App.tsx
├── index.tsx
├── react-app-env.d.ts
└── todoStore.tsx
```

完成这些步骤后，现在是时候在代码编辑器中打开我们的项目了。我将使用 VS 代码，但是你可以随意使用任何你喜欢的编辑器。

现在是时候开始编码了！

# 步骤 2:创建我们的 Todo 模型

首先，在介绍 Zustand 之前，我们将为我们的待办事项列表创建一个模型，以描述每个待办事项的数据结构将是什么样子。打开`Todo.ts`文件，将下面的代码放入其中。

在上面的代码中没有太多要解释的，但是我们正在定义一个类型，TypeScript 可以使用它来为我们提供自动完成功能，并确保传递正确的数据。

现在我们的模型已经创建好了，是时候介绍本教程的关键部分了，Zustand。

# 步骤 3:创建我们的 Zustand 商店

我们现在将为我们的待办事项应用程序创建状态管理逻辑。这就是 Zustand 发挥作用的地方。

下面的代码是我们的成品商店将看起来像什么。如果你不明白所有的事情，不要担心，因为我会一行一行地讲解。

`Lines 6 — 11`我们这里有一个界面，定义了我们商店的外观。这有 4 个部分。我们必须在`line 7`上做 Todo，这是一个 Todo 类型的列表。在`line 8`上，我们有一个名为 addTodo 的方法，你可能已经猜到了，这个方法将用于将 Todos 添加到我们的 todo 中。在`line 9`上，我们有一个从待办事项列表中删除待办事项的方法。在`line 10`上，我们有一个方法，给定列表中 todo 项的 id，将切换它的完成状态。

现在已经定义了我们的接口，让我们深入到 Zustand 以及我们如何用它管理状态。

我们正在创建自己的商店。你会注意到我们将使用钩子命名约定(useStore ),这是因为我们使用 Zustand 提供的钩子来访问我们的商店。稍后将详细介绍。我们正在使用 Zustand 中内置的一种叫做`create`的方法，顾名思义，它负责创建我们的商店。`create`函数采用一个有 3 个不同参数的箭头函数(在这个超级简单的教程中我们将只使用第一个参数),并返回一个匹配我们上面定义的接口的对象。这个箭头函数中的参数`set`非常重要，因为它允许我们改变商店的状态。您将在下面的代码中看到这一点。

`Line 15`我们在这里做的是设置待办事项列表的初始状态。在这种情况下，我们每次都将其设置为空列表。也许在更真实的场景中，我们会进行网络调用或检查本地存储的数据来确定初始状态。

`Lines 17 — 28`我们正在定义当我们的`addTodo`方法稍后在我们的代码中被调用时，它将如何执行。这个方法需要注意的是，它只需要接受 todo 项的描述，我们使用一个名为 uuid 的库，我们使用一个 spread 操作符向数组中添加项(这是因为状态是不可变的，每次都必须重新创建)。你将在`line 18`上看到我们正在调用我在上面简单描述过的 set 方法。基本上，这是一个箭头函数，它接受一个与我们上面定义的接口类型相匹配的参数。这个 arrow 函数返回一个对象，在这个对象中，我们可以得到部分更新的状态的样子(在这个例子中，更新的是我们的 todos)。我们没有更新像我们不同的状态管理函数这样的东西，所以我们不必将它们传递给对象。

`Lines 29 — 32`我们正在定义我们的`removeTodo`方法将在被调用时执行。我描述的关于集合和不可变状态的所有东西在这里仍然适用。这里需要注意的是，我们传递一个 id，这样我们就知道要删除哪个元素。这里移除元素的方法是使用 filter 函数从数组中过滤出所有与传递的 id 匹配的元素(显然，应该只有一个)。

`Lines 34 — 42`我们正在定义我们的`toggleCompletedState`方法。我上面讨论的关于 set 函数的所有内容在这里仍然适用。我们正在利用 JavaScript 内置的另一个数组函数(数组映射函数)。这个函数将获取一个数组(在这种情况下，我们的 todos 数组)并返回另一个相同长度的数组，除了它将被转换成不同的结构。在我们的例子中，我们使用 map 函数做的是利用另一个奇特的 JavaScript 特性，即三元运算符。所以如果`line 37`上的条件为真，那么我们将在`line 38`上运行代码，如果为假，那么`line 39`上的代码将被执行。在`line 38`上，我们翻转对象的完成状态；在`line 39`上，我们只是返回同一个对象，因为我们不想改变完成状态，除非它与我们的 id 匹配。

现在我们的商店已经创建，实际上只有最后一步，那就是使用我们刚刚在用户界面中为 React 应用程序编写的代码。

# 第 4 步:在我们的反应应用程序中使用 Zustand

在我们继续之前。我想清理我们的`index.tsx`文件中的代码，看起来像下面的代码。

不用说了，让我们将 Zustand 连接到用户界面。下面是使用 Zustand 的用户界面的代码。不用担心，因为我将在下面介绍重要的部分。

在本演练中，我不会触及 Material-UI 如何工作，因为这超出了本教程的范围，但本质上，它将允许我们轻松地设计和布局我们的应用程序。事不宜迟，让我们看看 Zustand 在我们的 UI 中是如何工作的。您将在`line 44`上看到，我们正在调用函数`useStore()`，该函数将接入我们在上面创建的 Zustand 商店。多亏了对象析构，我们可以取出所有的函数以及我们将在下面使用的状态。在`line 67`上，我们调用了`addTodo`方法，它将获取一个描述并在列表上创建一个新的待办事项。在`line 81`上，我们正在切换待办事项的完成状态。每当我们选中或取消选中待办事项列表中每个列表项的复选框时，就会出现这种情况。在`line 93`我们将从列表中删除一个待办事项。当垃圾桶图标被点击时，这个动作就会发生。最后，你将在`line 75`上看到我们正在循环我们的列表，并为待办事项列表中的每一项生成一个`ListItem`。

# 包扎

Zustand 可能是我在 React 中使用过的最简单、最简单的状态管理解决方案。使用它很愉快，对于那些已经理解 React 的人来说，没有很陡的学习曲线。

一如既往，我欢迎您的任何意见和反馈。请随意分享您最喜欢的 React 状态管理库。我很想听听。

# 附加教程

这里是 React 中其他状态管理库的一些教程，供感兴趣的人参考。

[](/making-a-react-to-do-list-with-redux-toolkit-in-typescript-dd852bfb2c67) [## 用 Redux Toolkit 在 TypeScript 中制作 React To-Do 列表

### 今天我们将学习如何使用 Redux 来管理应用程序的状态，从而制作一个待办事项列表。

javascript.plainenglish.io](/making-a-react-to-do-list-with-redux-toolkit-in-typescript-dd852bfb2c67) [](/managing-local-state-in-react-with-apollo-immer-and-typescript-e966abe58476) [## 使用 Apollo、Immer 和 TypeScript 管理本地状态

### 我们将学习如何在 Apollo 应用中使用反应变量本地管理状态。

javascript.plainenglish.io](/managing-local-state-in-react-with-apollo-immer-and-typescript-e966abe58476) 

# Github 上的源代码

[](https://github.com/13bfrancis/zustand-tut-1) [## 13bfrancis/zustand-tut-1

### 这个项目是用 Create React App 引导的。在项目目录中，您可以运行:在…中运行应用程序

github.com](https://github.com/13bfrancis/zustand-tut-1) 

## 进一步阅读

[](https://bit.cloud/blog/sharing-types-between-your-frontend-and-backend-applications-l5qih48g) [## 在前端和后端应用程序之间共享类型

### 您的后端 API 已经更新，可以返回新类型的数据。必须通知前端团队进行更新…

比特云](https://bit.cloud/blog/sharing-types-between-your-frontend-and-backend-applications-l5qih48g) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***