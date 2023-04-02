# 停止使用 React 表单，考虑改用 Formik

> 原文：<https://javascript.plainenglish.io/stop-using-react-forms-and-consider-using-formik-instead-d19d1b047366?source=collection_archive---------6----------------------->

## 较少的样板代码使它成为更好的选择

![](img/d6e04e49ccc04c3aeefa17f99226f3f5.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

之前，我写过关于[停止使用 Redux——如果你想要](https://betterprogramming.pub/stop-using-redux-consider-easy-peasy-if-you-want-3214c41bcce5),请考虑简单，读者非常喜欢。所以我想向我的读者介绍一种替代的 React 表单。

这根本不是一个有助于我获得的晋升。只是在你的 web 开发之旅中帮助你的一个选择。

那么，我们开始吧。

一个网站总是需要一个注册，关注我们，或订阅我们的形式。这是在网站所有者和用户之间建立联系的最好方式之一。

毫无疑问，我们可以将谷歌表单集成到我们的网站中，甚至使用 React 文档中解释的[控制的](https://reactjs.org/docs/forms.html#controlled-components)或[不控制的](https://reactjs.org/docs/uncontrolled-components.html)组件。

但老实说，我不喜欢在我的网站上使用谷歌表单。现在，第二个选项是使用受控或非受控组件来创建表单。

简单地说，受控组件是输入形式，其中值被改变并以反应状态保存，无论它是类组件还是功能组件。

React 文档用这样一个简单的例子来解释它:

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
}

handleChange(event) {    
  this.setState({value: event.target.value});  
}handleSubmit(event) {
  alert('A name was submitted: ' + this.state.value);
  event.preventDefault();
}

render() {
   return (
    <form onSubmit={this.handleSubmit}>        
     <label> Name:
     <input type="text" value={this.state.value} 
      onChange={this.handleChange} />        
     </label>
     <input type="submit" value="Submit" />
    </form>
    );
  }
}
```

这里我们使用状态和 onChange 处理程序来保存表单细节。

在不受控制的组件中，数据由 DOM 自己处理，使用 ref 从 DOM 获取表单细节。

React 文档用最简单的例子解释了这一点:

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />        
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

毫无疑问，这两种方法都很棒，我们可以用它们做任何事情。但是它由许多样板文件组成，在超过 5 个字段后看起来很奇怪。因此，我了解了 Formik，实际上，是 React 文档向我推荐了 Formik。

# 学习 Formik

我为我的一个客户创建了一个网站，并希望使用任何方法将用户数据发布到他们的后端。

所以我尝试了 Formik，并在几分钟内实现了它。

由于其格式良好的文档，它很容易学习和实现。

福米克解释说，他们帮助开发人员解决了 3 个最烦人的问题:

1.  获取表单状态内外的值
2.  验证和错误消息
3.  处理表单提交

他们处理得很顺利。

# Formik 入门

要开始使用 Formik，您必须将其安装在 react 应用程序中。

使用:

```
npm install formik — save
```

或者使用:

```
yarn add formik
```

福米克可以在几分钟内学会。让我们从 Formik 文档中提供的一个例子开始，然后根据我们的需要修改它:

```
import React from 'react';
import { useFormik } from 'formik';const SignupForm = () => { const formik = useFormik({
     initialValues: { email: '',},
     onSubmit: values => {
       alert(JSON.stringify(values, null, 2));
   },}); return (
    <form onSubmit={formik.handleSubmit}>
       <label htmlFor="email">Email Address</label> <input 
         id="email"
         name="email"
         type="email"
         onChange={formik.handleChange}
         value={formik.values.email}
       /> <button type="submit">Submit</button>
     </form> );};
```

我们添加了一个电子邮件输入和另一个提交按钮输入。

在 form 标签中，我们已经提到，当用户输入他们的电子邮件并提交时，Formik 将显示一个带有用户电子邮件的警告。

简单地说，它将更新 useFormik 中的`initialValues`。

`handleChange` 会这样工作:

在类组件中:

```
constructor(props) {
    super(props);
    this.state = {value: ''};
}handleChange(event) {    
  this.setState({value: event.target.value});  
}
```

在功能组件中:

```
const [values, setValues] = React.useState({});const handleChange = e => {
     setValues(prevValues => ({
     ...prevValues,
     [e.target.name]: e.target.value
});}
```

很简单。

但是通常，一个表单包含两个以上的字段来获取用户详细信息。

所以，让我们开始吧。

# Formik 中的验证

您已经在表单中看到，有些字段是必需填写的，而其他字段是可选的。

您如何验证这一点？通过定义一个验证函数。

你可以这样做:

```
const validate = values => { const errors = {}; if (!values.firstName) {
     errors.firstName = 'Required';
   } else if (values.firstName.length > 15) {
     errors.firstName = 'Must be 15 characters or less';
   } if (!values.lastName) {
     errors.lastName = 'Required';
   } else if (values.lastName.length > 20) { 
     errors.lastName = 'Must be 20 characters or less';
   } if (!values.email) {
     errors.email = 'Required';
     } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
       errors.email = 'Invalid email address';
     } return errors;
};
```

它将验证用户的名字、姓氏和电子邮件，如果用户输入了错误的内容，它将显示一个错误。

整个代码是这样的。

# 用“是”验证

您可以如上所示或使用 Yup 来验证用户。这是你自己的选择。

要使用 Yup，你必须安装它。

使用 NPM

```
npm install yup — save
```

或者使用纱线

```
yarn add yup
```

这很简单，只需删除你的验证函数，并用 Yup 定义验证。

代码将如下所示

# 减少 Formik 中的样板文件

最后，让我们通过定义一些 Formik 组件来减少样板文件。

我们将使用 formik、Field、Form 和来自 Formik 的 ErrorMessage，并在我们的功能组件中定义它。

如下图所示

# 让我们结束吧

Formik 是使用验证和处理表单提交的好方法。感谢贾里德·帕尔默介绍了这样一个处理表单的好方法。

试试用那个。最后，选择权在你——谢谢。

**注:**这里的例子直接取自[文档](https://formik.org/docs/overview)，以便于解释。因此，所有的荣誉都属于创建文档的创建者。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)