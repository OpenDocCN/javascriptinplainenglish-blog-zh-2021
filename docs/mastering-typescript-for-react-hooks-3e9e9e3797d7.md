# 掌握 React 挂钩的类型脚本

> 原文：<https://javascript.plainenglish.io/mastering-typescript-for-react-hooks-3e9e9e3797d7?source=collection_archive---------3----------------------->

因此，您希望在 React 应用程序中使用 TypeScript，但即使是钩子也让您感到苦恼。好吧，让我们让你熟悉如何使用这些钩子来使用 TypeScript 打字，并带你上路。

![](img/f8116705f0b024884bd95f29a09494d7.png)

Banner image

这篇文章旨在补充优秀的 [React 打字稿备忘单](https://github.com/typescript-cheatsheets/react)，你一定要看一看。

# 使用状态

useState 是一个有趣的工具，因为我们一直在使用它，而且大部分时间它都很好，直到它变得不好。举个例子:

```
const [myNumber, myNumberSet] = useState(10);const onClick = () => myNumberSet(20);
```

TypeScript 对此完全没有问题，因为在`useState`上的键入会查看初始值，看到它是一个数字，并将此类型设置为:

```
const [myNumber, myNumberSet] = useState<number>(10);
```

所以任何数字都可以。

当你遇到这样的情况时，问题就来了:

```
const [myAccount, myAccountSet] = useState(null);const onAuthResponse = () => myAccountSet({ user: "foo", ... });
```

TypeScript 不知道您最初设置为`null`的内容可能是一个帐户记录。所以你需要做的就是告诉它:

```
interface IAccount {
  user: string;
  ...
}
const [myAccount, myAccountSet] = useState<IAccount | null>(null);const onAuthResponse = () => myAccountSet({ user: "foo", ... });
```

现在，TypeScript 知道您的`myAccount`值可以是 null，也可以是一个匹配`IAccount`类型的对象。

数组也有类似的问题。举个例子:

```
const [myNumbers, myNumbersSet] = useState([]);const onClick = () => myNumbersSet([10, 20, 30]);
```

TypeScript 将会给出一个非常奇怪的错误，当需要一个`never[]`时，却试图使用一个`number[]`。这实际上是有意义的，因为据 TypeScript 所知，唯一的有效值是一个空数组(即`never[]`)。它不知道你打算在那里储存数字。

所以解决这个问题的方法是键入它

```
const [myNumbers, myNumbersSet] = useState<number[]>([]);const onClick = () => myNumbersSet([10, 20, 30]);
```

现在 TypeScript 又高兴了，因为即使是空数组也是`number[]`的有效类型。

# 使用效果

useEffect 的优点是它不接受任何类型。所以，如果你想确保你输入正确，不用担心，你会的。

如果你想自己检查一下，那么在你的 VS 代码中右击单词`useEffect`并使用`Go to Type Definition`命令转到 React 源代码中定义`useEffect`的地方。

`useEffect`有两个参数，第一个是没有参数的函数，要么返回 void，要么返回另一个函数(cleanup 函数)，后者没有参数，返回 void。

依我看，无论何时你在 TypeScript 中遇到问题，使用`Go to Type Definition`应该是你的第一站。

# 使用上下文

正确输入`useContext`实际上就是正确输入`createContext`调用。例如，您可能会看到这样的内容:

```
const MyContext = createContext(null);
```

这基本上让 TypeScript 对上下文中潜在的内容一无所知，所以它就这样了；上下文必须始终包含 null。这可能不是你想要的。

如果你想要`null`或者一些数据，最简单的方法就是这样定义它:

```
interface IMyContextState {
  userID: string;
}
const MyContext = createContext<IMyContextState | null>(null);
```

它告诉 TypeScript 上下文必须包含一个匹配`IMyContextState`或`null`的对象。

如果你有一个默认状态，那就简单多了:

```
const myDefaultState = {
  userID: "";
}export type MyContextType = typeof myDefaultState;const MyContext = createContext(myDefaultState);export default MyContext;
```

在这种情况下，我们不需要告诉 TypeScript 上下文已经知道了`myDefaultState`中的类型，但是我们现在将默认状态的模式导出为`MyContextType`。这样我们就可以像这样调用`useContext`时使用它:

```
import MyContext, { MyContextType } from './store';
...
const ctx:MyContextType = useContext(MyContext);
```

在这种情况下，`ctx`的输入有点矫枉过正，因为`useContext`已经知道了来自`MyContext`的类型，您可以这样做:

```
import MyContext from './store';
...
const ctx = useContext(MyContext);
```

# 用户教育

键入`useReducer`很像键入 Redux，所以这是一个两全之策，如果你做对了，你就离 Redux 键入更近了。所以`useReducer`取两个东西，减速器和初态。让我们从初始状态开始:

```
const initialState = {
  counter: 0,
};
```

接下来我们需要一些行动。现在，在 Javascript 中，我们根本不会键入这些内容，但在 TypeScript 中，我们可以也应该键入它们，看起来就像这样:

```
type ACTIONTYPES =
  | { type: "increment"; payload: number; }
  | { type: "decrement"; payload: number; };
```

然后减速器看起来会像这样:

```
function myReducer(state: typeof initialState, action: ACTIONTYPES) {
  ...
}const [state, dispatch] = useReducer(myReducer, initialState);
```

这将在`state`上给你提示，并确保任何调度呼叫都需要匹配`ACTIONTYPES`中的一个变量。

# useRef

键入`useRef`，特别是在使用带有 DOM 元素的 refs 时，这是一个非常常见的用例，非常简单。假设你有这样的东西:

```
return (<input ref={inputRef} />);
```

在您的代码中，相应的`useRef`将如下所示:

```
const inputRef = useRef<HTMLInputElement | null>(null);
```

这里指定类型也不是 100%必要的。唯一的技巧是确保获得相应 DOM 元素的正确类型。

如果你要用一个引用来保存数据，你可以这样做:

```
const intervalRef = useRef<number | null>(null);
```

如果你持有一个区间的引用。

# 使用备忘录

`useMemo`上的输入都是关于你放入的工厂函数所产生的内容。例如:

```
const [numbers] = useState([1,2,3,4]);
const filteredNums = useMemo(
  () => numbers.filter(n => n > 2),
  [numbers]
);
```

在这种情况下，由于工厂函数的输出，TypeScript 将`filteredNums`上的类型推断为`number[]`。如果您想键入它，您可以:

```
const filteredNums: number[] = useMemo(
  () => numbers.filter(n => n > 2),
  [numbers]
);
```

但是你真的不需要。TypeScript 非常非常擅长计算函数的返回类型。事实上，如果你愿意的话，你可以使用`ReturnType`实用程序类型从一个函数中获取返回类型，如下所示:

```
type MyFunctionReturnType = ReturnType<typeof myFunction>;
```

你可以在 TypeScript 语言网站上找到更多关于[惊人的实用程序类型的信息。](https://www.typescriptlang.org/docs/handbook/utility-types.html)

# 视频版本

如果你想深入了解这些信息，请查看相关的 YouTube 视频:

Mastering React Hooks with TypeScript YouTube video

# 结论

我使用 TypeScript 和 React 的次数越多，我就越确信它是值得投资的。您可以在编码时获得提示的好处。你通过这些类型来传达你的意图。并且您可以在编译时获得类型安全检查的好处。

希望这篇文章能够帮助您在 React 项目中尝试使用 TypeScript，并学习掌握 React 钩子的类型时实现这些好处。