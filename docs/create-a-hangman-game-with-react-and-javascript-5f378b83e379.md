# 用 React 和 JavaScript 创建一个刽子手游戏

> 原文：<https://javascript.plainenglish.io/create-a-hangman-game-with-react-and-javascript-5f378b83e379?source=collection_archive---------20----------------------->

![](img/86422aaca073c94709e6c4eb5ab73f1e.png)

Photo by [Irene Strong](https://unsplash.com/@leirenestrong?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个刽子手游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app hangman
```

和 NPM 一起创建我们的 React 项目。

# 创建刽子手游戏

为了创建刽子手游戏，我们编写:

```
import React, { useMemo, useState } from "react";export default function App() {
  const [answer] = useState("hangman");
  const [guesses, setGuesses] = useState([]);
  const [guessLetter, setGuessLetter] = useState("");
  const guessesLeft = useMemo(() => {
    return (
      6 -
      guesses.filter((g) => {
        return !answer.includes(g);
      }).length
    );
  }, [answer, guesses]); const lettersToShow = useMemo(() => {
    return answer.split("").map((a) => {
      if (guesses.includes(a)) {
        return a;
      }
      return "_";
    });
  }, [answer, guesses]); const isWin = useMemo(() => {
    const includedLetters = guesses.filter((g) => {
      return answer.includes(g);
    });
    return answer.split("").every((a) => {
      return includedLetters.includes(a);
    });
  }, [answer, guesses]); const guess = (e) => {
    e.preventDefault();
    const formValid = /[a-z]{1}/.test(guessLetter);
    if (!formValid) {
      return;
    }
    setGuesses((guesses) => [...guesses, guessLetter]);
    setGuessLetter("");
  }; const reset = () => {
    setGuesses([]);
    setGuessLetter("");
  }; if (isWin) {
    return (
      <div className="App">
        you win
        <button type="button" onClick={reset}>
          reset
        </button>
      </div>
    );
  } else {
    if (guessesLeft > 0) {
      return (
        <div>
          <p>guesses left: {guessesLeft}</p>
          <form onSubmit={guess}>
            <div>
              <label>guess</label>
              <input
                value={guessLetter}
                onChange={(e) => setGuessLetter(e.target.value)}
              />
            </div>
            <button type="submit">guess</button>
          </form>
          {lettersToShow.map((l, i) => {
            return <span>{l}</span>;
          })}
        </div>
      );
    } else {
      return (
        <div>
          you lost
          <button type="button" onClick={reset}>
            reset
          </button>
        </div>
      );
    }
  }
}
```

`answer`状态有正确答案。

`guesses`有一个我们已经猜到的字母数组。

`guessLetter`把我们输入的字母输入到猜测输入里了。

接下来，我们用`useMemo`创建几个变量。

我们通过从 6 中减去不在`answer`单词中的猜测字母的数量来计算回调中的`guessesLeft`。

我们观察`answer`和`guesses`，这样无论何时它们被更新，返回值都会被更新。

同样，我们通过将`answer`拆分成字母来创建`lettersToShow`状态。

然后，如果猜测的字母在`answer`中，我们返回该字母。

否则，我们返回一个下划线。

这让我们可以显示到目前为止猜对了什么。

`isWin`变量有一个布尔值来表示玩家是否赢了。

我们创建`includedLetters`来获取包含`guesses`数组中的字母的字母，这些字母包含在`answer`中。

如果`includedLetters`中的每个字母都在拆分后的`answer`字符串中，我们返回。

这让玩家知道是否已经猜出了`answer`单词中的所有字母。

`guess`功能让玩家输入猜测。

在其中，我们调用`e.preventDefault()`来做客户端提交。

然后，我们检查玩家是否在输入框中输入了字母，然后将猜测的字母添加到`guesses`数组中。

为此，我们用回调函数调用`setGuesses`,该回调函数返回一个数组，其中包含现有的`guesses`和猜测出最新字母的`guessLetter`。

我们还将`setGuessLetter`设置为空字符串来清空输入框。

`reset`功能将`guesses`和`guessLetter`重置为其原始值。

然后我们检查是`isWin`是`true`。

如果是，那么我们呈现“你赢了”消息和一个重置按钮。

当我们点击这个按钮时，它会调用`reset`。

否则，如果`guessLeft`大于 0，这意味着玩家可以继续猜下去。

我们呈现了`guessesLeft`值和表单。

在表单中，我们呈现一个设置`guessLetter`的输入。

`onChange` prop 有一个函数，它获取具有输入值的`e.target.value`来设置它。

由于`onSubmit`属性，当我们点击 guess 时，运行`guess`功能。

在那下面，我们显示`lettersToShow`。

在`eise`块中，我们显示“你输了”,此时玩家`guessesLeft`为 0，这意味着不再有猜测。

我们还在那里显示了重置按钮。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个刽子手游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)