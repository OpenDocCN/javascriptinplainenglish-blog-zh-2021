# 构建完整的堆栈 React 应用教程(第 1 部分)

> 原文：<https://javascript.plainenglish.io/building-a-full-stack-react-app-tutorial-821120e014a2?source=collection_archive---------5----------------------->

让我们学习如何从头开始创建一个全栈 React 应用程序

![](img/543dc485423fbe85923b62a2a5bd1cd6.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

现代 web 应用程序已经变得更加强大和复杂。不仅仅是从后端服务器渲染 HTML 和 CSS 文件。有了 React 这样的框架，构建前端繁重的项目变得容易多了。

React 使用基于组件的架构来创建单页面应用程序。本教程让你学习如何从头开始创建一个单页 web 应用程序。

## 全功能 React 应用程序的要素:

1.  创建可重用组件
2.  将代码分成小的组件
3.  反应路由器
4.  状态管理—上下文 API
5.  后端:REST API

![](img/b1e7c8ee5ed47dcca24d486c1aba7cfe.png)

Photo by [Dylan Gillis](https://unsplash.com/@dylandgillis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 了解应用程序—考试助手

考试助手是一个为学生提供的帮助他们考试的网络应用程序，它包含一个科目列表，每个科目都有不同主题的音频笔记。对于本教程，我们将只构建应用程序的前端部分。后端 API 会将音频文件存储在一个由教师上传的数据库中。

该应用程序的设计类似于 Spotify 应用程序，为学生提供音频文件播放列表。

## 创建 React 应用程序

```
npx create-react-app exam-assistant
```

通过在终端中键入上述命令来创建 React 应用程序。设计应用程序的前两步是理解所需的组件和路线。对于路由，我们使用一个名为 react-router-dom 的库。

```
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";
```

在我们的项目中，有两条路线供学生上传笔记，一条是主仪表板，另一条是教师上传笔记。

我们将使用 react-router 中的交换机组件。确保路线与指定的路径完全匹配。

```
function App() return (
     <Router basename={window.location.pathname || ''}> <Switch>
          <Route path="/teacher">
            <Teacher />
          </Route>
          <Route path="/">
            <Home />
          </Route>
      </Switch> </Router>
  );
}
```

## 构建主要组件

仪表板组件将有一个侧栏、主体和页脚。

侧边栏组件将显示主题列表。body 组件将显示从侧边栏中选择的主题的音频注释列表。页脚组件将显示从正文中选择的音频文件。

这就是我们遇到状态管理和适当钻探问题的地方。请注意同一层次结构中的组件是如何依赖于彼此的状态的。为了解决这个问题，我们必须从父组件传递道具，以便它到达所有子组件。

这就是上下文 API 的用武之地，它为我们提供了一个全局状态对象，就像这些组件之上的数据层，这样就可以从这个数据层中包装的任何组件访问上下文中的数据。

![](img/4cbb6ad8b14ba5935ca1f07563eab1bb.png)

Photo by [Edvard Alexander Rølvaag](https://unsplash.com/@edvardr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 使用上下文 API

创建上下文对象。

```
export const StateContext = createContext();export const useStateValue = () => useContext(StateContext);
```

每个上下文对象都带有一个提供者 React 组件，该组件允许消费组件订阅上下文更改。

```
export const StateProvider = ({ reducer, initialState, children }) => (
  <StateContext.Provider value={useReducer(reducer, initialState)}>
    {children}
  </StateContext.Provider>
);
```

创建一个初始状态对象和 reducer，然后将应用程序组件包装在状态提供程序中。这样，所有组件都可以访问初始状态和还原状态。

```
<StateProvider initialState={initialState} reducer={reducer}>
      <App />
 </StateProvider>
```

减速器和分配器

```
const reducer = (state, action) => {

  switch (action.type) {
    case "SET_TOKEN":
      return {
        ...state,
        token: action.token
      };
    case "SET_ITEM":
      return {
        ...state,
        item: action.item
      }
    case "SET_SONG":
      return {
        ...state,
        curr_song: action.song
      }
    case "SET_PLAYING":
      return {
        ...state,
        playing: action.playing
      }
    case "SET_AUDIO":
    let newplaylist = state.subject_audio
    newplaylist[action.name].push({'title':action.title,'teacher':'ajay'})
    return{
      ...state,
      subject_audio: newplaylist
    }
    default:
        return state;};
}export default reducer;
```

减速器有两个参数，当前状态和动作。动作是通过 onclick 事件等组件来调度的。还原器创建更改并为状态提供者返回新的状态。

**派单示例:**

```
const [{ item,subject_audio }, dispatch] = useStateValue();const onHandleClick = (id)=>{
    dispatch({
      type: "SET_SONG",
      song: id
    });
  }
```

至此，我们应用程序的前端部分就完成了。完整的回购代码可以在下面的链接中找到。在下一篇文章中，我将展示如何为应用程序创建后端。

[](https://github.com/Ash-D23/Exam-Assistant-v2) [## ash-D23/考试助手-v2

### 这个项目是用 Create React App 引导的。在项目目录中，您可以运行:在…中运行应用程序

github.com](https://github.com/Ash-D23/Exam-Assistant-v2) 

谢谢你把文章看完。希望这是有帮助的！

**参考文献:**

[](https://reactjs.org/docs/getting-started.html) [## 开始行动-做出反应

### 用于构建用户界面的 JavaScript 库

reactjs.org](https://reactjs.org/docs/getting-started.html) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)