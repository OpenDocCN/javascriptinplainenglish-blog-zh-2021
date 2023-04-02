# 用故事书记录受控组件

> 原文：<https://javascript.plainenglish.io/a-guide-to-documenting-controlled-components-with-storybook-10b889c03f87?source=collection_archive---------2----------------------->

## 管理外部故事书状态指南

![](img/81cb77b4b844e997d699e41d4c8a34a0.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

[Storybook 是一个奇妙的组件浏览器和游乐场](https://medium.com/javascript-in-plain-english/storybook-is-your-new-ui-component-explorer-22e9e69b9d0f)。我用它来开发、演示和记录我代码库中的所有组件。用户可以了解组件的工作原理和控制方式。但是，尽管为按钮、网格和表格等无状态组件设置故事很简单，但需要外部状态的组件(如表单输入)需要更多的配置。

# 故事书

先说一点背景。让我们看看这个输入组件

```
const Input = props => {
  const { className, onChange, type, value } = props;
  return (
    <input
      className={className}
      onChange={e => onChange(e.target.value)}
      type={type}
      value={value}
    />
  );
};
```

为该组件编写的故事如下所示:

```
import Input from './Input';export default {
  title: 'Input',
  component: Input,
};const Template = args => <Input {...args} />export const Default = Template.bind({});export const Number = Template.bind({});
Number.args = {
  type: 'number',
};export const Password = Template.bind({});
Password.args = {
  type: 'password',
};export const Value = Template.bind({});
Value.args = {
  value: 'value',
};
```

模板是一个抽象层，可以减少冗余代码的数量。每个命名的导出创建这个模板的副本，并通过`args`定义故事的道具。Storybook 将采用这些并以导出名称作为标题展示故事。

# 状态

由于这个`Input`组件要求您提供`onChange`和`value`，我们需要使用 Storybook 以某种方式管理这个状态。但是在哪里？如果你仔细看看，模板本身就是一个 React 功能组件，因此，我们可以使用`useState`钩子来管理输入状态！

```
const Template = args => {
  const [value, setValue] = useState(args.value ?? '');
  return (
    <>
      <Input
        {...args}
        onChange={(...params) => {
          args.onChange(...params);
          setValue(...params);
        }}
        value={value}
      />
      <pre style={{ marginTop: 10 }}>
        {JSON.stringify({ value }, null, 2)}
      </pre>
    </>
  );
};
```

*   初始状态设置为`args.value`。这是为了让我们可以有一个定义价值的故事来演示这个道具是如何工作的。
*   为`Input`定义的`onChange`函数不仅触发状态钩子更新器，还触发`args.onChange`。默认故事书设置自动为所有匹配`^on[A-Z].*`正则表达式的道具注入一个[故事书动作记录器](https://www.npmjs.com/package/@storybook/addon-actions)。注入的函数将在 actions 选项卡中记录每个函数调用及其参数，以便用户可以了解它是何时以及如何被触发的。
*   `pre`标签显示状态值。虽然不是完全必要的，但是这个状态值对于组件如何工作是必不可少的，所以呈现它有助于用户更好地理解组件。

有了这个模板更改，我们的`Input`组件现在可以像预期的那样交互了。

# 控制

如果您正在使用[故事书的控件插件](https://www.npmjs.com/package/@storybook/addon-controls)(自动包含在[故事书必备品](https://www.npmjs.com/package/@storybook/addon-essentials)中)，控制值道具的控件也应该被禁用。由于该值是通过`setState`控制的，所以如果在控制选项卡中改变了正确的值，将不会发生任何事情。

```
export default {
  title: 'Input',
  component: Input,
  argTypes: {
    // controlled value prop
    value: {
      control: {
        disable: true,
      },
    },
  },
};
```

注意，我们不需要禁用`onChange`，因为故事书控件是为功能道具自动禁用的。

# 最后的想法

故事书让我和我的团队受益良多。它使开发人员能够在一个地方展示和记录他们组件库的所有特性。使用这个简单的技巧来管理故事模板中的状态，甚至可以在故事书中记录受控制的组件，使用户能够在一个简单但强大的交互式操场上快速学习特性和功能。

# 资源

*   [官方故事书文档](https://storybook.js.org/)
*   [设置故事书指南](https://medium.com/javascript-in-plain-english/storybook-is-your-new-ui-component-explorer-22e9e69b9d0f)
*   [本条 Github 回购](https://github.com/mjchang/medium/tree/master/storybook-state)