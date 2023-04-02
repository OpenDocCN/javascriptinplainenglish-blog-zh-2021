# 如何编写自己的自定义 React 挂钩

> 原文：<https://javascript.plainenglish.io/how-to-write-your-own-custom-react-hooks-e0cc05160ba2?source=collection_archive---------15----------------------->

## 抽象函数中的复杂逻辑，并在组件间重用它

![](img/c30f7967c36696afd6d8eb08dedc0c23.png)

如果您使用 React 已经有一段时间了，那么您可能会遇到需要将一些逻辑提取到一个可重用的函数中。随着 React hooks 的出现，这样做已经变成了在公园里散步。我们可以编写自己的自定义 react 挂钩来抽象函数中的复杂逻辑，并跨组件重用它。

# 什么是自定义 React 挂钩？

自定义的 React 钩子实际上是一个在组件内部运行的函数。它可以在内部运行其他钩子或者其他函数。这些函数/钩子也可以是递归的。它使得像渲染道具和高阶组件这样的模式变得不必要。在编写功能组件时，这是一个强大的工具，它为我们提供了以下优势:

*   构建自己的钩子/逻辑
*   提供挂钩 React 特定功能的能力，例如生命周期和状态
*   便携式逻辑
*   快速迭代

有了应用程序中的钩子和定制的 React 钩子，我们可以开始依赖我们的组件来负责用户界面，钩子是处理业务逻辑的部分。

如果你还没有研究过 React 钩子，我们建议你在研究这个钩子之前先看看我们之前关于 React 钩子的文章。

在开始使用自定义 React 挂钩之前，需要知道的一件事是，函数有一个命名约定。里面的逻辑不要紧，但是函数前面一定要加“用”字。

在使用定制钩子之前，检查一下 React 文档中钩子 [post](https://reactjs.org/docs/hooks-rules.html) 的规则也是一个好主意。

这篇文章是关于理解和编写自定义的 React 钩子，而不是关于使用它们的可能性。天空是无限的，许多开源社区已经开发了数量惊人的钩子。虽然它们可能对我们的应用程序有用，但是我们应该知道如何编写我们自己的自定义 React 钩子，因为我们的业务用例相关钩子将不存在。

# 我们要做什么？

尽管我们知道自定义的 React 钩子释放出的合成水平远远超过了我们以前见过的任何东西，但我们将为这篇文章构建一个基本的自定义 React 钩子。我们将抽象我们的逻辑，将数据存储在浏览器的本地存储中。我们还将把我们制作的这个定制钩子添加到我们的[本地存储和 React 钩子](https://www.wisdomgeek.com/development/web-development/react/react-hooks-and-local-storage-lets-build-a-todo-app/)示例中。

我们将把一个键作为钩子的输入，这个键将作为在浏览器的本地存储器中存储值的键。我们还将为将要创建的变量获取一个默认值。钩子将向消费者返回一个变量，并向这个变量返回一个 setter。每当这个变量改变时，钩子也将负责更新它在本地存储中的值。

因此，我们的钩子有如下定义:

```
export const useLocalStorage = (key, defaultValue) => {
  // logic to be added
  return [value, setValue]
}
```

为了返回 React 跟踪的变量，我们可以使用 [useState React 钩子](https://www.wisdomgeek.com/development/web-development/react/react-hooks-and-local-storage-lets-build-a-todo-app/)。此外，由于我们在本地存储中总是以字符串的形式存储值，所以我们将使用 JSON 字符串来存储值，并在检索时解析它们。

```
export const useLocalStorage = (key, defaultValue) => {
  const storedValue = JSON.parse(localStorage.getItem(key));
  const [value, setValue] = useState(storedValue || defaultValue);
  return [value, setValue]l
}
```

这负责返回一个将使用 React state 跟踪的变量。但是我们还需要在每次更新时更新本地存储中的变量值。我们将在自定义的 React 钩子中使用 useEffect 钩子来实现这一点。

```
export const useLocalStorage = (key, defaultValue) => {
  const storedValue = JSON.parse(localStorage.getItem(key));
  const [value, setValue] = useState(storedValue || defaultValue);useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [value, key]);return [value, setValue]l
}
```

这对于我们自己定制的 React 钩子来说已经足够了！每当值改变时，更新的值将反映在本地存储中。而且每当钩子被初始化的时候，如果它不存在，这个值就会被设置为默认值。为了完整起见，我们将把这个键添加到效果的依赖项中，即使它在钩子的生命周期中不会被更新。

# 在我们的应用程序中使用自定义的 React 钩子

现在，我们可以交换应用程序中的以下代码:

```
function App() {
  const [items, setItems] = useState([]);
  const removeItem = (itemToBeDeleted) => {
    setItems(items.filter((item) => itemToBeDeleted !== item));
  };useEffect(() => {
    const items = JSON.parse(localStorage.getItem('items'));
    if (items) {
      setItems(items);
    }
  }, []);useEffect(() => {
    localStorage.setItem('items', JSON.stringify(items));
  }, [items]);return (
    <div className="App">
      <header className="App-header">
        To Do items
        <ItemList items={items} removeItem={removeItem} />
        <AddItemForm addItem={addItem} />
      </header>
    </div>
  );
}
```

使用:

```
function App() {
  const [items, setItems] = useLocalStorage('items', []);
  const removeItem = (itemToBeDeleted) => {
    setItems(items.filter((item) => itemToBeDeleted !== item));
  };return (
    <div className="App">
      <header className="App-header">
        To Do items
        <ItemList items={items} removeItem={removeItem} />
        <AddItemForm addItem={addItem} />
      </header>
    </div>
  );
}
```

它应该还能像以前一样工作。但是现在我们有了在自定义 React 钩子中抽象的本地存储逻辑。我们可以在希望保存到本地存储的任何地方跨多个组件使用这个钩子。

需要注意的是，自定义钩子是独立的。如果在两个组件中使用同一个钩子，它们将不会共享状态。因此，我们有一段真正可重用的代码，可以跨多个组件使用。

希望你在读完这篇文章后对 React 中的自定义钩子有更好的理解。现在开始创建你自己的吧。天空是无限的！请在下面留下你的评论，分享你打算创造什么样的钩子。

*原载于 2021 年 1 月 12 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/react/how-to-write-your-own-custom-react-hooks/)*。*