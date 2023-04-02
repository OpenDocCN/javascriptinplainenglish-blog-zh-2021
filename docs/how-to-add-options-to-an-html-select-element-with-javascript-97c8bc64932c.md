# 如何用 JavaScript 给一个 HTML select 元素添加选项？

> 原文：<https://javascript.plainenglish.io/how-to-add-options-to-an-html-select-element-with-javascript-97c8bc64932c?source=collection_archive---------7----------------------->

![](img/430149463be101c6f31255c199e675b8.png)

Photo by [Tamara Gak](https://unsplash.com/@tamara_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 为 HTML select 元素添加选项。

在本文中，我们将研究如何用 JavaScript 向 HTML select 元素添加选项。

# 使用 document.createElement 方法

我们可以使用`document.createElement`方法创建一个新的选项元素。

然后我们可以在 select 元素上调用`appendChild`来将它附加为 select 元素的子元素。

例如，我们可以编写以下 HTML:

```
<select></select>
```

创建空的选择元素。

然后，我们可以通过编写以下内容为 select 元素添加选项元素:

```
const select = document.querySelector('select')
const arr = ['apple', 'orange', 'grape']
for (const [index, a] of arr.entries()) {
  const opt = document.createElement('option');
  opt.value = index;
  opt.innerHTML = a;
  select.appendChild(opt);
}
```

我们用`document.querySelector`得到选择元素。

然后我们用我们想要添加的选项文本定义`arr`数组。

接下来，我们有一个 for-of 循环来遍历`arr`条目。

我们调用`arr.entries`来返回一个数组，数组条目的索引和值都在各自的数组中。

在循环体中，我们调用`document.createElement`来创建选项元素。

接下来，我们设置`value`属性来设置 option 元素的`value`属性的值。

然后我们设置`innerHTML`属性来设置用户在每个选项的下拉列表中看到的内容。

最后，我们用`opt`元素对象调用`select.appendChild`，将其添加为 select 元素的子元素。

因此，现在我们应该看到一个下拉菜单，有苹果、桔子和葡萄作为选项。

# 结论

我们可以用`document.createElement`方法将选项添加到 select HTML 元素中。

然后我们可以用`appendChild`将创建的 option 元素附加到 select 元素上。