# Redux:钩、线和简单

> 原文：<https://javascript.plainenglish.io/redux-hook-line-and-simple-2d6180229a82?source=collection_archive---------6----------------------->

## 至少可以说， [React Redux 指南](https://react-redux.js.org/api/hooks)有点冗长，所以我希望这个快速入门指南更简单。

![](img/b264be9644eb7b0109fd6b1ff5342e86.png)

如果你熟悉 React(如果你想理解这一点，你应该熟悉)，那么你就会理解在我的讲师所说的“道具训练”中通过多个组件和道具管理状态的麻烦。Redux 是这个单一来源的真相难题的一个很好的解决方案；但是，类组件 Redux 很多。你需要地图，然后从道具调度行动，这只是我想有多懒有点多。幸运的是，编写 Redux 的漂亮的人们给了我们功能组件生活方式的钩子。

这并不是要取代正式文件，而是作为一种补充，强调相关要点。我已经省略了导入和代码片段，它们不是使 Redux 挂钩正常工作的因素，所以重点只放在 Redux 上。

```
# If you use npm:npm install react-redux# Or if you use Yarn:yarn add react-redux
```

# 索引. js

在你的 index.js 文件中，你将做一些 Redux 设置，可以在他们的[快速入门指南](https://react-redux.js.org/next/api/hooks)中找到。您创建了一个商店，并将您的 reducer 传递给它。你可以有一个以上的减速器，并使用[组合减速器](https://redux.js.org/api/combinereducers)。你也可以对比他们的[示例代码](https://codesandbox.io/s/9on71rvnyo)。

```
import { Provider } from "react-redux";
import { createStore } from "redux";
import reducer from "./reducer";const store = createStore(reducer);ReactDOM.render(
    <*Provider* *store*={store}>
        <*App* />
    </*Provider*>
document.getElementById("root")
);
```

# 常数

```
export const INCREMENT_COUNT = "INCREMENT_COUNT";
```

首先，我们需要一个有助于自动完成的文件，这样我们可以避免耗时的打字错误。我们可以称之为‘action types . js’。我们创建的任何动作都将存在于一个动作类型文件中。

# 还原剂

```
import * as actionTypes from "./actions";const initialState = {count: 0,} const reducer = (*state* = initialState, *action*) => {switch (action.type) { case actionTypes.INCREMENT_COUNT: return { count: state.count + 1, }
    } return state;
}
```

在一个单独的文件中，我们的 reducer 将使用您创建的常量来处理实际逻辑所在的开关中的情况。所有减速器都应该是[纯功能](https://en.wikipedia.org/wiki/Pure_function)。

# 成分

```
import { useSelector, useDispatch } from "react-redux";
import * as actionTypes from "./actions";
```

[useSelector](https://react-redux.js.org/api/hooks#useselector) 挂钩将允许您读取存储。

[useDispatch](https://react-redux.js.org/api/hooks#usedispatch) 钩子允许你分派动作。

然后，您将像这样调用 useSelector 挂钩:

```
const count = useSelector((*state*) => state.count);
```

你可以在返回或任何你喜欢的地方呈现计数。

调度工作稍有不同:

```
const dispatch = useDispatch();
```

您仍然调用它并将它存储在一个变量中，但是随后您将操作传递给它:

```
dispatch({ type: actionTypes.INCREMENT_COUNT });
```

# 可选项:操作文件

还可以有一个返回 action 对象的 actions 文件。

```
import * as actionTypes from "../actionsTypes";export const incrementCount = () => {

    return {
        type: actionTypes.INCREMENT_COUNT,
    }
};
```

然后将它导入到一个文件中，并作为另一个抽象/简化来调用它。

```
import * as actionTypes from "../actionsTypes";
import * as actions from "../actions";dispatch(actions.incrementCount());
```

希望这个小指南能帮助你试用 Redux！我知道这可能有点吓人，但这真的只是很好地组织了你的代码。黑客快乐！