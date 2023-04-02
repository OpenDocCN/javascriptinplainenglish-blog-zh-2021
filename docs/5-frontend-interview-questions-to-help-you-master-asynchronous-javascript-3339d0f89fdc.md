# 帮助你掌握异步 JavaScript 的 5 个前端面试问题

> 原文：<https://javascript.plainenglish.io/5-frontend-interview-questions-to-help-you-master-asynchronous-javascript-3339d0f89fdc?source=collection_archive---------4----------------------->

## 问答，从初级到高级

![](img/5e407ce4f49e6c4e5459125d565f1e41.png)

src: [https://ivanjov.com/do-you-promise/](https://ivanjov.com/do-you-promise/)

学习 JavaScript 时，最难理解的事情之一是**承诺**。它们不容易理解，需要一些教程和大量的练习才能掌握。

今天我们将为您准备**编码面试**和**主承诺**。

在看到完整答案之前，请尝试回答以下问题:)

# *1。这个回报是什么？*

```
const **firstPromise** = new Promise((res, rej) => {
      setTimeout(res, 500, 'one');
});

const **secondPromise** = new Promise((res, rej) => {
      setTimeout(res, 100, 'two');
});

**Promise.race**([firstPromise, secondPromise]).then(res => console.log(res));
```

*   答:`"one"`
*   乙:`"two"`
*   丙:`"two" "one"`
*   丁:`"one" "two"`

## **回答**

当我们将多个承诺传递给 **Promise.race** 方法时，它解析/拒绝第一个解析/拒绝的承诺。对于 **setTimeout** 方法，我们传递一个定时器:第一个承诺(**first promise**)500 毫秒，第二个承诺(**second promise**)100 毫秒。这意味着**第二个承诺**首先解析为**‘二’**的值。 **res** 现在保存**‘two’**的值，该值被记录。正确答案是 **B** 。

# 2.产量是多少？

```
**async** function **getData**() {
      return await Promise.resolve('I made it!');
}

const **data** = getData();
console.log(data);
```

*   答:`"I made it!"`
*   乙:`Promise {<resolved>: "I made it!"}`
*   丙:`Promise {<pending>}`
*   丁:`undefined`

## **回答**

异步函数总是返回一个承诺。`await`仍然需要等待承诺的解析:当我们调用`getData()`来设置`data`等于它时，一个未决的承诺被返回。

如果我们想访问解析后的值`"I made it"`，我们可以在`data`上使用`.then()`方法:

```
data.then(res => console.log(res))
```

这将被记录`"I made it!"`。正确答案是 **C** 。

# 3.*输出值是多少？*

```
const **myPromise** = () => Promise.resolve('I have resolved!');

function **firstFunction**() {
    myPromise().then(res => console.log(res));
    console.log('second');
}

**async** function **secondFunction**() {
    console.log(await myPromise());
    console.log('second');
}

firstFunction();
secondFunction();
```

*   答:`I have resolved!`、`second`、*和*、`I have resolved!`、`second`
*   b:`second``I have resolved!`*`second``I have resolved!`*
*   *C: `I have resolved!`、`second`、*、*、`second`、`I have resolved!`*
*   *D: `second`、`I have resolved!`、`I have resolved!`、`second`*

## ***答案***

*有了承诺，我们基本上会说*我想执行这个函数，但它运行时我会暂时把它放在一边，因为这可能需要一段时间。只有当某个值被解析(或拒绝)并且调用堆栈为空时，我才希望使用该值。**

*我们可以通过`.then`和`async`函数中的`await`关键字获得该值。虽然`.then`和`await`都能体现出承诺的价值，但二者的作用原理略有不同。*

*在`firstFunction`中，我们(有点)把 myPromise 函数放在一边，同时它还在运行，但我们继续运行另一个代码，在这个例子中就是`console.log('second')`。然后，该函数用字符串`I have resolved`解析，当它看到调用堆栈为空时，就会记录该字符串。*

*利用`secondFunction`中的 wait 关键字，我们实际上暂停异步函数的执行，直到该值被解析后再移动到下一行。*

*这意味着它等待`myPromise`用值`I have resolved`解析，只有发生一次，我们移动到下一行:`second`被记录。正确答案为 **D** 。*

## *4.*这会带来什么回报？**

```
*Promise.resolve(5);*
```

*   *答:`5`*
*   *B: `Promise {<pending>: 5}`*
*   *C: `Promse {<fulfilled>: 5}`*
*   *D: `Error`*

## ***回答***

*我们可以向`Promise.resolve`传递任何类型的值，可以是承诺值，也可以是非承诺值。该方法本身返回一个带有解析值的承诺(`<fulfilled>`)。如果你传递一个正则函数，它将是一个有正则值的解析承诺。如果你传递了一个承诺，它将是一个解决了的承诺，并具有解决了的价值。*

*在这种情况下，我们只是传递了数值`5`。它返回一个解析的承诺，值为`5`。正确答案是 **C** 。*

## *5.产量是多少？*

```
***async** function* **range**(start, end) {
      for (let i = start; i <= end; i++) {
            yield Promise.resolve(i);
      }
}

(**async** () => {
      const **gen** = range(1, 3);
      for **await** (const item of gen) {
            console.log(item);
      }
})();*
```

*   *答:`Promise {1}` `Promise {2}` `Promise {3}`*
*   *B: `Promise {<pending>}` `Promise {<pending>}` `Promise {<pending>}`*
*   *C: `1` `2` `3`*
*   *D: `undefined` `undefined` `undefined`*

## ***回答***

*生成器函数`range`为我们传递的范围内的每一项返回一个带有承诺的异步对象:`Promise{1}`、`Promise{2}`、`Promise{3}`。我们设置变量`gen`等于异步对象，之后我们使用`for await ... of`循环遍历它。我们将变量`item`设置为等于返回的承诺值:首先是`Promise{1}`，然后是`Promise{2}`，然后是`Promise{3}`。由于*在等待*的`item`值，解析后的 promsie，承诺的解析后的*值*得到返回:`1`，`2`，然后`3`。正确答案是 **C** 。*

# *结论*

*希望你喜欢破解承诺任务并更新你的知识。我祝你在 JavaScript 学习上好运！*