# 创建反应计时器

> 原文：<https://javascript.plainenglish.io/react-timer-7bbb321cbb4f?source=collection_archive---------17----------------------->

![](img/a2b0a682e36b4527a3eb1fe5c388d251.png)

Photo by [Marcelo Leal](https://unsplash.com/@marceloleal80?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我决定在 React 中练习使用音程。上周，我做了一个秒表，然后我马上想到要做一个计时器。它真的很像秒表，只是它是倒着走的。所以，我想我应该试一试。虽然它看起来就像秒表一样简单，但是建造一个计时器有它自己的挑战。

我使用 React 钩子来让这个组件工作。所以，首先，我设置了一个时间和开始状态。时间的默认值为零，开始的默认值为 false。这就是它的样子。

```
const [time, setTime] = useState(0);
const [start, setStart] = useState(false);
```

为了让 time 以秒、分、小时显示时间，我使用了一种非常类似于秒表的方法。我们对时间值应用一些数学运算，并将数字切片，使其显示为两位数。这是它看起来的样子。

```
let seconds = ("0" + (Math.floor((time / 1000) % 60) % 60)).slice(-2);
let minutes = ("0" + Math.floor((time / 60000) % 60)).slice(-2);
let hours = ("0" + Math.floor((time / 3600000) % 60)).slice(-2);
```

现在我们将使用我们的 useEffect 钩子用一个间隔从每秒钟的时间中减去 10。当 start 的值改变时，这个钩子将运行。如果 start 为 true，间隔将运行，如果 start 为 false，间隔将被清除。

```
useEffect(() => { let interval = null; if (start) { interval = setInterval(() => { if (time > 0) { setTime(prevTime => prevTime - 10) } }, 10) } else { clearInterval(interval); } return () => { clearInterval(interval) }}, [start])
```

为了设置计时器，我创建了一些按钮来增加时间。每个按钮将增加一小时、一分钟或一秒钟。这对于递减也是一样的。为了实现这一点，我创建了一个接受输入的函数。如果计时器尚未启动，时间可以根据按下的按钮增加。

```
function adjustTimer(input) { if (!start) { switch (input) { case "incHours": setTime(prevTime => prevTime + 3600000) break; case "incMinutes": setTime(prevTime => prevTime + 60000) break; case "incSeconds": setTime(prevTime => prevTime + 1000) break; case "decHours": setTime(prevTime => prevTime - 3600000) case "decMinutes": setTime(prevTime => prevTime - 60000) break; case "decSeconds": setTime(prevTime => prevTime - 1000) break; default: break; } }}
```

这就是为我们提供计时器主要功能的所有逻辑。现在我们只需要将所有这些渲染到我们的屏幕上。时间显示将位于一组按钮之间，有助于增加和减少时间。还会有一个开始，停止和复位按钮。我们的 return 语句将如下所示。

```
return ( <div className="App"> <button onClick={() => adjustTimer("incHours")}>&#8679;</button> <button onClick={() => adjustTimer("incMinutes")}>&#8679;</button> <button onClick={() => adjustTimer("incSeconds")}>&#8679;</button> <div>{hours} : {minutes} : {seconds}</div> <button onClick={() => adjustTimer("decHours")}>&#8681;</button> <button onClick={() => adjustTimer("decMinutes")}>&#8681;</button> <button onClick={() => adjustTimer("decSeconds")}>&#8681;</button> <br/><br/> <button onClick={() => setStart(true)}>Start</button> <button onClick={() => setStart(false)}>Stop</button> <button onClick={() => {setStart(false); setTime(0)}}>Reset</button></div>);
```

这是我的计时器！公平地说，它并不完美。有些怪癖需要改正。我正在考虑有条件地渲染按钮，以便它们只在计时器进程的不同步骤中显示。

尽管如此，仍有很大的改进空间，但这是开始工作所需要的。编码快乐！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)