# 用 React 和 JavaScript 创建一个食谱应用程序

> 原文：<https://javascript.plainenglish.io/create-a-recipe-app-with-react-and-javascript-88c37b93435f?source=collection_archive---------30----------------------->

![](img/8597c299fe1d4a0d1692fb5cc80c9daf.png)

Photo by [Ryan Kwok](https://unsplash.com/@milkbox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个食谱应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app recipe-app
```

和 NPM 一起创建我们的 React 项目。

我们还需要`uuid`包来为我们的食谱项目生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建食谱应用程序

为了创建食谱应用程序，我们编写:

```
import React, { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [recipe, setRecipe] = useState({
    name: "",
    ingredients: "",
    steps: ""
  });
  const [recipes, setRecipes] = useState([]); const addRecipe = (e) => {
    e.preventDefault();
    const { name, ingredients, steps } = recipe;
    const formValid = name && ingredients && steps;
    if (!formValid) {
      return;
    }
    setRecipes((recipes) => [
      ...recipes,
      {
        id: uuidv4(),
        ...recipe
      }
    ]);
  }; const deleteRecipe = (index) => {
    setRecipes((recipes) => recipes.filter((_, i) => i !== index));
  }; return (
    <div>
      <style>
        {`
        .content {
          white-space: pre-wrap;
        }
        `}
      </style>
      <form onSubmit={addRecipe}>
        <div>
          <label>name</label>
          <input
            value={recipe.name}
            onChange={(e) =>
              setRecipe((recipe) => ({ ...recipe, name: e.target.value }))
            }
          />
        </div>
        <div>
          <label>ingredients</label>
          <input
            value={recipe.ingredients}
            onChange={(e) =>
              setRecipe((recipe) => ({
                ...recipe,
                ingredients: e.target.value
              }))
            }
          />
        </div>
        <div>
          <label>steps</label>
          <textarea
            value={recipe.steps}
            onChange={(e) =>
              setRecipe((recipe) => ({ ...recipe, steps: e.target.value }))
            }
          ></textarea>
        </div>
        <button type="submit">add recipe</button>
      </form>
      {recipes.map((r, index) => {
        return (
          <div key={r.id}>
            <h1>{r.name}</h1>
            <h2>ingredients</h2>
            <div className="content">{r.ingredients}</div>
            <h2>steps</h2>
            <div className="content">{r.steps}</div>
            <button className="button" onClick={() => deleteRecipe(index)}>
              delete
            </button>
          </div>
        );
      })}
    </div>
  );
}
```

我们有用于存储表单数据的`recipe`状态。

`recipes`有食谱条目。

然后我们定义`addRecipe`函数，让我们添加一个食谱。

在它里面，我们调用`e.preventDefault()`来做客户端表单提交。

然后我们检查`name`、`ingredients`和`steps`是否被设置。

如果是，那么我们调用`setRecipes`来添加条目。

我们传入一个回调函数，它接受现有的`recipes`值，然后我们返回它的一个副本，并带有一个在末尾有新条目的对象。

我们调用`uuidv4`为新条目返回一个惟一的 ID。

`deleteRecipe`函数用一个接受现有`recipes`的回调来调用`setRecipes`。然后它返回它的一个副本，在给定的`index`处没有条目。

在此之下，我们添加了`style`元素来设置步骤的样式。

当我们点击类型为`submit`的按钮时，我们将`onSubmit`属性设置为`addRecipe`的表单添加一个条目。

在表单内部，我们有带`onChange`属性的输入，这些属性被设置为调用`setRecipe`的函数，以将输入值设置为`recipe`对象中的一个属性。

在表单下面，我们将`recipes`值呈现在一个 div 中。

在它里面，我们显示了`name`、`ingredients`和`steps`。

在那下面，我们有一个按钮，当我们点击它时，它会用`index`调用`deleteRecipe`。

# 结论

我们可以用 React 和 JavaScript 创建一个食谱应用。

*更多内容看*[***plain English . io***](http://plainenglish.io)