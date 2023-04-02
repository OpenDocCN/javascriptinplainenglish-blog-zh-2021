# React 里的道具是什么？

> 原文：<https://javascript.plainenglish.io/props-in-react-6852d950ccbe?source=collection_archive---------23----------------------->

## 反应道具的介绍和指南

![](img/4efad539f337d5b016508386aa51b9c8.png)

Photo by [Md Mahdi](https://unsplash.com/@mahdi17?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 React 时很难不遇到 prop 这个概念。当我们在 React 中构建应用程序时，我们应该知道并理解这个概念，这一点很重要。

在我之前的文章中，我们已经学习了状态管理及其使用。今天，我们将在 React 中使用道具，并制作一个简单的接触表单。

开始之前，我们需要了解什么是组件。

一个**组件**是一个更大整体的一部分或元素。在编码中，我们通常将应用程序分成几个部分。或者我们想在相同或不同的项目中的其他地方使用相同的代码块。有了组件，我们就能实现这一点。事实上，到目前为止，我们已经在应用程序中使用了组件。

React 中有两种类型的组件，类组件和功能组件，在命名组件时，我们应该从大写字母开始。如果我们没有反应，就把它们当作 DOM(文档对象模型)标签，如

、

# 、等。下面，我们可以看到一个类组件的例子。

```
*import* React, { Component } *from* "react"; class SayHello extends Component {constructor(props) {super(props);this.state = {};}render() {*return* <h1>Hello, My name is Muzaffer.</h1>;}}*export* *default* SayHello;
```

> 类组件需要 render()方法。

这里我们看到了一个功能组件的示例。

```
*import* React *from* "react";const SayHello = () => {*return* <h1>Hello, My name is Muzaffer.</h1>;};*export* *default* SayHello;
```

**道具**

假设在我们的 SayHello 组件中，我们希望动态显示名称，而不仅仅是“Muzaffer”。我们可以通过在同一个组件中使用状态来实现这一点。但是如果我们想从不同的组件发送名字呢？我们将发送的名称可以从用户输入中获取，也可以通过 rest 服务获取。

为了做到这一点，我们使用道具。用**道具，我们可以在组件之间传递数据。在这样做的时候，我们需要做的是使用带有 HTML 属性的参数。在下面的例子中，我们使用 name 作为属性，使用“Muzaffer”作为值。**

```
*import* "./App.css";*import* SayHello *from* "./components/SayHello";function App() {*return* (<div className="App"><SayHello name="Muzaffer" /></div>);}*export* *default* App;
```

**既然我们传递了 prop，现在我们可以在 SayHello 组件上使用它了。我们唯一要做的就是在我们的 JSX 展示它。**

```
*import* React, { Component } *from* "react";class SayHello extends Component {constructor(props) {super(props);this.state = {};}render() {*return* <h1>Hello, My name is {this.props.name}.</h1>;}}*export* *default* SayHello;
```

**在功能组件中；**

```
*import* React *from* "react";const SayHello = (props) => {*return* <h1>Hello, My name is {props.name}.</h1>;};*export* *default* SayHello;
```

**既然我们已经学会了使用道具，现在我们可以向前迈一步，看看我们如何使用表单输入作为例子。**

**现在，假设我们的网站上有一个联系表单，我们希望人们使用该表单与我们联系。在我们的表单中，我们需要获得以下信息:**

*   **姓名**
*   **电话**
*   **电子邮件**
*   **和消息。**

**正如您所看到的，我们可以将这些信息看作是文本输入。所以我们可以为这些输入创建一个组件。**

**我们的文本输入组件将有三个道具，它们是**、【值】、【标签】**。使用 change prop，我们将把输入的 onChange 函数传递给 parent。使用 value prop，我们将从父组件发送输入的状态值。最后，label prop 将成为 input 的标签。**

**我们的自定义文本输入组件将如下所示:**

```
*import* React *from* "react";const CustomTextInput = (props) => {*return* (<divstyle={{display: "flex",justifyContent: "center",alignItems: "center",margin: "0 auto",width: "300px",}}><p style={{ textAlign: "left", width: "150px" }}>{props.label}{":"}</p><inputtype="text"value={props.value}onChange={props.change}style={{height: "30px",border: "1px solid gray",borderRadius: "4px",}}/></div>);};*export* *default* CustomTextInput;
```

**如你所见，我们有一个非常简单的组件。在我们的组件中，我们有一个 div 来包装我们的标签段落和文本类型的输入。我们有一些用于演示目的的内联样式。现在我们可以在项目中的任何地方使用我们的组件。**

**我们可以如下使用我们的组件。**

```
*import* { useState } *from* "react";*import* "./App.css";*import* CustomTextInput *from* "./components/CustomTextInput";*import* SayHello *from* "./components/SayHello";function App() {const [contactForm, setContactForm] = useState({name: "",phone: "",email: "",message: "",});const changeName = (e) => {setContactForm((prevState) => {prevState.name = e.target.value;*return* { ...prevState };});};const changePhone = (e) => {setContactForm((prevState) => {prevState.phone = e.target.value;*return* { ...prevState };});};const changeEmail = (e) => {setContactForm((prevState) => {prevState.email = e.target.value;*return* { ...prevState };});};const changeMessage = (e) => {setContactForm((prevState) => {prevState.message = e.target.value;*return* { ...prevState };});};*return* (<div className="App"><SayHello name="Muzaffer" /><CustomTextInputvalue={contactForm.name}change={changeName}label="Name Surname"/><CustomTextInputvalue={contactForm.phone}change={changePhone}label="Phone"/><CustomTextInputvalue={contactForm.email}change={changeEmail}label="Email"/><CustomTextInputvalue={contactForm.message}change={changeMessage}label="Message"/></div>);}*export* *default* App;
```

**在 App 组件中，我们创建了保存联系人表单输入值的状态。然后我们有 change 函数，它接收事件作为参数，并设置联系人表单状态。我们将这些作为道具传递给 CustomTextInput 组件。**

**如你所见，当我们使用 React 时，道具非常有用。一旦体验到道具的威力，就更想用了:)**

**今天我试图解释我们如何使用组件和道具，并在一个简单的联系人表单示例中使用它们。我希望我的帖子有所帮助。**

**我希望你有美好的一天。**

**参考资料:**

**[](https://reactjs.org/docs/components-and-props.html) [## 组件和道具-反应

### 组件可以让你将用户界面分割成独立的、可重用的部分，并独立地考虑每一部分。这一页…

reactjs.org](https://reactjs.org/docs/components-and-props.html) [](https://blog.logrocket.com/the-beginners-guide-to-mastering-react-props-3f6f01fd7099/) [## React - LogRocket 博客中如何将道具传递给组件

### 当您学习如何使用 React 开发 web 应用程序时，您将不可避免地遇到 props 的概念…

blog.logrocket.com](https://blog.logrocket.com/the-beginners-guide-to-mastering-react-props-3f6f01fd7099/) [](https://www.w3schools.com/react/react_components.asp) [## 反应组分

### 组织良好，易于理解的网站建设教程，有很多如何使用 HTML，CSS，JavaScript 的例子…

www.w3schools.co](https://www.w3schools.com/react/react_components.asp) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)**