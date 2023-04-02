# 用 Formik 和 Yup 进行表单验证

> 原文：<https://javascript.plainenglish.io/react-form-validation-using-formik-and-yup-1b558594c39b?source=collection_archive---------3----------------------->

## 如何在 React 中处理表单验证

![](img/a0d834951675ac6ba2b4af2fc3c6cf0b.png)

Photo by [Domenico Loia](https://unsplash.com/@domenicoloia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

前端开发人员必须进行客户端表单验证。这是因为它改善了用户体验和网站性能。它防止向后端服务器发送无效数据。REACT 与其他库的结合使这种实现变得容易。本文将向您展示如何向**文本字段**、**电子邮件字段**、**文本区域**和**日期字段**添加验证。我们将使用 REACT、formik 和 Yep。

**第一步。**打造新鲜的 react app。称之为表单-验证-app。[在此阅读 React 安装步骤](https://reactjs.org/docs/create-a-new-react-app.html)

```
npx create-react-app form-validation-app
```

**第二步:**然后把 formik 库安装到 app 上。[在此阅读 Formik 文档](https://formik.org/docs/overview)

```
cd form-validation-app
npm install formik --save
```

**第三步:**接下来把 *yup* 库安装到 app 上。

```
npm install yup --save
```

第四步:在你的 app 项目的 */src* 文件夹中创建一个名为 components 的文件夹。在 components 文件夹中，创建一个名为 Personalform.js 的文件。

```
import React from 'react'
import { useFormik } from 'formik'
import * as Yup from 'yup'
```

**第五步:**创建一个名为 *personalForm* 的功能组件。

```
import React from 'react'
import { useFormik } from 'formik'
import * as Yup from 'yup' const personalForm = () => {}
```

**第六步:**在 *personalForm* 组件中，创建三个变量，分别叫做 *initialValues* 、 *validationSchema、*和 *formik* 。

```
const personalForm = () => {
   *const* initialValues = {}
   const validationSchema = Yup.object({})
   const formik = useFormik({})
}
```

**步骤 7:** 向 *initialValues* 对象添加姓名、电子邮件、地址和 dob 属性。

```
*const* initialValues = {
   name: '',
   email: '',
   address: '',
   dob: ''
}
```

**步骤 8:** 向 validationSchema 添加名称、电子邮件、地址和日期字段的验证语句。

```
*const* validationSchema = Yup.object({
    name: Yup.string()
             .required('Required')
             .max(50),
    email: Yup.email()
              .required('Required'),
    address: Yup.string()
                .required('Required')
                .max(600),
    dob: Yup.date()
            .required('Required'),
});
```

**步骤 9:** 向 formik 变量添加 initialValues、validationSchema 和 onSubmit 属性。

```
const formik = useFormik({
    initialValues: initialValues,
    validationSchema: validationSchema
    onSubmit: values => {
     alert(JSON.stringify(values, null, 2));
    },
});
```

**第 10 步:**在 return 语句中，为每个字段添加 JSX 姓名、电子邮件、地址和出生日期。在它们中包含一个 *onChange* 处理程序。

```
<form *onSubmit*={formik.handleSubmit}>
       <label *htmlFor*="name">Name</label>
       <input
         *id*="name"
         *name*="name"
         *type*="text"
         *onChange*={formik.handleChange}
         *value*={formik.values.name}
       />{formik.errors.name ? 
      <div>{formik.errors.name}</div> : null}<label *htmlFor*="email">Email</label>
      <input
        *id*="email"
        *name*="email"
        *type*="email"
        *onChange*={formik.handleChange}
        *value*={formik.values.email}
      />{formik.errors.email ? 
      <div>{formik.errors.email}</div> : null}<label *htmlFor*="address">Physical Address</label>
      <textarea
         *id*="address"
         *name*="address"
         *onChange*={formik.handleChange}
         *value*={formik.values.address}
      />
      {formik.errors.address ? 
      <div>{formik.errors.address}</div> : null}<label *htmlFor*="dob">Date of Birth</label>
      <input
         *id*="dob"
         *name*="dob"
         *type*="date"
         *onChange*={formik.handleChange}
         *value*={formik.values.dob}
      />{formik.errors.dob ? 
      <div>{formik.errors.dob}</div> : null}<button *type*="submit">Submit</button>
</form>
```

最后的***personal form . js***文件一定是下面这个样子。

```
import React from 'react'
import { useFormik } from 'formik'
import * as Yup from 'yup' const personalForm = () => {*const* initialValues = {
   name: '',
   email: '',
   address: '',
   dob: ''
}*const* validationSchema = Yup.object({
    name: Yup.string()
             .required('Required')
             .max(50),
    email: Yup.email()
              .required('Required'),
    address: Yup.string()
                .required('Required')
                .max(600),
    dob: Yup.date()
            .required('Required'),
});const formik = useFormik({
    initialValues: initialValues,
    validationSchema: validationSchema
    onSubmit: values => {
     alert(JSON.stringify(values, null, 2));
    },
});return (
   <form *onSubmit*={formik.handleSubmit}>
       <label *htmlFor*="name">Name</label>
       <input
         *id*="name"
         *name*="name"
         *type*="text"
         *onChange*={formik.handleChange}
         *value*={formik.values.name}
       /> {formik.errors.name ? 
      <div>{formik.errors.name}</div> : null} <label *htmlFor*="email">Email</label>
      <input
        *id*="email"
        *name*="email"
        *type*="email"
        *onChange*={formik.handleChange}
        *value*={formik.values.email}
      /> {formik.errors.email ? 
      <div>{formik.errors.email}</div> : null} <label *htmlFor*="address">Physical Address</label>
      <textarea
         *id*="address"
         *name*="address"
         *onChange*={formik.handleChange}
         *value*={formik.values.address}
      />
      {formik.errors.address ? 
      <div>{formik.errors.address}</div> : null} <label *htmlFor*="dob">Date of Birth</label>
      <input
         *id*="dob"
         *name*="dob"
         *type*="date"
         *onChange*={formik.handleChange}
         *value*={formik.values.dob}
      /> {formik.errors.dob ? 
      <div>{formik.errors.dob}</div> : null} <button *type*="submit">Submit</button>);};
```

**步骤 11:** 将 ***personalForm*** 组件导入到 ***app.js*** 文件中，并添加到返回声明 JSX 中，如下所示。

```
import React from 'react'
import './App.css'
import PersonalForm from './components/PersonalForm'*function* App() {
  return (
     <div *classname*='App'>
       <PersonalForm/>
     </div>
)}export default App
```

运行应用程序

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io)