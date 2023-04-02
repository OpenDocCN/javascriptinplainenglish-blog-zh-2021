# 使用 Formik 和 Yup 简化 React 应用程序中的表单处理

> 原文：<https://javascript.plainenglish.io/make-form-handling-easy-in-react-apps-with-formik-and-yup-basic-validation-cd08fb43d722?source=collection_archive---------16----------------------->

![](img/1f2bf7976de0263a5773c01e0e8fcb7b.png)

Photo by [Heather Lo](https://unsplash.com/@llhheather?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Formik 是一个使 React 应用程序中的表单处理变得简单的库。

Yup 是一个集成了 Formik 的库。

在本文中，我们将看看如何用 Formik 处理表单输入。

# 确认

用 Formik 添加验证的一种方法是将我们的表单组件转换成一个带有使用`withFormik`高阶组件进行验证的表单。

例如，我们可以写:

```
import React from "react";
import { withFormik } from "formik";const MyForm = (props) => {
  const {
    values,
    touched,
    errors,
    handleChange,
    handleBlur,
    handleSubmit
  } = props;
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        onChange={handleChange}
        onBlur={handleBlur}
        value={values.email}
        name="email"
      />
      {errors.email && touched.email && <div id="feedback">{errors.email}</div>}
      <button type="submit">Submit</button>
    </form>
  );
};const MyEnhancedForm = withFormik({
  mapPropsToValues: () => ({ email: "" }),
  validate: (values) => {
    const errors = {};
    if (!values.email) {
      errors.email = "Required";
    } else if (
      !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)
    ) {
      errors.email = "Invalid email address";
    } return errors;
  }, handleSubmit: (values, { setSubmitting }) => {
    setTimeout(() => {
      alert(JSON.stringify(values, null, 2));
      setSubmitting(false);
    }, 1000);
  }, displayName: "BasicForm"
})(MyForm);export default function App() {
  return (
    <div className="App">
      <MyEnhancedForm />
    </div>
  );
}
```

为了做到这一点。

我们创建了`MyForm`组件来从`props`中获取我们需要的属性。

`values`有输入值。

`touched`有每个输入的触动状态。

`errors`有我们在`validate`方法中设置的表单验证错误/

`handleChange`有表单变更处理程序。

`handleBlur`有模糊处理程序。

`handleSubmit`有提交处理程序。

接下来，我们创建具有验证的`MyEnhancedForm`组件。

`mapPropsToValues`设置为返回初始值的函数。

`validate`检查`values`参数的值后，返回一个错误对象。

`handleSubmit`具有表单提交功能。

`values`具有表单值。

`setSubmitting`具有设置表单提交状态的功能。

`displayName`为调试设置组件的`displayName`属性。

然后我们使用`App`中的`MyEnhancedForm`来呈现表单。

# 使用 Yep 进行基本验证

为了使表单验证更容易，我们可以使用 Yup 库向表单添加验证。

例如，我们可以写:

```
import React from "react";
import { Formik, Form, Field } from "formik";
import * as Yup from "yup";const SignupSchema = Yup.object().shape({
  email: Yup.string().email("Invalid email").required("Required")
});export const ExampleForm = () => (
  <div>
    <h1>Signup</h1>
    <Formik
      initialValues={{
        email: ""
      }}
      validationSchema={SignupSchema}
      onSubmit={(values) => {
        console.log(values);
      }}
    >
      {({ errors, touched }) => (
        <Form>
          <Field name="email" type="email" />
          {errors.email && touched.email ? <div>{errors.email}</div> : null}
          <button type="submit">Submit</button>
        </Form>
      )}
    </Formik>
  </div>
);export default function App() {
  return (
    <div className="App">
      <ExampleForm />
    </div>
  );
}
```

我们用`Yup.object()`方法创建了`SignupSchema`。

我们将一个对象传入到`shape`方法中，为该对象添加验证。

为了验证字符串，我们调用`Yup.string().email()`方法。

`'email'`的参数有验证错误信息。

`required`使该字段成为必填字段。

然后我们将返回的对象传递给`validationSchema` prop。

`onSubmit`有提交处理程序。

`initialValues`有初始值。

然后为了创建`Field`对象，我们将`name`设置为属性，我们在`shape`方法的参数中应用了表单验证。

`touched`已进入触摸输入状态。

# 结论

我们可以使用 Formik 添加表单验证，并且使用 yeah 可以使这变得更容易。

*更内容于* [***通俗地说就是***](https://plainenglish.io/)