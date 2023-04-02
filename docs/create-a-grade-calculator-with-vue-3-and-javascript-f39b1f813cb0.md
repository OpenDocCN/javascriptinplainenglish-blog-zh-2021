# 用 Vue 3 和 JavaScript 创建一个分数计算器

> 原文：<https://javascript.plainenglish.io/create-a-grade-calculator-with-vue-3-and-javascript-f39b1f813cb0?source=collection_archive---------20----------------------->

![](img/4116e9c4a613dac061ad4a86e45b554b.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在这篇文章中，我们将看看如何用 Vue 3 和 JavaScript 创建一个成绩计算器。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create grade-calculator
```

并选择所有默认选项来创建项目。

我们还需要安装`uuid`包，这样我们就可以为每个成绩条目生成唯一的 id。

要安装它，我们运行:

```
npm i uuid
```

# 创建等级计算器

为了创建分数计算器，我们编写:

```
<template>
  <form @submit.prevent="calculate">
    <div v-for="(grade, index) of grades" :key="grade.id">
      <label>grade</label>
      <input v-model.number="grade.value" />
      <button type="button" @click="deleteGrade(index)">delete grade</button>
    </div>
    <button type="button" @click="addGrade">add grade</button>
    <button type="submit">calculate average</button>
  </form>
  <div>Your average grade is {{ average }}</div>
</template><script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  data() {
    return {
      grades: [{ id: uuidv4(), value: 0 }],
      average: 0,
    };
  },
  computed: {
    formValid() {
      return this.grades.every(({ value }) => !isNaN(+value));
    },
  },
  methods: {
    addGrade() {
      this.grades.push({ id: uuidv4(), value: 0 });
    },
    deleteGrade(index) {
      this.grades.splice(index, 1);
    },
    calculate() {
      if (!this.formValid) {
        return;
      }
      this.average =
        this.grades.map(({ value }) => value).reduce((a, b) => a + b, 0) /
        this.grades.length;
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单，让我们用`calculate`方法处理表单提交。

`prevent`修饰符让我们做客户端提交，而不是服务器端。

在里面，我们用`v-for`为每个年级条目渲染 div。

在每个 div 中，我们有一个输入字段，它通过`v-model`绑定到`grade.value`属性。

`number`修饰符将输入值转换成一个数字。

删除成绩按钮被设置为`type` `button`，这样当我们点击它时它就不会提交表单。

它调用`deleteGrade`删除给定`index`处的等级条目。

在那下面，我们有添加等级按钮，当我们点击它时通过调用`addGrade`来添加等级。

在它下面，我们有一个提交表单的按钮。

div 用于显示平均成绩。

在脚本标签中，我们有返回`grades`数组和`average`的`data`方法。

它们都是活性物质。

`formValid`计算属性用`isNaN`函数检查每个`grades`条目的`value`属性是否是一个数字。

在那下面，我们有我们称之为。

`addGrade`方法调用`push`向`this.grades`数组添加一个新条目。

`uuidv4`返回一个 UUID 字符串，这样我们就可以给条目添加一个 ID。

我们需要惟一的 ID，这样 Vue 3 就可以识别呈现的条目。

我们将其设置为`key`属性的值，使其成为该行的唯一标识符。

`deleteGrade`方法调用`splice`删除带有`index`的条目，调用 1 删除带有给定`index`的条目。

`calculate`方法调用`map`来返回包含每个`grades`条目的`value`的数组。

然后它调用`reduce`将数字加在一起。第二个参数中的 0 是初始值。

然后总数除以`this.grades.length`得到平均值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个成绩计算器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)