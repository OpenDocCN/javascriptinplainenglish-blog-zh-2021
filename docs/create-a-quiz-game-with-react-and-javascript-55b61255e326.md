# 用 React 和 JavaScript 创建一个问答游戏

> 原文：<https://javascript.plainenglish.io/create-a-quiz-game-with-react-and-javascript-55b61255e326?source=collection_archive---------21----------------------->

![](img/479758953ced8162ebe3e488c8cbaaab.png)

Photo by [Shubham Sharan](https://unsplash.com/@shubhamsharan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个加法游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app quiz-game
```

和 NPM 一起创建我们的 React 项目。

# 创建问答游戏

为了创建问答游戏，我们编写:

```
import React, { useState } from "react";const questions = [
  {
    question: "What is American football called in England?",
    choices: ["American football", "football", "Handball"],
    rightAnswer: "American football"
  },
  {
    question: "What is the largest country in the world?",
    choices: ["Russia", "Canada", "United States"],
    rightAnswer: "Russia"
  },
  {
    question: "What is the 100th digit of Pi?",
    choices: ["9", "4", "7"],
    rightAnswer: 9
  }
];export default function App() {
  const [score, setScore] = useState(0);
  const [questionIndex, setQuestionIndex] = useState(0);
  const [answer, setAnswer] = useState(""); const restart = () => {
    setScore(0);
    setAnswer("");
    setQuestionIndex(0);
  }; const submit = (e) => {
    e.preventDefault();
    if (answer === questions[questionIndex].rightAnswer) {
      setScore((score) => score + 1);
    } if (questionIndex < questions.length) {
      setQuestionIndex((i) => i + 1);
    }
  };if (questionIndex < questions.length) {
    return (
      <div>
        <label>{questions[questionIndex].question}</label>
        {questions[questionIndex].choices.map((c, i) => {
          return (
            <div>
              <input
                type="radio"
                name="choice"
                value={c}
                onChange={(e) => setAnswer(e.target.value)}
                checked={answer === c}
              />
              {c}
            </div>
          );
        })}
        <button type="button" onClick={submit}>
          check
        </button>
        <p>score: {score}</p>
      </div>
    );
  } else {
    return (
      <form>
        <div v-else>
          <button type="button" onClick={restart}>
            restart
          </button>
        </div>
        <p>score: {score}</p>
      </form>
    );
  }
}
```

我们有一个带有`question`、`choices`和`rightAnswer`属性的`questions`数组，分别包含问题、问题的选项和问题的正确答案。

然后在`App`中，我们用`useState`创建了`score`、`questionIndex`和`answer`状态。

`answer`是玩家选择的答案。

在那下面，我们有`submit`函数，我们调用`e.preventDefault()`来做客户端表单提交。

然后我们检查我们的`answer`选择是否与`rightAnswer`相同。

如果是，那么我们调用`setScore`来增加分数。

如果`questionIndex`小于`questions.length`，这意味着我们有更多的问题要显示。

因此，我们调用`setQuestionIndex`通过回调来增加分数，该回调返回原始索引`i`加 1。

接下来，我们有一个`if`语句，它对`submit`函数中的`if`进行同样的检查。

如果`questionIndex`小于`questions.length`，我们应该用单选按钮提问供玩家选择答案。

我们设置`checked`属性来设置单选按钮为选中。

我们通过比较`answer`值和`c`值来确定哪个被检查。

`onChange`让我们用一个调用`setAnswer`来设置选择的函数来设置选择。

在那下面，我们显示 check 按钮，当我们点击它时，它调用`submit`来提交答案。

然后我们显示下面的`score`。

如果`if`条件为`false`，我们显示重启按钮，调用`restart`重置所有值。

我们还展示了下面的`score`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个问答游戏。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)