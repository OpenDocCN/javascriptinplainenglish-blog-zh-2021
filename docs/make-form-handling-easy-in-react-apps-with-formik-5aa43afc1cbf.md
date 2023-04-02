# 使用 Formik 简化 React 应用程序中的表单处理

> 原文：<https://javascript.plainenglish.io/make-form-handling-easy-in-react-apps-with-formik-5aa43afc1cbf?source=collection_archive---------14----------------------->

![](img/7567d6b1b6687899e80f54e8977ac320.png)

Photo by [Tuân Nguyễn Minh](https://unsplash.com/@tuannguyenminh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Formik 是一个使 React 应用程序中的表单处理变得简单的库。

在本文中，我们将看看如何用 Formik 处理表单输入。

# 装置

我们可以通过运行以下命令来安装 Formik:

```
npm install formik --save
```

或者

```
yarn add formik
```

# 基本用法

我们可以通过书写来使用它:

```
import React from "react";
import { Formik } from "formik";export default function App() {
  return (
    <div className="App">
      <Formik
        initialValues={{ email: "", password: "" }}
        validate={(values) => {
          const errors = {};
          if (!values.email) {
            errors.email = "Required";
          } else if (
            !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
          ) {
            errors.email = "Invalid email address";
          }
          return errors;
        }}
        onSubmit={(values, { setSubmitting }) => {
          setTimeout(() => {
            alert(JSON.stringify(values, null, 2));
            setSubmitting(false);
          }, 400);
        }}
      >
        {({
          values,
          errors,
          touched,
          handleChange,
          handleBlur,
          handleSubmit,
          isSubmitting
        }) => (
          <form onSubmit={handleSubmit}>
            <input
              type="email"
              name="email"
              onChange={handleChange}
              onBlur={handleBlur}
              value={values.email}
            />
            {errors.email && touched.email && errors.email}
            <input
              type="password"
              name="password"
              onChange={handleChange}
              onBlur={handleBlur}
              value={values.password}
            />
            {errors.password && touched.password && errors.password}
            <button type="submit" disabled={isSubmitting}>
              Submit
            </button>
          </form>
        )}
      </Formik>
    </div>
  );
}
```

`initialValues`有初始值。

`validate`是一个让我们验证输入的表单值的函数。

`values`拥有我们输入的价值观。

我们用字段的错误来设置`errors`对象。

`onSubmit`有一个函数，在`values`对象中有输入的值。

`setSubmitting`是一个可以设置表单提交状态的功能。

在`form`元素中，我们将`onSubmit`表单设置为来自渲染道具参数的`handleSubmit`函数，以运行`onSubmit`如果它是值的话。

`values.email`和`values.password`具有每个字段的表单值。

`handleChange`让我们将输入的值合并到`values`对象的不同位置。

`onBlur`有`handleBlur`方法处理模糊事件。

`touched`具有每个表单域的已触摸状态。

`isSubmitting`有表单的提交状态。

我们可以用`Form`、`Field`和`ErrorMessage`组件来简化代码。

例如，我们可以将上面的代码简化为:

```
import React from "react";
import { ErrorMessage, Field, Form, Formik } from "formik";export default function App() {
  return (
    <div className="App">
      <Formik
        initialValues={{ email: "", password: "" }}
        validate={(values) => {
          const errors = {};
          if (!values.email) {
            errors.email = "Required";
          } else if (
            !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
          ) {
            errors.email = "Invalid email address";
          }
          return errors;
        }}
        onSubmit={(values, { setSubmitting }) => {
          setTimeout(() => {
            alert(JSON.stringify(values, null, 2));
            setSubmitting(false);
          }, 400);
        }}
      >
        {({ isSubmitting }) => (
          <Form>
            <Field type="email" name="email" />
            <ErrorMessage name="email" component="div" />
            <Field type="password" name="password" />
            <ErrorMessage name="password" component="div" />
            <button type="submit" disabled={isSubmitting}>
              Submit
            </button>
          </Form>
        )}
      </Formik>
    </div>
  );
}
```

这些组件替换了表单输入元素和错误文本。

只要`name`值在`Field`和`ErrorMessage`之间匹配，我们就会看到显示相同的值。

# 结论

我们可以用 Formik 轻松处理 React 中的表单。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)