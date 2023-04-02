# 用 React 实现一个离线工作的搜索特性

> 原文：<https://javascript.plainenglish.io/implement-a-search-feature-with-react-that-works-offline-ea7cbc158907?source=collection_archive---------5----------------------->

## 不要等待后端 API。自己动手！

![](img/445ef732be0f9710412e7bc14676438f.png)

Photo by [Evgeni Tcherkasski](https://unsplash.com/@evgenit?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/search?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

您正在设计一个应用程序，您需要显示一个列表或表格，其中的数据可以立即提供给您。

该列表包含大约 30-40 条记录(或者更多)。

现在，您的用户需要一个搜索功能，以便他们可以轻松地过滤数据。

你是做什么的？

# 第一选项

您可以回到后端开发人员那里，请求一个搜索 API，使用数据库查询或其他方法返回匹配的数据。

但是这使得搜索过程非常耗时。用户必须等待结果返回才能看到任何东西。

您还必须维护 API 调用，以便一切按预期运行。

不太方便吧？

# 让我们离线做吧

假设我们有一个用户列表。数据如下所示。你有一系列这些。

```
data = [
   {
     name: "Mohammad Faisal",
     company: "Some Company",
     age: 56,
     address: "Dhaka, Bangladesh"
   }
   ... more
]
```

顶部有一个搜索栏，用户可以在那里搜索文本。

```
const [searchText , setSearchText] = useState('');const onTextChange = (e) => setSearchText(e.target.value);return <input onChange={onTextChange} />
```

因此，一种选择是当您的`searchText`值改变时触发回调。

```
useEffect(() => { // do the filtering here },[searchText])
```

但是你如何进行搜索呢？

有一些 javascript 函数可以帮我们完成这项工作。

```
data.filter(singleUser => singleUser.name.includes(searchText))
```

这很好。因此，当用户搜索文本时，列表将根据用户的`name`属性进行过滤。

我们也可以将此扩展到其他属性。通过一个一个的过滤。

```
data.filter(singleUser => {
  return 
      singleUser.name.includes(searchText)) **|| ** 
      singleUser.address.includes(searchText))
}
```

但是正如你所看到的，如果你必须搜索 10 个字段，这可能会很快失控。你必须把所有的东西都打出来。

不方便吧？

让我们做得更好。

# JSON 的力量

因此，我们将利用现有的`JSON.stringify()`和`JSON.parse()`方法。

因为在一个对象内部搜索是困难的，因为我们在搜索之前可能不知道那个对象的键，所以我们不能把它们一般化。

所以我们将把整个对象变成一个字符串，并在其上进行搜索。

useSearch.ts

您可以将这种逻辑转移到一个漂亮整洁的钩子上，以提高可用性。

# 进一步改进

如果用户使用正确的大写字母进行搜索，我们实现的解决方案将会工作。

因此，如果用户搜索`faisal`，他们可能会同时想要两个结果

*   `faisal`和`Faisal`

那么我们如何解决这个问题呢？

我们可以将字符串化的数组变成一个`lower case`字符串。有一个 javascript 函数可以实现这个`toLowerCase()`

并且也将`searchText`转换成小写来解决这个问题

最后，我们的代码将如下所示

这是一个可重用的钩子，你将提供一个对象数组和一个`searchText`，它将返回过滤后的数据。

现在你有了一个功能性的离线搜索，而且速度非常快！

今天到此为止！希望你学到了有趣的东西。

祝您愉快！

**通过**[**LinkedIn**与我联系](https://www.linkedin.com/in/56faisal/)

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的**[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) *。**