# 用 Vue 3 和 JavaScript 创建一个预算跟踪程序

> 原文：<https://javascript.plainenglish.io/create-a-budget-tracker-app-with-vue-3-and-javascript-351fa8957cf2?source=collection_archive---------14----------------------->

![](img/c8e56f0cf885aba2098af115e21fdd55.png)

Photo by [StellrWeb](https://unsplash.com/@stellrweb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个待办事项应用程序。

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
vue create budget-tracker
```

并选择所有默认选项来创建项目。

我们还需要`uuid`包来为我们的杂货清单项目生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建预算跟踪器

预算跟踪器让我们输入预算和费用项目。

为此，我们写道:

```
<template>
  <div>
    <form>
      <fieldset>
        <label>budget</label>
        <input v-model.number="budget" />
      </fieldset>
    </form> <form @submit.prevent="add">
      <h1>add expensse</h1>
      <fieldset>
        <label>description</label>
        <input v-model="expense.description" />
      </fieldset> <fieldset>
        <label>cost</label>
        <input v-model.number="expense.cost" />
      </fieldset>
      <button type="submit">add expense</button>
    </form> <p>remaining budget: ${{ remainingBudget }}</p> <div v-for="(item, index) of expenses" :key="item.id">
      {{ item.description }} - ${{ item.cost }}
      <button @click="remove(index)">remove</button>
    </div>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  data() {
    return {
      expense: {
        description: "",
        cost: 0,
      },
      expenses: [],
      budget: 0,
    };
  },
  computed: {
    expenseValid() {
      const { cost, description } = this.expense;
      return +cost >= 0 && description.length > 0;
    },
    remainingBudget() {
      const { budget, expenses } = this;
      const totalExpenses = expenses
        .map(({ cost }) => cost)
        .reduce((a, b) => a + b, 0);
      return budget - totalExpenses;
    },
  },
  methods: {
    add() {
      if (!this.expenseValid) {
        return;
      }
      this.expenses.push({
        id: uuidv4(),
        ...this.expense,
      });
      this.expense = {};
    },
    remove(index) {
      this.expenses.splice(index, 1);
    },
  },
};
</script>
```

第一个表单元素有一个输入字段，让我们输入预算。

`v-model`将输入的值绑定到`budget`反应属性。

`number` reactive 属性将我们输入的内容转换成一个数字。

类似地，我们有第二个表单元素让我们输入费用项目。

它具有`description`和`cost`属性。

add expense 按钮触发第二个表单上的 submit 事件，并调用`add`方法将费用项添加到`expenses`反应属性数组中。

`p`元素呈现`remainingBudget`计算属性，该属性包含预算减去总支出。

并且`v-for`指令呈现我们输入的费用项目。

在 component 对象中，我们有带有 reactive 属性的`data`方法，通过返回一个包含这些属性的对象来初始化。

我们用`expenseValid`计算属性来检查`expense` 字段是否有效。

`remainingBudget`计算`budget`减去从`expenses`项计算的总费用。

在`methods`中，我们有`add`方法，通过调用`this.expenses.push`来添加预算项目。

我们用`uuidv4`函数为每个条目生成一个惟一的 ID。

`remove`方法通过索引`splice`删除一个`expenses`条目。当我们点击它时，它被称为删除按钮。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个预算跟踪程序。

*查看更多内容请点击*[***plain English . io***](https://plainenglish.io/)