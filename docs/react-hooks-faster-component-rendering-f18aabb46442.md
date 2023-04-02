# 提高 React 组件渲染速度的 4 种方法

> 原文：<https://javascript.plainenglish.io/react-hooks-faster-component-rendering-f18aabb46442?source=collection_archive---------6----------------------->

## 如何提高 React 组件渲染速度和性能

![](img/5a38f77cda2603afad2413a2eaf4e653.png)

Photo by [Bofu Shaw](https://unsplash.com/@hikeshaw?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在构建面向用户的软件时，性能优化已经成为一个重要的考虑因素。我想不出有多少次我失去了兴趣，关闭了手机上的一个应用程序或一个网站，因为页面——甚至是我最感兴趣的组件——加载时间太长。[显然](https://www.nngroup.com/articles/how-long-do-users-stay-on-web-pages)，一般用户在一个网页上只会停留 10-20 秒，除非有一个清晰的价值主张能够吸引他们的注意力。一个高性能的页面/应用程序应该尽可能快地显示这些重要信息。

像 React 这样的前端 JavaScript 框架已经将这一概念融入其中，您可能会对较小的应用程序中提供的现成内容感到满意。React 已经在尝试最小化更新 UI 所需的昂贵的 DOM 操作。事实上，这里的主要租户是 DOM/虚拟 DOM 比较，以决定哪些组件需要重新呈现。

但是，更大规模的系统可能会受益于加速组件呈现的附加工具，从而加快应用程序的速度。

在本文中，我将关注功能组件和 React 挂钩，因为这是我最近的写作方式，尽管这些概念也可以在基于类的组件中重用。

# 1.使用备忘录()

这个钩子实质上缓存了它所传递的函数值。当考虑提高 React 组件的性能时，一个重要的考虑因素是尽可能少地运行消耗 CPU 的操作。

正如在[之前的文章](https://medium.com/@df.eporwei/react-hooks-usememo-ace8e81782b1)中所讨论的那样，`useMemo`使用了一个叫做记忆化的计算机科学概念。这描述了一个操作，它存储一个昂贵操作的结果，并在使用相同的参数再次调用该函数时简单地返回缓存的值。

`useMemo`的函数签名看起来和`useEffect`非常相似。看起来是这样的:

```
const memoizedValue =
    useMemo(() => computeSomethingExpensive(a, b), [a, b]);
```

与`useEffect`类似，在初始渲染后，`useMemo`不会再次计算`memoizedValue`，除非其中一个依赖关系`[a,b]`发生变化。

在下面的例子中，我们假设的昂贵函数是`expFunction`，我们在`useMemo`中调用它，并获取和缓存`resCount`作为结果。这里，`useMemo`只有在`count`改变时才会被重新计算。因此，我们最终得到的是这样一种情况，如果我们在输入字段中键入相同的数字，我们将看到缓存的`resCount`值，而不是重新计算的值。

```
function App() {
    const [count, setCount] = useState(0);

    const expFunction = (count) => {
        return count * 90;
    }    

    const resCount = useMemo(()=> {
        return expFunction(count);
    }, [count])    

    return (
        <>
            Count: {resCount}
            <input type="number" onChange={(e)=> setCount(e.target.value)} placeholder="Set Count" />
        </>
    )
}
```

关于`useMemo`需要注意的是，它是在渲染期间运行的，所以正常情况下不应该出现在渲染阶段的东西不应该出现在这里。这意味着副作用属于`useEffect`而不是`useMemo`。

另一件事是，如果依赖列表为空，将在每次渲染时计算`memoizedValue`，这违背了本练习的目的😕。

# **2。使用回拨**

这里也发生了记忆化，但不是像`useMemo`那样返回记忆化的值，`useCallback`返回一个记忆化的函数，该函数只在它的一个依赖关系改变时才改变。

这个钩子的主要用途是当我们需要在渲染之间维护同一个函数实例的时候。

请记住，在 JS 中，在函数和对象上使用`==`或`===`只执行引用相等。这意味着即使它们共享相同的源，函数实例对解释器来说也是不同的对象:

```
function adds() {
   return (a, b) => a + b;
}const sum1 = adds();
const sum2 = adds();sum1(2, 4);   //- 6
sum2(2, 4);   //- 6sum1 == sum2   //- False
sum1 == sum1   //- Truesum1 === sum2   //- False
sum1 === sum1   //- True
```

举个例子，假设我们想要显示一个很长的列表，并且希望当我们点击列表中的每一项时发生一些事情。作为优化组件的第一步，我们将它包装在`React.memo`中，以防止不必要的重新渲染。

```
import useSearch from './fetch-items';

function MyBigList({ term, onItemClick }) {
  const items = useSearch(term);
  const map = item => <div onClick={onItemClick}>{item}</div>;

  return <div>{items.map(map)}</div>;
}

export default React.memo(MyBigList);
```

当列表中的每一项被点击时，我们要调用`onItemClick`。

```
function ListRenderer({ term }) {

  return (
    <MyBigList
      term={term}
      onItemClick={event => { 
        console.log('You clicked ', event.currentTarget); }
      }
    />
  );
}
```

这里的问题是，传递给`onItemClick`的匿名函数在每次渲染时都获得一个新的实例，所以当 React 比较下一个和上一个道具以决定是否重新渲染`MyBigList`时，它没有通过相等性检查。因此，即使函数没有改变，`MyBigList`——及其所有项目——得到了不必要的重新渲染🥲.

`useCallback`在这种情况下很有用:

```
function ListRenderer({ term }) {
  const onItemClick = useCallback(event => {
    console.log('You clicked ', event.currentTarget);
  }, [term]);

  return (
    <MyBigList
      term={term}
      onItemClick={onItemClick}
    />
  );
}
```

`onItemClick`被记忆，这样即使`ListRenderer`被重新渲染，只要`term`不变，`useCallback`返回相同的函数，`MyBigList`不重新渲染。

需要注意的是，如果子组件很轻，并且可以重新渲染而不会出现性能问题，那么调用`useCallback`是不必要的。*性能优化的成本可能比一开始就不优化要高。*

# 3.React.memo()

根据记忆化的概念，也可以记忆整个功能组件，这样如果传递的属性没有改变，它就可以跳过重新渲染。这种技术可用于优化经常渲染的组件，当传递相同的属性时，这些组件具有相同的输出。

```
function SomeOtherComponent(props) {
   ...
}
const MyComponent = React.memo(SomeOtherComponent);
```

默认情况下`React.memo()`会对道具做一个浅显的比较，但是如果你需要更深入的比较，可以传递第二个参数:

```
function SomeOtherComponent(props) {
   ...
}function compareProps(prevProps, nextProps) {
  /*
   return true if passing nextProps to render would return
   the same result as passing prevProps to render,
   otherwise return false
  */
}const MyComponent = React.memo(SomeOtherComponent, compareProps);
```

注意，React.memo 只检查适当更改；如果您的组件使用 useState 或 useContext，则当状态或上下文发生变化时，该组件将正常重新呈现。

# 4.开窗术

这是 docs 中建议的一种技术，它可以极大地减少创建的 DOM 节点以及渲染很长的列表所需的时间。使用这种方法，一次只装载列表中项目的一个子集——显示给用户的项目。两个著名的库提供了使用这种技术帮助显示列表、表格和网格的组件，它们是 [react-window](https://react-window.vercel.app/#/examples/list/fixed-size) 和 [react-virtualized](https://bvaughn.github.io/react-virtualized/#/components/List) 。

# 其他优化方法

## **使用生产版本**

它将缩小你的代码库，并尽可能地减少它。

## **尽可能避免渲染中的匿名函数**

因为没有向匿名函数传递标识符，所以它们不会在呈现之间持久化。这意味着在每次渲染中，解释器都会为这些函数分配一块新的内存(即使它们没有改变)，而不是通过调用对方法的引用来分配一次。

```
//- Don't do this ❌
function Component() {
    return (
      <button onClick={
           () => console.log('Unnamed; new instance each render.')}
      >Unnamed
      </button>
    );
}//- Do this ✅
function Component() {
    const handleClick = () => console.log('Call me by my name');           return (
      <button onClick={handleClick}>Click me</button>
    );
}
```

## **安装和卸载可能非常昂贵**

使用条件来安装和卸载组件将导致浏览器重画和重排。这种方法通常是昂贵的，而且根据组件和生成的 DOM 节点的复杂性，可能会更贵。这是因为当节点被删除和追加时，周围 HTML 元素的位置和几何形状需要重新计算。一个可选的解决方法是使用 CSS 可见性/不透明性来隐藏元素。

# 结论

最后一个我认为绝对值得一提的工具是 Chrome Timeline Devtools，它可以在 Performance 选项卡中找到。该工具在可视化过度重新渲染的组件时特别有用。通过显示哪些组件被不必要地重新渲染以及重新渲染的频率，它可以很好地概述组件的“健康状况”,从而帮助快速确定应用程序中潜在的问题区域。Chidume Nnamdi 已经写了一篇详细的文章，介绍了它的工作原理以及如何使用它。

还有很多方法可以提高 React 应用程序的性能，但这是我发现最常用的几种方法。欢迎在评论中提供更多建议。

快乐编码。

## 参考

*   [不要过度使用 useCallback](https://dmitripavlutin.com/dont-overuse-react-usecallback/)
*   [如何在 JavaScript 中比较对象](https://dmitripavlutin.com/how-to-compare-objects-in-javascript/)
*   [React.memo](https://reactjs.org/docs/react-api.html#reactmemo)
*   [优化和提高 React 应用程序性能的方法](https://www.smashingmagazine.com/2020/07/methods-performance-react-apps/)

## 进一步阅读

[](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) [## 帮助您在 React 中更快开发的 5 种工具和实践

### React 工具、技巧和最佳实践将帮助您更快地构建应用

javascript.plainenglish.io](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***