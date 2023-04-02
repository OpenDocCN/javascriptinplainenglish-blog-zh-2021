# 用 React 和 JavaScript 创建一个预算跟踪程序

> 原文：<https://javascript.plainenglish.io/create-a-budget-tracker-app-with-react-and-javascript-c600a93cfa94?source=collection_archive---------13----------------------->

![](img/7bbb6c9bfa7fb2fb99fc0436e6e45a6d.png)

Photo by [StellrWeb](https://unsplash.com/@stellrweb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个预算跟踪器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app budget-tracker
```

和 NPM 一起创建我们的 React 项目。

我们需要`uuid`来让我们轻松地为我们的预算项目创建唯一的 id。

要添加它，我们运行:

```
npm i uuidv4
```

# 创建购物清单应用程序

为了创建购物清单应用程序，我们编写:

```
import { useMemo, useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [budget, setBudget] = useState("");
  const [expense, setExpense] = useState({});
  const [expenses, setExpenses] = useState([]); const add = (e) => {
    e.preventDefault();
    const { cost, description } = expense;
    const formValid = +budget > 0 && +cost > 0 && description;
    if (!formValid) {
      return;
    }
    setExpenses((ex) => [
      ...ex,
      {
        id: uuidv4(),
        ...expense
      }
    ]);
  }; const remove = (index) => {
    setExpenses((expenses) => expenses.filter((_, i) => i !== index));
  }; const remainingBudget = useMemo(() => {
    const totalExpenses = expenses
      .map(({ cost }) => +cost)
      .reduce((a, b) => +a + +b, 0);
    return budget - totalExpenses;
  }, [budget, expenses]); return (
    <div className="App">
      <div>
        <form>
          <fieldset>
            <label>budget</label>
            <input value={budget} onChange={(e) => setBudget(e.target.value)} />
          </fieldset>
        </form> <form onSubmit={add}>
          <h1>add expensse</h1>
          <fieldset>
            <label>description</label>
            <input
              value={expense.description}
              onChange={(e) =>
                setExpense((ex) => ({ ...ex, description: e.target.value }))
              }
            />
          </fieldset> <fieldset>
            <label>cost</label>
            <input
              value={expense.cost}
              onChange={(e) =>
                setExpense((ex) => ({ ...ex, cost: e.target.value }))
              }
            />
          </fieldset>
          <button type="submit">add expense</button>
        </form> <p>remaining budget: ${remainingBudget}</p> {expenses.map((ex, index) => {
          return (
            <div key={ex.id}>
              {ex.description} - ${ex.cost}
              <button onClick={() => remove(index)}>remove</button>
            </div>
          );
        })}
      </div>
    </div>
  );
}
```

我们有`budget`、`expense`和`expenses`状态。

`budget`有预算数。

`expense`有费用项。

`expenses`有费用项目。

然后添加`add`方法，让我们添加一个费用项目。

在其中，我们调用`e.preventDefault()`来让我们向客户端提交。

然后我们检查`expense`属性对于`formValid`变量是否有效。

如果是`true`，那么我们用一个回调函数调用`setExpenses`来返回一个`expenses`数组，新的条目附加在上面。

在`remove`方法中，我们用回调函数调用`setExpenses`，该回调函数返回不带给定`index`项的`expenses`数组。

接下来，我们添加用`useMemo`创建的`remainingBudget`状态。

在回调中，我们将来自`expenses`数组的所有`cost`值加在一起得到`totalExpenses`。

然后我们用`totalExpenses`减去`budget`。

我们观察`budget`和`expenses`的变化，如第二个参数中的数组所示。

在`return`语句中，我们有一个表单让我们输入`budget`值。

在第二个表单中，我们可以输入`expense`属性的值。

我们设置了`value`和`onChange`道具，这样我们就可以设置属性了。

为了用输入设置一个属性值，我们使用 spread 来扩展返回对象中的现有值，然后我们将我们想要更改的属性添加到最后的`e.target.value`。

在那下面，我们显示`remainingBudget`值。

在下面，我们将`expenses`项目显示为 div。

当我们点击按钮时，里面的按钮用`index`调用`remove`来删除一个项目。

# 结论

我们可以用 React 和 JavaScript 创建一个简单的预算应用程序。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)