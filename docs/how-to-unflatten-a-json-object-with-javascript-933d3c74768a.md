# 如何用 JavaScript 取消 JSON 对象的扁平？

> 原文：<https://javascript.plainenglish.io/how-to-unflatten-a-json-object-with-javascript-933d3c74768a?source=collection_archive---------12----------------------->

![](img/cb114e2f972d340aa7a069538bce9a6b.png)

Photo by [Brooke Lark](https://unsplash.com/@brookelark?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 取消 JSON 对象的扁平。

在本文中，我们将研究如何用 JavaScript 取消嵌套 JSON 对象的扁平。

# 拆分每个属性路径，并将嵌套属性添加到未展平的对象中

要取消展平 JavaScript 对象，我们可以拆分每个属性路径，并将嵌套属性添加到取消展平对象中。

为此，我们写道:

```
const unflatten = (data) => {
  if (Object(data) !== data || Array.isArray(data))
    return data;
  const regex = /\.?([^.\[\]]+)$|\[(\d+)\]$/
  const props = Object.keys(data);
  let result, p;
  while (p = props.shift()) {
    const m = regex.exec(p)
    let target;
    if (m.index) {
      const rest = p.slice(0, m.index);
      if (!(rest in data)) {
        data[rest] = m[2] ? [] : {};
        props.push(rest);
      }
      target = data[rest];
    } else {
      if (!result) {
        result = (m[2] ? [] : {});
      }
      target = result
    }
    target[m[2] || m[1]] = data[p];
  }
  return result;
};console.log(unflatten({
  'a[0].b[0]': "c",
  'a[0].b[1]': "d"
}))
```

我们创建了`unflatten`函数来对展平的对象进行去平滑。

它接受可以是任何值的参数。

在函数中，我们检查`data`是一个对象还是一个数组。

如果其中一个为真，那么我们就原样返回`data`。

否则，我们有`regex`来解析属性路径。

`props`拥有来自`data`的按键。

然后，我们遍历这些键并调用`regex.exec`来获取属性路径部分，并将其分配给`m`。

接下来，我们得到提取的属性部分的`index`。

然后我们检查属性路径 path 是否在`data`中。

如果不是，那么我们把它加到`data`。

然后我们用`rest`到`props`调用`props.push`。

然后我们将`data[rest]`赋值给`target`来更新`targer`。

否则，我们将`result`赋值给`target`。

如果没有剩余的属性部分，我们将把`target`的属性添加到数据中。

然后我们返回`result`。

现在，当我们运行`unflatten`函数时，我们应该看到一个带有数组值的`a`属性的对象。

在其中，我们有一个带有数组值的`b`属性，数组值中有`'c'`和`'d'`。

# 结论

我们可以通过拆分属性路径，然后用循环将它们添加到未展平的对象中，来取消展平的 JSON 对象。

*更多内容请看*[***plain English . io***](http://plainenglish.io)