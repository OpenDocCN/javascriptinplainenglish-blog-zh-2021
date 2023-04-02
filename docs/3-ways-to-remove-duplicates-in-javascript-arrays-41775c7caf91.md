# 删除 JavaScript 数组中重复项的 3 种方法

> 原文：<https://javascript.plainenglish.io/3-ways-to-remove-duplicates-in-javascript-arrays-41775c7caf91?source=collection_archive---------12----------------------->

![](img/172bc5edcf91539e788f3f707920283d.png)

这篇博客将向您展示用 JavaScript 从数组中过滤唯一值、删除重复值的 3 种方法。

# 1.使用 filter 和 indexOf 仅获取每个值的第一个实例

这种方法包括在数组上运行一个`**filter**`**——对于每个值，只有当它是数组中具有该值的第一个项目时，我们才将其添加到唯一数组中，即如果`arr.indexOf(value) === index`:**

```
const arr = ['a', 'b', 'a', 'b', 'c'];const uniqueArr = arr.filter((value, index) => {
  return arr.indexOf(value) === index;
});console.log(uniqueArr); // ['a', 'b', 'c']
```

# 2.使用地图对象存储唯一值

第二种方法依赖于 **JavaScript map 对象**，它们不能有重复的键。它包括创建一个空的`mapObj`，并将数组的每个值作为一个键添加到`mapObj`。然后可以使用`Object.keys(mapObj)`检索最终的唯一数组:

```
const arr = ['a', 'b', 'a', 'b', 'c'];const mapObj = {};
arr.forEach(a => { 
  mapObj[a] = true;
});
const uniqueArr = Object.keys(mapObj);console.log(uniqueArr); // ['a', 'b', 'c']
```

# 3.转换成一个集合，并扩展回一个数组

最后，最短的方法是简单地用**将数组转换成一个**T5，然后用 spread 操作符(T7 操作符)将这个`Set`变回一个数组:

```
const arr = ['a', 'b', 'a', 'b', 'c'];const uniqueArr = [...new Set(arr)];console.log(arr); // ['a', 'b', 'c']
```

*希望这有所帮助！*