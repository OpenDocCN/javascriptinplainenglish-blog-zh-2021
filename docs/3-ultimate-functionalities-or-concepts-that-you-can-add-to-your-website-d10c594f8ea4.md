# 3 个终极功能或概念，你可以添加到你的网站

> 原文：<https://javascript.plainenglish.io/3-ultimate-functionalities-or-concepts-that-you-can-add-to-your-website-d10c594f8ea4?source=collection_archive---------21----------------------->

## 您将了解搜索功能、三元运算符中的多个条件以及简单易用。

![](img/9ef9d3bc3825a8656014c77fb634b386.png)

Source: [Pexels](https://www.pexels.com/photo/adult-displeased-businesswoman-with-papers-in-light-modern-office-3808822/)

嗯，您可能已经使用了 map、filter、slice、三元运算符和许多其他 JavaScript 方法。

但是你们大多数人还没有学会如何从中获得更多。简而言之，在本文中，您将学习如何以更精确的方式使用上述 JavaScript 方法。

它可以是任何事情，比如创建功能或学习更多的相关知识。然后我们将学习 Redux 的替代方案。

在这里，我不会谈论简单的方法，

```
var num = [1, 2, 3, 4, 5];var newarray = num.map((number) => number * 10);
console.log(newarray);//The output will be
[10, 20, 30, 40, 50]
```

但我们将使用这种方法来创建我们的网站功能。我知道你们中的一些人对数组方法没有概念，所以你们可以[阅读这个](/5-javascript-array-methods-that-you-will-use-often-bdd1c96ac8c7)然后再回来。

> **注意**:在这里，我不会给你提供完整的代码。你必须自己去做。但是我会教你，给你解释背后的概念。

# **1。搜索功能**

现在我们开始吧。

![](img/964fadfcb2c184bf90e8cbbbd83b77cb.png)

Photo by [Edho Pratama](https://unsplash.com/@edhoradic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

互联网上的几个网站都包含搜索功能。你们中的许多人希望在自己的网站上实现它。

这就是了，

首先，您必须[获取数据](/display-api-data-using-axios-in-a-react-app-with-hooks-eb9ca298f27)，您必须在其中应用搜索功能。例如，它可能是用户的名字，当然也可能是类似的名字。

如果它存在于后端，请使用 Axios。并将它保存在钩子或类中的状态中。

假设您已经通过 setCourses 将数据保存在一个函数钩子中。

```
import { useState, useEffect } from "react";const [courses, setCourses] = useState(''); 
```

并创建另一个函数挂钩来添加用户输入数据，

```
const [search, setSearch] = useState('');
```

输入会是这样的，

```
<div><input className="bg-grey-lightest border-none text-black p-2 rounded-lg xl:w-80 w-auto" placeholder="Search Courses"type="text"onChange={(e) => setSearch(e.target.value)} /></div>
```

在这里，为了样式化，我使用了 TailwindCSS 来保持简单。你可以任意选择。

然后创建一个方法来添加搜索功能，

```
const filterCourse = courses.filter((course) => {return course.title.toLowerCase().includes(search.toLowerCase());});
```

它将通过将课程数据转换为小写并将其与转换为小写的搜索数据进行匹配来过滤课程数据。

像这样展示它，

```
<ul class="absolute w-full text-black pt-1">{filterCourse.map((data, id) => (<li key={id}><a class="bg-white py-1 px-2 block" href="#">{data.name}</a></li>))}</ul>
```

但是等待，当你想看到无序列表后，只有用户将输入超过 2 个字母。

你会怎么做？

从字面上看，我已经搜索了很多，解决方案是足够简单的。使用带有条件的三元运算符。

```
<ul class="absolute w-full text-black pt-1">{**search.length > 2 ?** filterCourse.map((data, id) => (<li key={id}><a class="bg-white py-1 px-2 block" href="#">{data.name}</a></li>))**: " "**}</ul>
```

所以它只会在搜索长度超过 2 个字母后显示列表。

是不是很酷？嗯，比我们想象的要多。

[](/stop-using-css-and-bootstrap-use-tailwind-css-instead-94c689ec3b8a) [## 停止使用 CSS 和 Bootstrap，改用 Tailwind CSS

### 顺风 CSS 给你更多的灵活性，节省你的时间。

javascript.plainenglish.io](/stop-using-css-and-bootstrap-use-tailwind-css-instead-94c689ec3b8a) 

# 2.**三元运算符中的多重条件**

从字面上看，在一周之前，我不知道这件事。我知道我们可以像 if-else 条件一样使用三元运算符。

但是如果有多个条件或者有几个 else-if 的条件呢？

你会怎么做？一周之前我一点概念都没有。

但是您可以使用三元运算符来实现。

但是怎么做呢？

我从堆栈溢出中学到了这一点。

```
var yourVar = condition1 ? someValue
            : condition2 ? anotherValue
            : defaultValue;
```

在反应中你可以这样使用，

```
{condition1 ? someValue : condition2 ? anotherValue: defaultValue; }
```

它将帮助您在三元运算符中添加多个条件。

大多数专家建议不要在你的项目中大量使用多重条件三元运算符。所以尽量只在需要的时候使用。

# 3.**用 Easy Peasy 代替 Redux**

当我们有一个大规模的应用程序时，我们必须在 React 或任何其他框架中使用一些状态管理工具。

但是当我们有[容易的和平](https://www.npmjs.com/package/easy-peasy)的时候为什么要放弃呢？

Redux 有很多样板代码，让我们(开发人员)有点不知所措，而 Easy-Peasy 没有。

在此之前，我的项目每次都使用 Redux。但实际上，它包含了很多样板文件，让我效率低下。

这是我使用 Easy Peasy 的唯一原因。

在学习和实现了 Easy-peasy 之后，我已经在我的项目中尝试过了，效果很好。你也可以使用 React Context，这是最重要的一个。

所以，我想帮助你提高你的生产力。原因只有一个，用不用完全是你自己的选择。

为了更好的解释，我在这里举一个[官方文件的例子](https://www.npmjs.com/package/easy-peasy)。

**a)首先，创建一个商店:**

很简单，你必须创建一个文件，并在其中创建一个商店。商店将包含从创建商店、定义状态甚至动作的所有内容。

```
const store = createStore({
  todos: {
    items: ['Create store', 'Wrap application', 'Use store'],
    add: action((state, payload) => {
      state.items.push(payload);
    }),
  },
});
```

所以在这里，我们用状态和动作定义了一个商店。

**b)用商店包装你的应用程序**

```
function App() {
  return (
    <StoreProvider store={store}>
      <TodoList />
    </StoreProvider>
  );
}
```

**c)使用商店**

现在，您可以在任何组件中使用存储，甚至可以通过下面的代码访问状态和动作。

```
function TodoList() {
  const todos = useStoreState((state) => state.todos.items);
  const add = useStoreActions((actions) => actions.todos.add);
  return (
    <div>
      {todos.map((todo, idx) => (
        <div key={idx}>{todo}</div>
      ))}
      <AddTodo onAdd={add} />
    </div>
  );
}
```

是的，它用更少的代码以一种简单的方式类似于 Redux。

你也可以从这里了解更多信息— [停止使用 Redux——如果你需要的话，请考虑 Easy Peasy](https://betterprogramming.pub/stop-using-redux-consider-easy-peasy-if-you-want-3214c41bcce5)。

现在是你选择用还是不用的时候了，我只是给你提供了另一个选择。

# 让我们结束吧

这些概念对于一个 Web 开发者来说是至关重要的，我必须用最简单的方式来解释它们。

我想，我已经做到了。

就这样——谢谢。

[](/6-free-tools-that-helped-me-become-an-expert-web-developer-41b999403865) [## 6 个免费工具，帮助我成为一名专业的网络开发人员

### 由一位拥有 30 多年经验的 web 开发人员建议。

javascript.plainenglish.io](/6-free-tools-that-helped-me-become-an-expert-web-developer-41b999403865) [](/how-to-learn-web-development-using-free-resources-1c677e70de14) [## 如何利用免费资源学习 Web 开发

### 初学者的深入指南。

javascript.plainenglish.io](/how-to-learn-web-development-using-free-resources-1c677e70de14) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)