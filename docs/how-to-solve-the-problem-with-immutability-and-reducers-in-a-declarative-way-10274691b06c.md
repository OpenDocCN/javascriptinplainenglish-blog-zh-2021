# 如何以不可变和声明的方式处理 Redux Reducers

> 原文：<https://javascript.plainenglish.io/how-to-solve-the-problem-with-immutability-and-reducers-in-a-declarative-way-10274691b06c?source=collection_archive---------14----------------------->

![](img/9b53152b094062aa4947e83ff072fd9e.png)

Photo by [Chinh Le Duc](https://unsplash.com/@mero_dnt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都在 Redux 代码中编写了一个缩减器，它有十亿个扩展操作符。我们很高兴它能起作用，但是我们为它的冗长而感到难过。

我将从《粉碎》杂志上的[这篇](https://www.smashingmagazine.com/2020/06/better-reducers-with-immer/)作者[希迪·奥尔吉](https://www.smashingmagazine.com/author/chidi-orji/)的文章中借用一个例子，来展示我所说的减速器类型，以防你有幸从未有机会在野外遇到这些怪物:

```
const updateReducer = (state = initState, action) => {
  switch (action.type) {
    case 'ADD_PACKAGE':
      return {
        ...state,
        packages: [...state.packages, action.package],
      };
    case 'UPDATE_INSTALLED':
      return {
        ...state,
        packages: state.packages.map(pack =>
          pack.name === action.name
            ? { ...pack, installed: action.installed }
            : pack
        ),
      };
    default:
      return state;
  }
};
```

老实说，这本书并没有那么糟糕:相信我，我看过和写过更糟糕的书！

那么这里的问题到底是什么呢？好吧，如果我们想更新一个对象的属性，这个对象深深地嵌套在我们的状态树中，为了克隆当前状态并返回新状态，我们必须做大量的复制和传播工作。记住:reducers 不应该执行副作用，因为它们应该是纯函数，所以最终我们不能改变状态对象，我们必须返回新的状态，因此是一个不同的对象(一个不同的引用)。

就可读性和可维护性而言，过度使用 spread 操作符的问题是，我们没有表达任何关于状态如何更新的意图。我们只是四处复制东西，当我们到达我们想要更新的属性时，周围有很多代码，除了复制我们的状态树的结构之外没有任何用途。

# 让事情具有宣示性

嵌入在 React 中的函数式编程概念教会我们的一件事是，以声明的方式表达意图使我们的代码更容易理解。这对我们未来的自己和我们的同事来说更容易，因为我们写代码是为了让其他人阅读。如果这不重要，我们都会写汇编或字节码，高级编程语言就不会存在了。

因此，与其手动复制东西，然后试图找出我们编写的代码应该做什么，不如实际描述代码应该做什么。以声明方式做到这一点的最佳方式是使用函数。

让我们看看`'ADD_PACKAGE'`动作是如何更新我们前面例子中的状态的:

```
case 'ADD_PACKAGE':
  return {
    ...state,
    packages: [...state.packages, action.package],
  };
```

很简单，对吧？因此，一个新值*将*关联到`packages`属性，我们可以通过*向旧包列表添加*一个新包来获得这个新值。

所以，让我们定义一些函数来执行这些操作。首先，我们要定义一个`assoc`函数:

```
const assoc = (key, value, record) => Object.assign(
  {},
  record,
  { [key]: value }
);
```

接下来是一个`append`功能:

```
const append = (element, list) => [ ...list, element ];
```

我们可以使用这些函数来更新我们的状态:

```
case 'ADD_PACKAGE’:
  return *assoc*(
    'packages’,
    *append*(action.package, state.packages),
    state
  );
```

现在，对于一个简单的例子，好处并不明显。让我们试着用`'UPDATE_INSTALLED'`行动:

```
case 'UPDATE_INSTALLED':
  return {
    ...state,
    packages: state.packages.map(pack =>
      pack.name === action.name
        ? { ...pack, installed: action.installed }
        : pack
    ),
  };
```

在这种情况下，只有当包`name`等于`action.name`时，我们才希望*调整*(或者*关联*一个新值到)包的`installed`属性。现在，我们仍然可以*映射*我们的包列表，但是这有点误导。当我们*映射*一个集合时，我们会认为集合中的所有值都将被转换，所以决定我们是否想要只更新一个元素不仅仅是映射，这是映射的一个特殊版本:我们正在进行选择性更新。

> *在我们的代码中有很多处理分支的方法:最简单的是使用* `*if*` *语句或表达式。尽管有更好的方法来处理条件性，如果条件性意味着行为的改变，我们真正需要的只是一个专门的行为。*

因此，让我们创建一个专门的函数来更好地描述这种行为:

```
const adjustByWhere = (adjustFn, selectFn, list) => {
  return list.map((acc, item) => {
    return selectFn(item) ? adjustFn(item) : item;
  });
};
```

现在，我听到你说:**嘿，那和你在减速器里的东西一模一样！没错！这是同一件事，但它被抽象在一个名称下，这个名称真正描述了事情实际在做什么，这就是进行声明式编程的全部意义:让您的代码描述它做什么，而不是让我们每次读取它时都试图弄清楚它做什么。**

我们的操作如下所示:

```
case 'UPDATE_INSTALLED':
  return *assoc*(
    'packages’,
    adjustByWhere(
      package => *assoc*('installed', action.installed, package),
      package => package.name === 'foo',
      state.packages
    ),
    state
  );
```

这个解决方案远非完美，我们可以对 API 做一些改进，但想法是存在的:开始编写代码，告诉你正在做什么，而不是每次阅读时都必须弄清楚。

# 明摆着的难题

> *如果我不提* `*Immer*` *我会觉得很不负责任，因为它出色地解决了这个问题。我将简要地谈论它，但是如果你想深入研究，请确保阅读文档。*

`Immer`它的出现就像一个巨大的破坏球，为这个问题提供了另一种解决方案:它给你一个草稿，你可以直接更新，改变你想要的任何属性，而不是让你手动复制你的应用程序以前的状态来返回新的状态。在你完成交易后，它会用你修改的草稿不变地创建新的状态。如果你问我(或者如果你问任何人，这是一个聪明的想法)，这是非常整洁和聪明的。

前面的代码看起来像这样:

```
import { produce } from 'immer';const updateReducer = (state = initState, action) =>
  produce(state, draft => {
    switch (action.type) {
      case 'ADD_PACKAGE': {
        draft.packages.push(action.package);
        break;
      }
      case 'UPDATE_INSTALLED': {
        const package = draft.packages.find(p => p.name === action.name);
        if (package) package.installed = action.installed;
        break;
      }
      default: {
        break;
      }
    }
  });
```

现在，这看起来简单多了。然而，这里有一个问题:当使用`immer`时，我们必须遵循几个规则，因为这就是魔术的工作方式。

简而言之:

*   您可以修改草稿或返回新对象。如果你两样都做了，地狱就会爆发。
*   您不能为草稿指定不同的值。您可以更改草稿中的任何内容*，但不能更改草稿本身。*

如果你想进一步了解它，查看文档中的条目[。](https://immerjs.github.io/immer/return)

仅此而已。希望你喜欢阅读这篇文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)