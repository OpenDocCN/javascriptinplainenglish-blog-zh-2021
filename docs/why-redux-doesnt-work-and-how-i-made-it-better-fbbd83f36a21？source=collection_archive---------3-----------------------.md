# Redux 为什么不行

> 原文：<https://javascript.plainenglish.io/why-redux-doesnt-work-and-how-i-made-it-better-fbbd83f36a21?source=collection_archive---------3----------------------->

## 以及我如何让它变得更好

![](img/ba214fdf357ee3850ebcac01272ea272.png)

Redux official logo

众所周知，Redux 和 React 一样，是高度非个人化的——并以此为荣。这实际上是他们的工作方式，许多开发人员喜欢它带来的灵活性。但不是我。

我承认一个专横的库甚至比一个非专横的库更难共事，但是两者都太多会带来混乱和头痛。Redux 是一个好的开始，但是，根据我的经验，它对大多数 React 应用程序来说还不够好。

刚开始用 Redux 的时候，喜欢它的简洁，更重要的是，它就是好用。但是当我建立了越来越多的商店时，我发现自己正在从旧项目中复制和粘贴冗余的、样板式的代码。我花了更多的时间重新输入旧代码，花更少的时间实际设计商店。甚至在使用 Redux toolkit 时也是如此，我发现它很有帮助，但仍然不能令人满意。

因此，几周前，我决定对此做些什么:我设计了一个基于 Redux 的高度自以为是的状态管理库，我可以将它用于我自己的 React 项目。

在这篇文章中——献给所有和我一样沮丧的开发人员——我分享了我的想法。

但首先，我觉得有必要阐述一下我对 Redux 的不满，正是这种不满驱使我编写了自己的库。

## 它没有建筑

架构是将脚本和应用程序分开的东西。十年前，当我们还在 HTML 页面中注入 JS 脚本时，构建 Javascript 代码没有什么意义。但是在 Typescript 和 SPA 框架的世界中，这不仅是明智的，而且是负责任的做法。

架构为软件设计提供了几个重要的好处。首先，它不仅在应用程序内部，而且在整个组织甚至整个行业中引入了一致性，这取决于它的采用程度。同样重要的是，好的架构使代码更具可读性和可消化性:你知道在哪里可以找到什么，以及它们是如何组合在一起的。这提高了生产率，并增进了对代码库的理解。

Redux 让架构对开发者完全开放。它的设计模式提供了一个坚实的基础，但是基础就是基础。就像你不会仅仅生活在一个混凝土的基础上，你也不应该仅仅用 Redux 来为你的 React 应用建立一个中心商店。

## 很难扩大规模

假设您需要将您的状态分成不同的部分。当然，您可以使用 Redux toolkit 的切片模式，但是您最终会得到许多没有清晰层次的移动部件。这将 Redux 存储的缩放限制在一个维度。

所有这些都意味着，随着应用的增长，仅用 Redux 来管理中央状态变得越来越不方便。它*起作用*，但是我们可以做得更好。

## 它模糊了实现和接口之间的界限

这是软件设计的大罪。存储是用归约器和初始状态实现的；它通过动作创建器和选择器进行接口。如果没有一个清晰划分界限的架构，这种区别就会变得模糊不清。

画出这种区别不仅引入了关注点的分离，而且有助于减少商店内的名称冲突。我们都讨厌那种输入要导入的函数名，却只能看到三个不同的文件的感觉。

## 缺乏类型安全

这显然是一个 Typescript 问题，但是(如果您没有看过我在 Medium 上发表的其他文章)，我认为 Typescript 是设计良好的 Node.js 应用程序不可或缺的一部分。我的理智依赖于类型安全，而 Redux 几乎不能提供任何东西。如果我改变了一个动作的有效负载类型，但没有修改它的 reducer，我应该会立即得到一个错误，阻止编译。如果我删除了一个 reducer，但是没有删除它的 action creator，我会得到一个错误，阻止编译。你明白了。

尽管 Redux toolkit 试图解决这个问题，但它没有提供既优雅又完全类型安全的解决方案。幸运的是，扣篮做到了。

# 更干净的状态管理方法

我写了 Dunk 来解决所有这些缺点，我怀疑有类似需求的其他人也会觉得它很方便。

Dunk 是一个可伸缩的、积极的类型安全状态管理框架，旨在最小化代码重复和最大化模块化。它构建在 Redux 之上，并公开了基本相同的 API，因此您可以在已经使用 Redux 的任何地方使用它。

此外，它包含对 thunks 的一流支持，使异步操作变得轻而易举。

那么，它是如何工作的呢？

## 模块，而不是切片

切片的最大限制是它们的单维度。你可以想要多少就有多少，但是中央政府没有明确的层级。这抑制了可伸缩性。相反，像任何好的架构一样，我们想要的是模块化——而这正是 Dunk 所提供的。

在 Dunk store 中，基本元素是可组合的模块，每个模块都有自己的状态、动作、reducers 和子模块。Dunk 提供了实用程序类和函数，使得定义动作创建器和选择器以及嵌套模块变得毫不费力。而且它完全是类型安全的，降低了运行时错误的风险。

## 扣篮界面

Dunk 还在商店的界面和它的实现之间画出了急需的区别。

在内部，模块定义了三件事:状态、动作和归约器。理想情况下，这些都不应该被商店的客户访问(比如 React 组件)。

从外部来看，模块定义了两件事:修改状态的动作创建器和读取状态的选择器。我们将很快看到两者的一些例子。

# 创建扣篮模块

首先，您需要安装软件包:

```
npm i @bswohlers/dunk
```

一个模块应该包含三个文件:`types.ts`、`reducer.ts`和`index.ts`。

我们将从类型开始。首先，我们为我们的状态定义一个类型:

```
type RootState = {
  counter: number;
}
```

接下来，我们列举模块可以处理的动作:

```
export enum RootActions {
  SET_COUNTER = "set-counter",
  INC_COUNTER = "inc-counter",
  RESET_COUNTER = "reset-counter"
}
```

注意，这必须是唯一字符串的`enum`。

最后——这也是 Dunk 获得其神奇的类型安全性的主要原因——我们将定义一个类型来指定每个动作的有效载荷类型。

```
type RootActionPayloads = DunkActionPayloads<RootActions, {
  [RootActions.SET_COUNTER]: number;
  [RootActions.INC_COUNTER]: undefined;
  [RootActions.RESET_COUNTER]: undefined;
}>
```

例如，我们的`SET_COUNTER`动作将把一个`number`作为它的有效载荷。我们马上会看到这如何帮助防止粗心的错误。

唯一需要创建的类型是`DunkModule`，它将这三种类型捆绑在一起，以便于以后参考:

```
export type RootModule = DunkModule<RootState, RootActions, RootActionPayloads>;
```

接下来，让我们创建我们的减速器。Dunk 提供了`composeReducers`函数来帮助我们轻松地创建一个类型安全的缩减器。我们需要做的就是为每个动作传入初始状态和 reducers。

```
export const rootReducer = composeReducers<RootModule>({
  counter: 0
}, {
  [RootActions.SET_COUNTER]: (state, payload) => {
    return { ...state, counter: payload };
  },
  [RootActions.INC_COUNTER]: (state) => {
    return { ...state, counter: state.counter + 1 };
  },
  [RootActions.RESET_COUNTER]: (state) => {
    return { ...state, counter: 0 };
  }
});
```

因为我们将`RootModule`作为类型参数传递给`composeReducers`，所以`payload`和`state`是为每个减速器自动类型化的。这也确保了我们每个动作都有一个缩减器。

最后，我们将在`index.ts`中定义模块的接口。我们可以使用`DunkInterfaceCreator`类，它没有状态，公开了一些方法来帮助我们定义模块的动作创建者和选择器。

```
const creator = new DunkInterfaceCreator<RootModule, RootState>();
```

让我们从创建一个选择器开始。选择器是将存储的状态作为参数并返回对状态的一些操作的函数，允许接口的客户端读取存储中的数据。我们需要做的就是向`defineSelector`方法传递一个简单的函数:

```
const getCounter = creator.defineSelector(state => state.counter);
```

接下来，我们将定义动作创建者。动作创建器是返回动作或 thunk 动作的函数(关于 thunk 的更多信息，见此处的[。多亏了 thunk 中间件，`store.dispatch`可以处理这两种类型。](https://www.npmjs.com/package/redux-thunk)

下面是一个返回`SET_COUNTER`动作的动作创建器:

```
const setCounter = creator.defineActionCreator((value: number) => ({
  type: RootActions.SET_COUNTER,
  payload: value
}));
```

下面是一个动作创建器，它返回一个 thunk，该 thunk 按时间间隔递增计数器:

```
countInterval = creator.defineActionCreator((interval: number) => {
  return (dispatch, getState) => {
    setInterval(() => {
      const oldCounterValue = getState().counter;
        dispatch(setCounter(oldCounterValue + 1));
    }, interval);
  }
});
```

最后，我们将选择器和动作创建器结合起来，形成这个模块的接口部分:

```
export const RootInterface = creator.createInterfacePiece({
  selectors: {
    getCounter
  },
  actionCreators: {
    setCounter,
    countInterval
  }
})
```

我们还不能直接使用这个接口——我们首先需要通过将它传递给`createDunkInterface`来完成它，我们很快就会看到。

# 创建一个扣篮商店

要创建一个商店，我们可以将根缩减器传递给`createDunkStore`:

```
const store = createDunkStore(rootReducer);
```

`store`本质上将拥有与 Redux store 相同的接口，因此您可以在任何可以使用 Redux store 的地方使用它。

接下来，我们将创建商店的界面。我们通过将根接口传递给`createDunkInterface`来实现这一点:

```
const Store = createDunkInterface(RootInterface);
```

现在，我们可以调度操作:

```
store.dispatch(Store.actionCreators.countInterval(1000));
```

或者使用选择器:

```
const counter = Store.selectors.getCounter(store.getState());
```

# 嵌套模块

Dunk store 卓越的可伸缩性在于其模块的可组合性。通过嵌套模块，您可以完全按照您想要的方式组织您的数据存储，确保关注点的分离和干净的目录结构。

让我们创建一个名为 Settings 的子模块。在商店的根目录下创建一个名为`settings`的目录。就像我们的根模块一样，创建`types.ts`、`reducer.ts`和`index.ts`。

类型:

```
type SettingsState = {
  incrementStep: number;
}

export enum SettingsActions {
  SET_INC_STEP = "settings/set-inc-step",
}

type SettingsActionPayloads = DunkActionPayloads<SettingsActions, {
  [SettingsActions.SET_INC_STEP]: number
}>

export type SettingsModule = DunkModule<SettingsState, SettingsActions, SettingsActionPayloads>;
```

减速器:

```
export const settingsReducer = composeReducers<SettingsModule>({
  incrementStep: 1,
}, {
  [SettingsActions.SET_INC_STEP]: (state, payload) => {
    return { ...state, incrementStep: payload };
  }
});
```

索引:

```
const creator = new DunkInterfaceCreator<SettingsModule, RootState>();

const setIncStep = creator.defineActionCreator((value: number) => ({
  type: SettingsActions.SET_INC_STEP,
  payload: value
}));

export const SettingsInterface = creator.createInterfacePiece({
  actionCreators: {
    setIncStep
  }
});
```

现在我们已经完成了我们的子模块，我们只需要通过添加它作为`RootModule`的子模块来将其集成到商店中。

第一步是更新`RootState`:

```
type RootState = {
  counter: number;
  Settings: SettingsModule;
}
```

接下来，我们更新传递给`rootReducer`的初始状态:

```
export const rootReducer = composeReducers<RootModule>({
  counter: 0,
  Settings: settingsReducer
}, {
  [RootActions.SET_COUNTER]: (state, payload) => {
    return { ...state, counter: payload };
  },
});
```

最后，为了将设置接口集成到商店的接口中，我们需要将其指定为根接口的子接口:

```
export const RootInterface = creator.createInterfacePiece({
  selectors: {
    getCounter
  },
  actionCreators: {
    setCounter,
    countInterval
  }
}, {
  Settings: SettingsInterface
})
```

就是这样。我们现在可以通过界面轻松访问设置模块的动作、选择器和 thunks。例如，如果我们要设置`incrementStep`:

```
store.dispatch(Store.Settings.actions.setIncStep(5));
```

# 就这么简单

Redux 是一个很棒的库，但是在生产中使用它就像试图用棍子盖房子一样。尽管有对非个人化库的大肆宣传，状态管理是前端开发的一部分，清晰的架构和严格的设计模式将改善开发人员的体验并提高生产率。

这里有一个官方文档的链接，可以更深入地了解 API 以及如何充分利用 Dunk。这里的[是一个到 GitHub repo 的链接。](https://github.com/wwohlers/dunk-js)

*更多内容请看*[***plain English . io***](http://plainenglish.io)