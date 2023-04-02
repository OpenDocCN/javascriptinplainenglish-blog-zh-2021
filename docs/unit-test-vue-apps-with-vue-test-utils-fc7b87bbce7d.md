# 使用 Vue 测试工具对 Vue 应用进行单元测试

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-fc7b87bbce7d?source=collection_archive---------18----------------------->

![](img/f8b758603adb2ba47b2b097748f6f5a0.png)

Photo by [Siora Photography](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 装置

我们可以在运行 Vue CLI 来搭建应用程序时添加它。

我们从列表中选择单元测试，然后选择 Jest 来添加带有产品代码的测试框架。

# 使用

一旦我们添加了测试文件，我们就可以编写单元测试了。

在我们的单元测试中，我们可以像使用组件一样与组件进行交互。

为此，我们安装组件，并通过触发元素上的事件来与元素进行交互。

此外，我们可以模拟任何需要设置的数据和外部资源，以便进行测试。

这样，我们可以独立地运行我们的测试，而不依赖于任何会使测试不可靠的外部事物。

要编写我们的第一个测试，我们可以通过编写以下内容将测试添加到 tests/unit 文件夹中:

```
import { shallowMount } from '@vue/test-utils'const MessageComponent = {
  template: '<p>{{ msg }}</p>',
  props: ['msg']
}describe('MessageComponent', () => {
  it('renders props.msg when passed', () => {
    const msg = 'new message'
    const wrapper = shallowMount(MessageComponent, {
      propsData: { msg }
    })
    expect(wrapper.text()).toMatch(msg)
  })
})
```

我们有将`msg`道具的值呈现到屏幕上的`MessageComponent`。

在我们的测试中，在我们传递给`it`的回调中，我们调用`shallowMount`来挂载没有其子组件的组件。

`propsData`让我们传递测试所需的道具数据。

然后`wrapper.text()`方法返回呈现的文本。

我们使用`toMatch`来检查结果。

为了运行测试，我们运行`npm run test:unit`来运行单元测试，然后我们应该会看到一些绿色的文本来表明测试通过了。

# 模拟用户交互

我们也可以很容易地模拟用户交互。

为此，我们可以写:

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

我们有了想要测试的`Counter`组件。

它有一个按钮，当我们点击它时,`count`增加 1。

然后在测试中，我们调用`shallowMount`来挂载组件。

然后我们调用`wrapper.find`来获取按钮和`p`元素。

为了模拟按钮上的点击，我们调用`trigger`来触发点击事件。

`trigger` is async is 返回一个承诺，所以我们的测试回调必须是一个`async` 函数，我们必须`await`这个`trigger`方法。

然后我们用`text`方法检查 p 元素中显示的文本，看看文本是否已经更新。

# 结论

通过使用 Jest 和模拟用户动作，我们可以很容易地编写单元测试来测试 Vue 应用。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**