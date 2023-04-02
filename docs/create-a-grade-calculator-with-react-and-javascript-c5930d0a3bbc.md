# 用 React 和 JavaScript 创建一个分数计算器

> 原文：<https://javascript.plainenglish.io/create-a-grade-calculator-with-react-and-javascript-c5930d0a3bbc?source=collection_archive---------16----------------------->

![](img/421f42cc04d0866996c1c58c35962352.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个分数计算器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app grade-calculator
```

和 NPM 一起创建我们的 React 项目。

此外，我们必须安装`uuid`包，让我们为每个成绩条目分配唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建等级计算器

为了创建分数计算器，我们编写:

```
import React, { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [grades, setGrades] = useState([{ id: uuidv4(), value: 0 }]);
  const [average, setAverage] = useState(0); const addGrade = () => {
    setGrades((grades) => [...grades, { id: uuidv4(), value: 0 }]);
  }; const deleteGrade = (index) => {
    setGrades((grades) => grades.filter((_, i) => i !== index));
  }; const calculate = (e) => {
    e.preventDefault();
    const formValid = grades.every(({ value }) => !isNaN(+value));
    if (!formValid) {
      return;
    }
    setAverage(
      grades.map(({ value }) => value).reduce((a, b) => +a + +b, 0) /
        grades.length
    );
  }; return (
    <div className="App">
      <form onSubmit={calculate}>
        {grades.map((g, i) => {
          return (
            <div key={g.id}>
              <label>grade</label>
              <input
                value={g.value}
                onChange={(e) => {
                  const grds = [...grades];
                  grds[i].value = e.target.value;
                  setGrades(grds);
                }}
              />
              <button type="button" onClick={() => deleteGrade(i)}>
                delete grade
              </button>
            </div>
          );
        })} <button type="button" onClick={addGrade}>
          add grade
        </button>
        <button type="submit">calculate average</button>
      </form>
      <div>Your average grade is {average}</div>
    </div>
  );
}
```

我们最初将`grades`状态集定义为一个只有一个条目的数组。

然后我们定义保持平均成绩的`average`州。

`addGrade`功能让我们添加一个等级条目。

在其中，我们用回调函数调用了`setGrades`,该回调函数返回一个在末尾有新条目的`grades`数组的副本。

`id`被设置为`uuidv4`的返回值，以设置唯一 ID。

然后我们创建`deleteGrade`函数，该函数调用带有回调的`setGrades`，该回调返回没有给定`index`的`grades`数组，以从`grades`数组中移除给定的条目。

`calculate`函数计算平均值。

在其中，我们调用`e.preventDefault()`进行客户端表单提交。

然后我们检查每个`grade`条目的每个`value`属性是否是一个数字。

如果是，那么我们用一个表达式调用`setAverage`来计算平均值。

我们将`grades`映射到一个只有`value`值的数组。

然后我们调用该数组上的`reduce`将所有的值加在一起，并用回调函数返回。

`reduce`的第二个参数有初始返回值。

在那下面，我们有一个将`onSubmit`属性设置为`submit`的表单来提交表单。

在其中，我们将`grades`数组呈现为一个输入。

将`key`属性设置为`g.id`以将其设置为唯一的 ID，这样 React 就可以跟踪条目。

将`value`设置为`g.value`。

在`onChange`回调中，我们复制了`grades`。然后我们将给定索引的`grades`条目的`value`设置为`e.target.value`。

`e.target.value`有输入值。

然后我们调用`setGrades`用最新的值更新`grades`数组。

在那下面，我们有删除等级按钮，当我们点击它的时候调用`deleteGrade`。

在输入下方，我们有“添加等级”和“计算平均值”按钮。

当我们点击 add grade 按钮时，它会调用`addGrade`。

计算平均值按钮触发`submit`事件，因为它具有类型`submit`。

在表格下方，我们显示了`average`等级值。

# 结论

我们可以用 React 和 JavaScript 创建一个成绩计算器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)