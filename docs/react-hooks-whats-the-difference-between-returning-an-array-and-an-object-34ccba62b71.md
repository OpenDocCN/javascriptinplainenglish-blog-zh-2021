# react Hooks——返回一个数组和一个对象有什么区别？

> 原文：<https://javascript.plainenglish.io/react-hooks-whats-the-difference-between-returning-an-array-and-an-object-34ccba62b71?source=collection_archive---------5----------------------->

> 这种微小的差异在可用性上造成了巨大的变化。

![](img/8461369804647ff4dcde64d930e937b2.png)

您可能已经在 React 中编写了自己的自定义挂钩，看起来有点像这样:

```
const useExample = () => {
  let myVar = "";

  // Hook Logic... return {
    myVar
  } 
}
```

并且这样称呼它:

```
...
const {myVar} = useExample();
```

这很简单。我们从`useExample`钩子返回一个对象，并使用对象析构来访问`myVar`。

但是如果你看看其他钩子，你可能会注意到它们不使用对象析构——它们使用数组。

```
...
const [value, setValue] = useState(0);
```

这种退货方式有什么区别？要找到一个明确的答案可能很难，但其实很简单。从钩子返回变量的两种方式**同样有效**，它们只是有**不同的用例**。

# {x}和[x]的区别

> 如果一个钩子返回一个数组([x])，那么你可以自己给变量命名。
> 
> 如果一个钩子返回一个对象({x})，那么你必须使用钩子本身返回的变量名。

回到`useState`钩子，它在一个数组中返回它的变量，因为我们很可能会对每个组件不止一次地使用这个钩子。我们需要能够多次实例化那个钩子，但是每个实例都有不同的名称。示例:

```
const [val, setVal] = useState(0);
const [data, setData] = useState("");
```

在`useExample`钩子中，我们被迫使用变量名`myVal`。

React 确实让我们覆盖了我们的对象变量名，但是这比使用数组返回要多得多。下面是上面以对象返回形式重写的`useState`示例:

```
const {state: val, setState: setVal} = useState(0);
const {state: data, setState: setData} = useState("");
```

为了清楚起见，下面是为了使用数组返回而重写的`useExample`钩子的样子:

```
const {myVar: newVarName} = useExample(); //Object return
const [newVarName] = useExample(); //Array return
```

## 用例

> 如果我们要在一个组件中使用一个钩子的多个实例，那么使用数组返回。
> 
> 如果我们的组件只有一个(或几个)钩子，使用 object return。

就是这样！我希望您觉得这篇文章很有用，并且现在已经很好地理解了在 React 中使用钩子返回数组和对象之间的区别。

如果您喜欢这篇文章或觉得它有用，请随意。或者，你可以在 Medium [*这里*](https://jamesmbrightman.medium.com/membership) *支持我或者给我买一杯* [*咖啡*](https://ko-fi.com/jamesbrightman) *！非常感谢所有的支持。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)