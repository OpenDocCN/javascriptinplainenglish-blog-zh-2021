# 在 React Web 应用程序中使用 Redux 和 Firestore

> 原文：<https://javascript.plainenglish.io/using-redux-and-firestore-in-your-react-web-app-eb38a9b316f8?source=collection_archive---------11----------------------->

![](img/676909466444ba3803780c54f02a9c3b.png)

Redux is a state management framework and Firestore is a NoSQL database provided by Google

# Redux

## 介绍

Redux 是 JavaScript 的一个状态管理工具，它使得在应用程序中维护状态变得更加简单。

它在 React 应用程序中特别有用，因为它可以让您避免通过许多不同的子组件向下传递道具的行为，直到它到达需要数据的深层嵌套组件。

相反，应用程序的所有状态信息都存储在一个叫做*的存储中。* [以下是关于如何在 React 应用中设置商店的指南](https://redux.js.org/faq/store-setup)

使用 Redux，一旦创建了一个商店，任何设置为使用 Redux 功能的组件都可以直接从商店中访问信息。再也不用担心传道具或者用回调更新家长了。Redux 的 MapStateToProps 和 MapDispatchToProps 函数(结合一个称为 reducer 的东西)将为您处理所有这些。

## mapStateToProps

mapStateToProps 函数确实如其名所示。它会将商店中您希望您的组件可以访问的任何商品映射到您的组件道具。这听起来可能令人困惑，但当你看到一个例子时，这并不太糟糕。

假设我们有一个叫做食品杂货的组件。我们想让我们的杂货组件访问应用程序状态中存储的所有杂货的当前列表。这些存在于名为 state.groceryList 的属性中。

```
// Groceries.jsfunction mapStateToProps(state) { const { groceryList } = state return { 
    fruits: groceryList.fruits
    veggies: groceryList.veggies
    dairy: groceryList.dairy
  }}export default connect(mapStateToProps)(Groceries)
```

mapStateToProps 函数被逐行传递一个表示整个 Redux 存储的参数“state”。

然后，使用 prop 析构将属性 groceryList 从状态中取出，并将其赋给一个也称为 groceryList 的变量。

从那里，mapStateToProps 的返回值表示将被添加到组件属性对象中的属性。因此，在上面的例子中，食品杂货将有 props.fruits、props.veggies 和 props.dairy，所有这些都被添加到由其父代传递到食品杂货中的任何其他属性中。

最后一行是什么赋予了食品杂货自我支撑的能力。connect 函数接受 1 或 2 个函数(在本例中，mapDispatchToProps 的第 2 个参数为空),然后将每个函数的返回值赋给杂货的 Props 对象。理论上，您可以随意调用这个函数，connect 仍然会将它的第一个参数的返回值赋给 props，但是约定是将其称为 mapStateToProps。

## mapDispatchToProps

mapDispatchToProps 函数做的事情与 mapStateToProps 非常相似，但它不是让您访问应用程序的状态，而是让您的组件函数称为 actions，用于更新 Redux 的状态。

它们通过将一个动作分派给一个称为 reducer 的文件来实现这一点。我将在下一节解释这个缩减器，所以现在，让我们把重点放在 mapDispatchToProps 函数上。

假设我们使用 redux 在应用程序的状态中存储一个用户名。第一次加载应用程序时，它可能还不知道你的名字，或者可能有一些其他功能需要你更改用户名。为了设置/更新这个 name 属性，我们需要使用一个 Redux 动作来更新商店。这就是 mapDispatchToProps 的用武之地。

我们将从实际执行名称更新的代码开始。

```
const setName = (name) => ({
  type: 'SET_NAME',
  name,
})
```

所以你要做的是传递给 setName 一个字符串，它表示名字应该是什么。然后，在组件的底部，您希望创建 mapDispatchToProps 函数，如下所示:

```
const mapDispatchToProps = (dispatch) => ({
  setName: (name) => dispatch(setName(name)),
})
```

上面的函数接受 dispatch 函数作为参数。然后这个函数返回一个带有 setName 属性的对象，它的值也是一个函数。setName 属性是一个函数，它接受一个 Name 参数，然后传递我们在第一个代码块中定义的 setName 函数作为调度函数的参数。这些都将被映射到组件的 props，所以您可以通过调用 props.setName 来访问这个函数。

然后，dispatch 将 setName(name)函数的返回发送给 rootReducer。请记住，setName(name)的返回值是一个具有“SET_Name”类型属性和传递给它的名称字符串的 NAME 属性的对象。

## 还原剂

缩减器是由一堆 switch-case 语句组成的。如果它所传递的动作的类型属性与其中一种情况相匹配，您将在 case 语句中找到相应的代码。同样，这很难用语言来解释，所以我们来看一个例子:

```
const name = (state = '', action) => {
  switch(action.type) {
    case 'SET_NAME':
      return action.name;
    default :
       return state;
  }
}
```

继续以 setName 为例，我们的 reducer 被传递了 setName 操作，它的类型是‘SET _ NAME’。因为 action.type 与我们的 reducer 中的“SET_NAME”的大小写相匹配，所以我们的 reducer 将返回 action.name，它是包含我们想要保存在 Redux 存储中的名称的字符串。

现在，如果您查看 Redux 的 state.name 属性，它将是 setName 传递给它的任何名称。所以综合起来看:

```
//calling:props.setName('Chris')//results in dispatch calling:dispatch(setName('Chris'))//which then is passed to our reducer as:const name = ('', {type: 'SET_NAME', name: 'Chris'})//when ends up setting store.state.name = 'Chris'
```

## 连接

让所有这些动作、状态变量和 reducer 一起工作的最后一步是方便的 connect 函数。Connect 是 Redux 提供的一个函数(记得从你的组件顶部的‘react-Redux’导入)包装你的组件，并允许它有效地传递自身 props。

Connect 最多接受 4 个可选参数，但它们必须按照定义的顺序。今天我们只关注前两个，即 mapStateToProps 和 mapDispatchToProps。

```
import { connect } from 'react-redux'const connectToStore = connect(mapStateToProps, mapDispatchToProps)
const ConnectedComponent = connectToStore(Component)
```

上述函数将把 mSP 和 mDP 的返回值映射到组件的 props。connect 返回另一个函数，该函数接受组件应该作为参数包装。

实际上，您通常会看到它在一个步骤中完成，如下所示:

```
connect(mapStateToProps, mapDispatchToProps)(Component)
```

这和上面的两行完全一样，但是更清晰，而且通常是预期的语法，所以一定要以这种方式学习。

您并不总是希望 mapStateToProps 和 mapDispatch 都支持您的组件，因此两者都不是必需的。如果您只想要 mapStateToProps，您只能传递一个参数，如下所示:

```
connect(mapStateToProps)(Component)
```

但是，如果您只需要 mapDispatchToProps，因为 connect 期望 mapStateToProps 作为第一个参数，所以您需要在第一个槽中传递 null，如下所示:

```
connect(null, mapDispatchToProps)(Component)
```

# Firestore

你可以在 React 应用中安装一个非常有用的包来使用 Redux 和 Firebase，这个包的名字叫做 [react-redux-firebase](http://react-redux-firebase.com/docs/getting_started) 。

## firestoreConnect

react-redux-firebase npm 提供了一个名为 firestoreConnect 的高阶功能，允许您使用 react 的生命周期挂钩来监听/取消监听 Firestore 的更新。

假设您在 Firestore 中有一个聊天和消息的数据库，您希望听到任何更改，以便重新呈现您的应用程序。您可以使用 firestoreConnect 并向它传递一个数组，其中包含您想要监听的路径。它看起来会像这样:

```
firestoreConnect(() => ['todos']), // sync todos collection from Firestore into redux
```

一个更复杂的版本甚至可能是这样的:

```
firestoreConnect((props) => [ {
    collection: "chats",
    doc: props.match.params.chatId,
    subcollections: [
      {
      collection: "messages",
      orderBy: ["timestamp", "desc"],
      },
    ], limit: props.convLimit storeAs: "conversation_" + props.match.params.chatId, },
])
```

您现在可以直接在 Redux 中从 Firestore 访问所有这些收藏和文档。

# 将这一切结合在一起

最后，为了让所有这些不同的部分协同工作，我们将使用 Redux 库提供的一个名为 compose 的函数。

## 构成

compose 允许您以一种清晰的语法将多个“存储增强器”串在一起，而不必将它们作为参数互相传递。使用 connect with firestoreConnect 时，您需要以下语法:

```
export default compose( connect(mapStateToProps, mapDispatchToProps),
  firestoreConnect(() => ['todos']))(Component);
```

现在，您已经将 mapStateToProps、mapDispatchToProps 和 fireStoreConnect 的所有功能连接到了您的组件！

*更多内容尽在*[plain English . io](http://plainenglish.io/)