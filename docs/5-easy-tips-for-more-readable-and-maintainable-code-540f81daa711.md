# 提高代码可读性和可维护性的 5 个简单技巧

> 原文：<https://javascript.plainenglish.io/5-easy-tips-for-more-readable-and-maintainable-code-540f81daa711?source=collection_archive---------7----------------------->

![](img/521cc3e7792a225a7b7b93471aa8103f.png)

Photo by [ian dooley](https://unsplash.com/@sadswim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.用动词如“是”或“可以”作为布尔变量的前缀

声明布尔变量时，在变量名前加上动词前缀，如“is”或“can ”,以帮助读者快速理解他们正在处理的值的类型。让我们看一些例子。

***显示 vs is display***

```
const display = false;
const isDisplaying = false; // Better
```

虽然你可以将*显示*解释为“是”或“否”，但我认为该显示也可以包含“阻塞”、“内嵌”、“无”等值。而使用“isDisplaying”时，可能性的范围可能仅限于“真”或“假”

***拨动 vs 康托***

```
const toggle = false;
const canToggle = false; // Better
```

再一次，我认为“canToggle”比“Toggle”更直观。“切换”为更多的解释打开了大门，比如“关”或“开”，或者甚至可以是执行一些附加逻辑的功能。使用 canToggle，很明显，它要么是一个布尔值，要么是一个将返回布尔值的函数。

***更多项目 vs 更多项目***

```
const moreItems = false;
const areMoreItems= false; // Better
```

在这个例子中，我们用“are”作为前缀，这只是“is”的一种形式。“moreItems”在这个上下文中可以指一系列附加的项目，但是 MoreItems 清楚地表示是否有更多的项目。

# 2.将“id”属性放在 HTML 元素的前面

如果你使用 HTML，或者像 React 或 Vue 这样的 JavaScript 框架，你应该知道一个或

上的属性数量会快速增长。当浏览一个大的 html 文件或表单时，总是将 id="elementId "属性**放在第一个**会很有帮助，这样读者可以很快知道他们在看什么元素

```
<form id="signUpForm">
   // RIGHT WAY
   <input 
      id="email"  // Clear at top
      type="email"
      onChange={(e) => setEmail(e.target.value)} // React code
      value={email}
      tabIndex="1"
    </input> // WRONG WAY
    <input 
      onChange={(e) => setPhone(e.target.value)} // React code
      value={phone}
      tabIndex="2"
      id="phone" // ID is harder to find
      type="phone"   
    </input>
</form>
```

对于第一个输入，我们将 id 属性放在第一位，对于第二个输入，我们将它隐藏在几个属性中。当扫描这段代码时，我认为读者会比第二个更快地将第一个输入识别为电子邮件字段。在第二个输入中，读者可能不得不扫描 onChange 方法，并试图从那里进行解释，而在第一个输入中，这是很难错过的。

# 3.当与 DOM 交互时，总是用“handle”作为函数的前缀

如果在使用 React 之类的框架/库时，您正在向 DOM 元素传递回调函数，并且您正在接收一个“事件”对象的形式，我强烈建议您在函数前面加上“handle”。您会在 React 文档中经常看到这一点，但是我想重申一下，当通读一个组件时，这种约定是多么有用。

```
// NOT AS GOOD
function save(event){
   event.preventDefault();
}<button onClick={save}></form>VS// GOOD
function handleSave(event){
   event.preventDefault();
}<button onClick={handleSave}></form>
```

如果您从执行业务逻辑或调用 API 服务的外部来源引入其他方法，如“save ”,那么区分与 DOM 元素交互的函数和不与 DOM 元素交互的函数会很有帮助，使用前缀“handle”会使这变得简单而高效。

# 4.使用 CQRS 模式来区分查询和命令

如果你不熟悉 CQRS 模式，我建议你先阅读马丁·福勒的这篇伟大的文章。我的快速总结是，动作分为两类，查询(获取信息)和命令(对某些东西进行操作)。如果你了解 CRUD，那么查询就是“R”，命令就是“CUD”(以及其他一切)。

由于大多数应用程序在查询和命令之间有一个平衡，构建应用程序来区分这两者可以使代码更容易阅读和维护。例如，如果您的应用程序调用 api，我会在我的 React 应用程序中创建一个 backendConfig 文件，并像这样构造它。

```
// backendConfig.js //export queryEndpoints = {
   getAllCustomers: '/api/get-all-customers'
   getCustomer: '/api/get-customer/'
}export commandEndpoints = {
   createCustomer: '/api/create-customer',
   updateCustomer: '/api/update-customer'
} // CustomerService.js //import {queryEndpoints, commandEndpoints} from './backendConfig.js'// Create Customer method
...
axios.post(commandEndpoints.createCustomer, customer);
...// Get Customer method
...
const customer = await axios.get(queryEndpoints.getCustomer + customerId);
...
```

这个例子省略了很多相关的逻辑，但是希望您理解将端点划分为查询和命令的意图和好处。如果您有一个更大的 API，这将非常有用，并且在添加新的端点或查找现有的端点时会节省您的时间。

# 5.条件语句总是使用花括号

你们中的一些人可能不同意我的观点，但是我在写条件语句时总是使用括号。如果您来自 Python，也许您喜欢只使用缩进，但是我发现花括号提供了大量的空白，既可以阅读代码，又可以快速确认您需要考虑的条件。此外，您会遇到必须对多行条件语句使用花括号的情况，因此最好保持一致，并在任何地方都使用它们。我知道你可能希望使用更少的代码行，但是我认为不值得为了让某人不小心跳过一个重要的条件而进行权衡。

```
// GOOD
if(isValid){
   save();
}vs// NOT AS GOOD - Less consistent
if(isValid) save(); 
OR 
if(isValid)
   save();
```

我确实使用三元运算符，但我通常会通过换行和缩进来使它们变得明显。我也只在把结果赋给变量的时候使用它们。

```
const errorMessage = !form.isValid
   ? "The form is invalid" 
   : "";
```

# 包扎

现在你知道了！编写更简洁、更易维护的代码的 5 个简单技巧。如果你同意或不同意这些观点，请在下面的评论中留言，如果你喜欢这篇文章，请留下一些掌声，跟我来。编码快乐！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)