# 用 React 和 JavaScript 创建一个随机引用文本生成器

> 原文：<https://javascript.plainenglish.io/create-a-random-quote-text-generator-with-react-and-javascript-4d6a54ac3d4a?source=collection_archive---------17----------------------->

![](img/9631eb5c957eee25b1acd3ab7f0c6c80.png)

Photo by [Max Böhme](https://unsplash.com/@max_thehuman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个随机引用文本生成器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app quote-text-generator
```

和 NPM 一起创建我们的 React 项目。

# 创建随机报价文本生成器

为了创建随机报价文本生成器，我们编写:

```
import { useState } from "react";const quotes = [
  {
    quote:
      "One of my most productive days was throwing away 1,000 lines of code.",
    cite: "Ken Thompson"
  },
  {
    quote:
      "I have always wished for my computer to be as easy to use as my telephone; my wish has come true because I can no longer figure out how to use my telephone.",
    cite: "Bjarne Stroustrup"
  },
  {
    quote: "When in doubt, use brute force.",
    cite: "Ken Thompson"
  },
  {
    quote: "Talk is cheap. Show me the code.",
    cite: "Linus Torvalds"
  },
  {
    quote:
      "Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live.",
    cite: "Martin Golding"
  },
  {
    quote:
      "Most good programmers do programming not because they expect to get paid or get adulation by the public, but because it is fun to program.",
    cite: "Linus Torvalds"
  },
  {
    quote:
      "Most software today is very much like an Egyptian pyramid with millions of bricks piled on top of each other, with no structural integrity, but just done by brute force and thousands of slaves.",
    cite: "Alan Kay"
  },
  {
    quote:
      "Most of you are familiar with the virtues of a programmer. There are three, of course: laziness, impatience, and hubris",
    cite: "Larry Wall"
  },
  {
    quote:
      "First learn computer science and all the theory. Next develop a programming style. Then forget all that and just hack.",
    cite: "George Carrette"
  }
];
export default function App() {
  const [index, setIndex] = useState(); const generate = () => {
    const index = Math.floor(Math.random() * quotes.length);
    setIndex(index);
  }; return (
    <div className="App">
      <button onClick={generate}>generate</button>
      <p>{quotes[index] && quotes[index].quote}</p>
      <p>{quotes[index] && quotes[index].cite}</p>
    </div>
  );
}
```

我们在报价生成器中选择了一组`quotes`。

我们用一个按钮返回 JSX，当我们点击它时，这个按钮运行`generate`。

在`generate`函数中，我们调用`Math.random`来生成一个介于 0 和 1 之间的数字。

然后我们把它乘以`quotes.length`，然后用`Math.floor`把它四舍五入到最接近的整数，得到指数。

最后，我们用`p`元素来呈现选择。

在呈现每个属性值之前，我们检查是否定义了`quotes[index]`。

# 结论

我们可以用 React 和 JavaScript 创建一个随机引用文本生成器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)