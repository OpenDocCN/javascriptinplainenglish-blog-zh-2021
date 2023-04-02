# 用 Vue 3 和 JavaScript 创建一个地址簿应用

> 原文：<https://javascript.plainenglish.io/create-an-address-book-app-with-vue-3-and-javascript-908a875ce542?source=collection_archive---------8----------------------->

![](img/3a4507486544e9e3a080db79667c877c.png)

Photo by [Paulina Garcia](https://unsplash.com/@pauucastillo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个地址簿应用程序。

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
vue create address-book
```

并选择所有默认选项来创建项目。

我们还需要安装`uuid`包，这样我们就可以为每个成绩条目生成唯一的 id。

要安装它，我们运行:

```
npm i uuid
```

# 创建地址簿

为了创建地址簿应用程序，我们编写:

```
<template>
  <form @submit.prevent="addContact">
    <div>
      <label>name</label>
      <input v-model="contact.name" />
    </div>
    <div>
      <label>address</label>
      <input v-model="contact.address" />
    </div>
    <div>
      <label>phone</label>
      <input v-model="contact.phone" />
    </div>
    <button type="submit">add</button>
  </form>
  <div v-for="(contact, index) of contacts" :key="contact.id">
    <p>name: {{ contact.name }}</p>
    <p>address: {{ contact.address }}</p>
    <p>phone: {{ contact.phone }}</p>
    <button type="button" @click="deleteContact(index)">delete </button>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";export default {
  name: "App",
  data() {
    return {
      contact: {
        name: "",
        address: "",
        phone: "",
      },
      contacts: [],
    };
  },
  computed: {
    formValid() {
      const { name, address, phone } = this.contact;
      return (
        name &&
        address &&
        /^[(]{0,1}[0-9]{3}[)]{0,1}[-\s\.]{0,1}[0-9]{3}[-\s\.]{0,1}[0-9]{4}$/.test(
          phone
        )
      );
    },
  },
  methods: {
    addContact() {
      if (!this.formValid) {
        return;
      }
      const { name, address, phone } = this.contact;
      this.contacts.push({ id: uuidv4(), name, address, phone });
    },
    deleteContact(index) {
      this.contacts.splice(index, 1);
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单来监听由 add 按钮触发的提交事件。

`prevent`指令让我们在客户端而不是服务器端提交表单。

在它里面，我们有输入字段，让我们添加联系人的姓名、地址和电话号码。

在此之下，我们用`v-for`指令呈现 div，以呈现`contacts`反应属性数组的内容。

`key` prop 是必需的，它应该是一个惟一的 ID，以便 Vue 3 能够正确识别条目。

在其中，我们呈现了`contact`的`name`、`address`和`phone` 属性。

我们添加了一个删除按钮，以便可以删除联系人。

在脚本标签中，我们在`data`方法中返回反应属性。

`formValid`计算属性检查`name`、`address`和`phone`是否有效。

我们用正则表达式检查电话号码。

我们允许前缀用括号括起来，段之间用破折号，总共 10 个数字。

`test`方法让我们检查一个字符串是否匹配给定的 regex 对象。

在`addContact`方法中，我们检查`formValid`是否所有的值都有效。

如果是，那么我们调用`push`将一个条目添加到`contacts`数组中。

`uuidv4`生成条目的唯一 ID。

`deleteContact`删除与`splice`和`index`的联系。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松添加通讯录。

*更多内容看*[***plain English . io***](https://plainenglish.io/)