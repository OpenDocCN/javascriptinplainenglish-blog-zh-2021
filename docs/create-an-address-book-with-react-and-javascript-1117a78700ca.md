# 用 React 和 JavaScript 创建地址簿

> 原文：<https://javascript.plainenglish.io/create-an-address-book-with-react-and-javascript-1117a78700ca?source=collection_archive---------15----------------------->

![](img/88412f9c33a1bfc02d1b51c4dd7ab9fe.png)

Photo by [Paulina Garcia](https://unsplash.com/@pauucastillo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个地址簿应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app address-book
```

和 NPM 一起创建我们的 React 项目。

此外，我们必须安装`uuid`包，让我们为联系人条目分配唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建地址簿应用程序

为了创建地址簿应用程序，我们编写:

```
import React, { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [contact, setContact] = useState({
    name: "",
    address: "",
    phone: ""
  });
  const [contacts, setContacts] = useState([]); const addContact = (e) => {
    e.preventDefault();
    const { name, address, phone } = contact;
    const formValid =
      name &&
      address &&
      /^[(]{0,1}[0-9]{3}[)]{0,1}[-\s.]{0,1}[0-9]{3}[-\s.]{0,1}[0-9]{4}$/.test(
        phone
      );
    if (!formValid) {
      return;
    }
    setContacts((contacts) => [
      ...contacts,
      { id: uuidv4(), name, address, phone }
    ]);
  }; const deleteContact = (index) => {
    setContacts((contacts) => contacts.filter((_, i) => i !== index));
  }; return (
    <div className="App">
      <form onSubmit={addContact}>
        <div>
          <label>name</label>
          <input
            value={contact.name}
            onChange={(e) =>
              setContact((contact) => ({ ...contact, name: e.target.value }))
            }
          />
        </div>
        <div>
          <label>address</label>
          <input
            value={contact.address}
            onChange={(e) =>
              setContact((contact) => ({ ...contact, address: e.target.value }))
            }
          />
        </div>
        <div>
          <label>phone</label>
          <input
            value={contact.phone}
            onChange={(e) =>
              setContact((contact) => ({ ...contact, phone: e.target.value }))
            }
          />
        </div>
        <button type="submit">add</button>
      </form>
      {contacts.map((contact, index) => {
        return (
          <div key={contact.id}>
            <p>name : {contact.name}</p>
            <p>address : {contact.address}</p>
            <p>phone : {contact.phone}</p>
            <button type="button" onClick={() => deleteContact(index)}>
              delete
            </button>
          </div>
        );
      })}
    </div>
  );
}
```

我们定义了用于存储表单数据的`contact`状态。

并且定义了`contacts`状态来存储联系人条目。

接下来，我们定义`addContact`函数。

在里面，我们调用`e.preventDefault()`来做客户端提交。

然后我们检查`name`、`address`和`phone`值是否有效。

如果是，那么我们用一个回调函数调用`setContacts`，这个回调函数返回一个`contacts`数组的副本，并在末尾添加一个新的条目。

`uuidv4`返回联系人的唯一 ID。

`deleteContact`通过用回调函数调用`setContacts`来删除一个条目，该回调函数返回一个不包含给定`index`处条目的`contacts`数组的副本。

下面，我们添加一个表单，将`onSubmit`属性设置为`addContact`，这样当我们点击类型为`submit`的按钮时`addContact`可以运行。

在表单内部，我们用`value`属性定义了 3 个输入，以从状态中获取值。

它们的`onChange`属性被设置为调用`setContact`的函数，回调函数返回一个`contact`值的副本，但是使用它设置的属性的新值。

`e.target.value`有输入值。

在表单下面，我们通过使用回调函数调用`map`来呈现`contacts`状态，该回调函数返回一个 div，其中显示了每个`contact`条目的属性值。

将`key`属性设置为`contact.id`，以便 React 可以区分条目。

在那下面，我们显示了当我们点击它时用`index`调用`deleteContact`的删除。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个地址簿应用程序。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)