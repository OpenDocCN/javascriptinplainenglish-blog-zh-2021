# 用 React 和 JavaScript 创建一个货币转换器

> 原文：<https://javascript.plainenglish.io/create-a-currency-converter-with-react-and-javascript-939535c28fb0?source=collection_archive---------18----------------------->

![](img/6e87916df86a9c1a68056096c47ba408.png)

Photo by [Macau Photo Agency](https://unsplash.com/@macauphotoagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将了解如何使用 React 和 JavaScript 创建货币转换器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app currency-converter
```

和 NPM 一起创建我们的 React 项目。

# 创建货币转换器

为了创建货币转换器，我们编写:

```
import React, { useMemo, useState } from "react";export default function App() {
  const [value, setValue] = useState(0);
  const [fromCurrency, setFromCurrency] = useState("");
  const [toCurrency, setToCurrency] = useState("");
  const [currencies] = useState(["EUR", "USD", "CAD"]);
  const [result, setResult] = useState(0); const fromCurrencies = useMemo(() => {
    return currencies.filter((c) => c !== toCurrency);
  }, [currencies, toCurrency]); const toCurrencies = useMemo(() => {
    return currencies.filter((c) => c !== fromCurrency);
  }, [currencies, fromCurrency]); const convert = async (e) => {
    e.preventDefault();
    const formValid = +value >= 0 && fromCurrency && toCurrency;
    if (!formValid) {
      return;
    }
    const res = await fetch(
      `https://api.exchangeratesapi.io/latest?base=${fromCurrency}`
    );
    const { rates } = await res.json();
    setResult(+value * rates[toCurrency]);
  }; return (
    <div>
      <form onSubmit={convert}>
        <div>
          <label>value</label>
          <input value={value} onChange={(e) => setValue(e.target.value)} />
        </div>
        <div>
          <label>from currency</label>
          <select
            value={fromCurrency}
            onChange={(e) => setFromCurrency(e.target.value)}
          >
            {fromCurrencies.map((c) => (
              <option key={c}>{c}</option>
            ))}
          </select>
        </div>
        <div>
          <label>to currency</label>
          <select
            value={toCurrency}
            onChange={(e) => setToCurrency(e.target.value)}
          >
            {toCurrencies.map((c) => (
              <option key={c}>{c}</option>
            ))}
          </select>
        </div>
        <button type="submit">convert</button>
      </form>
      <div>
        {value} {fromCurrency} is {result.toFixed(2)} {toCurrency}
      </div>
    </div>
  );
}
```

我们有一个`value`状态，存储要转换的货币值。

`fromCurrency`有可兑换的货币。

`toCurrency`有可兑换的货币，

`currencies`有货币选择。

`result`有转换的结果。

`fromCurrencies`有我们可以选择转换的选项。

我们使用带有回调的`useMemo`钩子返回我们可以选择的所有货币。

我们从返回的数组中排除了`toCurrency`值。

第二个参数具有要监视的值，以便第一个回调再次运行来更新返回值。

同样，我们用同样的方法来定义`toCurrencies`，但是我们排除了`fromCurrency`值。

接下来，我们定义执行货币转换的`convert`函数。

在它内部，我们调用`e.preventDefault()`让我们进行客户端表单提交。

然后我们检查`value`是否大于 0，并且`fromCurrency`和`toCurrency`是否被设置。

如果所有条件都满足，我们就从汇率 API 中获取汇率。

然后我们调用`setResult`来计算转换后的货币值。

接下来，我们添加表单让我们输入值。

它将`onSubmit`属性设置为`convert`函数，当我们单击类型为`submit`的按钮时，该函数就会运行。

其中有一个输入用于设置`value`。

`e.target.value`有输入值。

每当我们改变输入的值时,`onChange`就会运行。

同样，我们有选择下拉框，让我们分别选择要转换的货币。

我们用`value`和`onChange`属性设置它们的值。

我们在 select 元素中呈现`fromCurrencies`和`toCurrencies`来呈现选择。

在表单下方，我们向用户显示结果。

`toFixed`方法返回带有我们传入的小数位数的数字的字符串形式。

# 结论

我们可以用 React 和 JavaScript 创建一个货币转换器。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)