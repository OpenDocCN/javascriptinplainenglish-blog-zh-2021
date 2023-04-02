# 如何用 React & Formik 构建单选按钮和复选框表单

> 原文：<https://javascript.plainenglish.io/react-js-forms-using-formiks-field-component-68a3bf5513d7?source=collection_archive---------17----------------------->

![](img/a0794fdc6b2983aec3c7ceea4585f942.png)

Photo by [Myriam Jessier](https://unsplash.com/@mjessier?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

网站表单很少只包含简单的文本字段和文本区域字段。它们通常包含更复杂的输入类型。这些包括下拉选择框、单选按钮和复选框输入。事实证明，在 React 中实现这些类型的输入对一些开发人员来说是一个挑战。

本文将向您展示一些复杂输入的逐步实现。这些是*下拉选择框*、*单选按钮、*和*复选框*输入。我们将在 Formik 中使用 ***<字段/ >*** 组件。

**第一步。**打造新鲜的 React app。称之为复杂表单应用程序。[在此阅读 React 安装步骤](https://reactjs.org/docs/create-a-new-react-app.html)

```
npx create-react-app complex-form-app
```

**第二步:**然后把 Formik 库安装到 app 上。[在此阅读 Formik 文档](https://formik.org/docs/overview)。

```
cd complex-form-app
npm install formik --save
```

**第三步:**接下来把*的*库安装到 app 上。

```
npm install yup --save
```

**第四步:**在 app 项目的 */src* 文件夹中创建一个名为 components 的文件夹。在 components 文件夹中，创建一个名为 Complexform.js 的文件。

```
import React from 'react'
import { Formik, Form, Field, ErrorMessage } from 'formik'
import * as Yup from 'yup'
```

**第五步:**创建一个名为 *complexForm* 的功能组件。

```
import React from 'react'
import { Formik, Form, Field, ErrorMessage } from 'formik'
import * as Yup from 'yup'
const complexForm = () => {}
```

**第六步:**向 *initialValues* 对象添加城市、宗教和职业属性。

```
*const* initialValues = {
   city: '',
   religion: '',
   occupation: []
}
```

**步骤 7:** 向 validationSchema 添加城市、宗教和职业字段的验证语句。

```
*const* validationSchema = Yup.object({

      city: Yup.string().required('Required'),
      religion: Yup.string().required('Required'),
      occupation: Yup.array().required('Required')})
```

**步骤 8:** 向 Formik 组件添加 initialValues、validationSchema 和 onSubmit 属性。

```
<Formik
    *initialValues*={initialValues}
    *validationSchema*={validationSchema}
    *onSubmit*={onSubmit}
></Formik>
```

**第九步:**在***<Formik/>***组件中，为城市、宗教、职业这三个字段分别添加带有 JSX 的渲染道具。使用 Formik 中的 ***<字段/ >*** 和 ***<错误消息/ >*** 组件。

```
<Formik
    *initialValues*={initialValues}
    *validationSchema*={validationSchema}
    *onSubmit*={onSubmit}
>{*formik* => {<Form><Field *component*='select' *name*='city' *placeholder*='select    options'>
  <option *value*="Los Angeles">Los Angeles</option>
  <option *value*="Philadelphia">Philadelphia</option>
  <option *value*="Chicago">Chicago</option>
  <option *value*="Washington DC">Washington DC</option>
  <option *value*="New York">New York</option>
  <option *value*="San Diego">San Diego</option>
  <option *value*="Fort Worth">Fort Worth</option>
  <option *value*="Houston">Houston</option>
</Field>
<ErrorMessage *name*="city" /><Field *type*='radio' *name*="religion" *value*="christianity" />
<Field *type*='radio' *name*="religion" *value*="muslim" />
<Field *type*='radio' *name*="religion" *value*="jew" />
<Field *type*='radio' *name*="religion" *value*="hindu" />
<ErrorMessage *name*="religion" /><Field *type*="checkbox" *value*="lawyer" *name*="occupation" />
<Field *type*="checkbox" *value*="teacher" *name*="occupation" />
<Field *type*="checkbox" *value*="footballer" *name*="occupation" />
<Field *type*="checkbox" *value*="preacher" *name*="occupation" />
<Field *type*="checkbox" *value*="doctor" *name*="occupation" />
<Field *type*="checkbox" *value*="economist" *name*="occupation" />
<Field *type*="checkbox" *value*="businessman" *name*="occupation" /><ErrorMessage *name*="occupation" /><button
  *type*="submit"
>
</button></Form>}}</Formik>
```

最终的***complex form . js***文件必须如下图所示。

```
import React from 'react'
import { Formik, Form, Field, ErrorMessage } from 'formik'
import * as Yup from 'yup' const complexForm = () => {*const* initialValues = {
   city: '',
   religion: '',
   occupation: []
}*const* validationSchema = Yup.object({

      city: Yup.string().required('Required'),
      religion: Yup.string().required('Required'),
      occupation: Yup.array().required('Required')})*const* onSubmit = *values* => console.log('Form data', values)return (<Formik
    *initialValues*={initialValues}
    *validationSchema*={validationSchema}
    *onSubmit*={onSubmit}
> {*formik* => {<Form><Field *component*='select' *name*='city' *placeholder*='select    options'>
  <option *value*="Los Angeles">Los Angeles</option>
  <option *value*="Philadelphia">Philadelphia</option>
  <option *value*="Chicago">Chicago</option>
  <option *value*="Washington DC">Washington DC</option>
  <option *value*="New York">New York</option>
  <option *value*="San Diego">San Diego</option>
  <option *value*="Fort Worth">Fort Worth</option>
  <option *value*="Houston">Houston</option>
</Field>
<ErrorMessage *name*="city" /><Field *type*='radio' *name*="religion" *value*="christianity" />
<Field *type*='radio' *name*="religion" *value*="muslim" />
<Field *type*='radio' *name*="religion" *value*="jew" />
<Field *type*='radio' *name*="religion" *value*="hindu" />
<ErrorMessage *name*="religion" /><Field *type*="checkbox" *value*="lawyer" *name*="occupation" />
<Field *type*="checkbox" *value*="teacher" *name*="occupation" />
<Field *type*="checkbox" *value*="footballer" *name*="occupation" />
<Field *type*="checkbox" *value*="preacher" *name*="occupation" />
<Field *type*="checkbox" *value*="doctor" *name*="occupation" />
<Field *type*="checkbox" *value*="economist" *name*="occupation" />
<Field *type*="checkbox" *value*="businessman" *name*="occupation" /><ErrorMessage *name*="occupation" /><button
  *type*="submit"
>
</button></Form>}}</Formik>}export default complexForm
```

**第十步:**将 ***complexForm*** 组件导入到 ***app.js*** 文件中，并添加到返回语句 JSX 中，如下所示。

```
import React from 'react'
import './App.css'
import ComplexForm from './components/complexForm'*function* App() {
  return (
     <div *classname*='App'>
       <ComplexForm/>
     </div>
)}export default App
```

运行应用程序。

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io/)