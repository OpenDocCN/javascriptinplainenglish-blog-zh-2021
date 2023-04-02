# 使用 createAsyncThunk 和 React 设置 Redux 应用程序

> 原文：<https://javascript.plainenglish.io/setup-an-redux-application-using-createasyncthunk-and-react-79d88331288a?source=collection_archive---------7----------------------->

![](img/89498c57de041c42c3d0b6dfd9bbb4ec.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

今天我们将讨论如何使用 Redux thunk 创建一个 React 应用程序。除了……有点曲折。

![](img/4e8d0b0098d41737be08385118e26e82.png)

Photo by [Anne Nygård](https://unsplash.com/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

事实上，我已经在这里写了一篇关于如何在 React 应用程序上设置 redux-thunk 的文章:[如何在 React 项目中设置 Redux-Thunk |作者 Michael Tong | JavaScript in Plain English](/how-to-set-up-redux-thunk-on-a-react-project-79b0c29c96db)

如果你已经阅读了本教程或任何其他 react redux 教程，你会意识到配置 redux store 相当麻烦，而且有很多样板文件。安装完成后，您必须编写大量复杂的代码，以便应用程序能够与商店正确交互(mhm 操作创建者)。

您可能见过类似这样的代码:

或者这个:

呸。这看起来很难消化和阅读。

如果我告诉您，我们可以使用另一个工具来完成所有这些 redux 魔法，而不需要配置商店的所有样板文件，会怎么样？

使用 redux toolkit，您只需担心几件事情:

*   configureStore 设置
*   创建切片(将缩减器、动作、状态组合成一个函数)
*   createAsyncThunk(它接受一个 redux 字符串，指定要调度的动作并返回一个承诺)

就是这样！现在让我们从头开始设置它。

步骤 1:通过下面的方法创建一个 react 项目:`npx create-react-app reduxtoolkitapp`

第二步:之后，为 redux 安装以下两个包:`npm install — save-dev react-redux @reduxjs/toolkit`

在 src 文件夹下，创建一个名为 store 的文件夹。在该文件夹中，创建一个名为 reducerConfig.js 的文件，其内容如下:

像往常一样，我们将使用的所有减速器组合成组合减速器。在我们的例子中，我们的 reducer 将是一个片的形式，状态和动作作为函数组合在一起。

步骤 3:在 src 文件夹下，创建一个名为 redux 的文件夹。在同一文件夹中，创建一个包含以下内容的 ToDoSlice.js 文件:

步骤 4:在同一个 redux 文件夹中，创建一个名为 thunk.js 的文件:

在 ToDoSlice.js 里面，我们有一个名字，用来标识 reducer 的名字。我们还有一个状态和一个 reducer 函数列表，即 addToList 和 deleteFromList。

注意有一种叫做 extraReducers 的东西。你大概能猜到它在做什么，但是等一下 redux 的旧实现中的 extraReducers 是什么？

答案是……没有。事实上，这些 extraReducers 所做的是允许我们在调度调用的不同阶段执行一些回调。

例如，当 addItem 操作在这里被调度时，它调用 addItem.pending。当我们为 addItem.pending 声明 builder.addCase 时，我们也声明了在发生这种情况时要调用的回调，这就是 startSubmitting 方法。

只有在调度名为“Todo/addItem”的 createAsyncThunk 时，才会调用这个 startSubmitting 方法，如 thunk.js 中的 addItem 函数所示。

一旦 thunk 被调度，addItem.fulfilled 的回调就会被调用。NotSubmitting 被触发并将 isModifying 标志变回 false。

![](img/d61cf57fe178fbba49f3824900ee7a4a.png)

Photo by [David Pupaza](https://unsplash.com/@dav420?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果在调度操作时抛出错误，该怎么办？在这种情况下，将调用设置为 addItem.rejected 的回调，在我们的情况下，它还会将 isModifying 标志设置为 false，表明该流程不再运行。

为了使所有这些工作，我们仍然必须用提供者和商店包装我们的应用程序。

第五步:转到 src/index.js，替换为以下内容:

在这里，我们简单地导入我们在 reducerConfig 文件中创建的存储，并将应用程序包装在它周围。

我们刚刚完成设置 redux 工具包。我们来修改一下 app.js，看看怎么用。

第六步。转到 src/app.js 并替换为以下内容:

在返回状态中，我们有一个地方添加商品名称，还有一个地方呈现商店中的商品列表。当用户添加一个项目时，它将分派该动作，并将新项目放入 redux 存储中。

同样，对于正在呈现的每个项目，都有一个按钮允许用户删除相应的项目。

当我们单击 add item 时，addItem.pending 的回调被调用，以将加载状态更改为 true。当调度操作完成时，调用 addItem.fulfilled 的回调，将加载状态改回 false。

当然，如果 addItem dispatch 调用失败，则会调用 addItem.rejected 的回调。

就是这样！您刚刚创建了一个具有 redux-toolkit 功能的应用程序。

*更多内容看*[***plain English . io***](http://plainenglish.io/)