# 使用 Vue 测试工具对 Vue 应用进行单元测试——生命周期和异步测试

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-lifecycle-and-async-tests-1c7061ab7c0f?source=collection_archive---------11----------------------->

![](img/6c34340b6d648e6068352bfbebd9ad56.png)

Photo by [Aziz Acharki](https://unsplash.com/@acharki95?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 生命周期挂钩

当我们调用`mount`或`shallowMount`来安装我们的组件时，生命周期方法将被运行。

但是，`beforeDestroy`或`destroyed`方法不会被触发，除非用`wrapper.destroy()`手动销毁组件。

组件不会在每次测试结束时自动销毁，所以我们必须手动清理任何依赖关系。

# 编写异步测试

当我们编写测试时，我们必须意识到对反应性属性的任何更改都是异步完成的。

这意味着我们必须作为一个异步函数进行测试，或者使用`then`并运行我们的测试代码，该代码在`then`回调中更新了 reactive 属性之后运行。

例如，我们可以写:

```
import { shallowMount } from '@vue/test-utils'const Counter = {
  template: `
    <div>
      <button @click="count++">Add up</button>
      <p>clicks: {{ count }}</p>
    </div>
  `,
  data() {
    return { count: 0 }
  }
}describe('Counter', () => {
  it('renders new number when Add up button is clicked', async () => {
    const wrapper = shallowMount(Counter)
    const button = wrapper.find('button')
    const text = wrapper.find('p')
    await button.trigger('click')
    expect(text.text()).toBe('clicks: 1')
  })
})
```

到`await`的`trigger`方法，这样我们可以在更新完成后检查`count`反应属性的更新值。

我们也可以写:

```
import { shallowMount } from '@vue/test-utils'const Counter = {
  template: `
    <div>
      <button @click="count++">Add up</button>
      <p>clicks: {{ count }}</p>
    </div>
  `,
  data() {
    return { count: 0 }
  }
}describe('Counter', () => {
  it('renders new number when Add up button is clicked', () => {
    const wrapper = shallowMount(Counter)
    const button = wrapper.find('button')
    const text = wrapper.find('p')
    button.trigger('click')
      .then(() => {
        expect(text.text()).toBe('clicks: 1')
      })
  })
})
```

这是没有 async 和 await 的相同代码。

# 断言发出的事件

我们可以检查当我们对组件做一些事情时，发出了哪些事件。

为此，我们可以调用`emitted`方法来检查发出了哪些事件。

例如，我们可以写:

```
import { shallowMount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <button @click="$emit('foo')">emit foo</button>
    </div>
  `,
}describe('Foo', () => {
  it('emits foo event when the emit foo button is clicked', async () => {
    const wrapper = shallowMount(Foo)
    const button = wrapper.find('button');
    await button.trigger('click')
    expect(wrapper.emitted().foo).toBeTruthy()
  })
})
```

我们有`Foo`组件，当我们单击它时，它调用`$emit`来发出`'foo'`事件。

然后在测试的最后一行，我们调用`wrapper.emitted()`来检查是否发出了`foo`事件。

如果发出了，那么`foo`属性应该为 the。

我们还可以检查哪个有效载荷被发射。例如，我们可以写:

```
import { shallowMount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <button @click="$emit('foo', 123)">emit foo</button>
    </div>
  `,
}describe('Foo', () => {
  it('emits foo event with payload 123 when the emit foo button is clicked', async () => {
    const wrapper = shallowMount(Foo)
    const button = wrapper.find('button');
    await button.trigger('click')
    expect(wrapper.emitted().foo.length).toBe(1)
    expect(wrapper.emitted().foo[0]).toEqual([123])
  })
})
```

我们检查`foo`属性的`length`,看看它发出了多少次。

并且通过访问`foo`的数组值并检查内容来检查有效载荷。

# 结论

我们可以检查事件是否被发出，并意识到像`destroy`这样的生命周期钩子不会自动运行。