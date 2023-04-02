# 故事书快照测试

> 原文：<https://javascript.plainenglish.io/storybook-snapshot-testing-3e2b7abeffea?source=collection_archive---------3----------------------->

## 用故事书故事进行自动笑话快照测试

![](img/61b740b4a145efe2ac6ae645b2ccccb0.png)

Photo by [Christina Hernández](https://unsplash.com/@chrismckflurry?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

随着组件库的成熟，我开始关注测试。因为这些组件是我的应用程序的可视化构建模块，所以我想使用 Jest 的快照来确保没有意外的视觉变化。在我开始编写测试后不久，我意识到有一种
似曾相识的感觉——我已经用 Storybook 编写了一堆类似的东西！

在 Storybook 中，[我通过为每个组件道具创建故事来演示我的组件的功能和特性](https://medium.com/javascript-in-plain-english/storybook-is-your-new-ui-component-explorer-22e9e69b9d0f)，这样用户可以直观地看到不同的变化并与之交互。用不同的道具渲染组件正是我在测试中所做的！既然我已经通过 Storybook 完成了展示组件库功能的所有工作，我可以利用它进行快照测试吗？

# 故事镜头

Storybook 的 Storyshot 插件就是这样做的:它将现有的 Storybook 故事重新用于 Jest 快照测试。它获取这些故事，并自动为每个故事创建快照。

# 设置

设置非常简单。简单地创建一个测试文件，可以通过 Jest 获得并运行 Storyshots 插件。

```
// Storybook.test.jsimport initStoryshots from '[@storybook/addon-storyshots](http://twitter.com/storybook/addon-storyshots)';initStoryshots();
```

# 测试

配置完成后，Storyshot 测试的行为将与其他快照测试完全相同。运行`jest`将运行测试套件。如果快照文件尚不存在，Jest 将创建它们。如果有，Jest 会将 Storyshot 快照与保存的快照进行比较，如果有任何不匹配，就会出错。运行`jest --update-snapshot`将重新生成保存的快照以解决任何错误。

# MDX

Storybook 支持降价(MDX)故事，如下所示。

```
// stories/Button.stories.mdximport { Meta, Story } from "[@storybook/addon-docs](http://twitter.com/storybook/addon-docs)/blocks";
import { Button } from "./Button";<Meta title="Example/Button MDX" component={Button} /># Button
## This is a demo of a Button markdown documentation page.- This is a primary button:<Story name="Primary">
  <Button label="Button" primary />
</Story>
```

Storyshots 也支持这类故事的快照测试。但是要做到这一点，Jest 需要能够理解和解析 markdown 语法。支持降价故事的[故事书文档插件](https://www.npmjs.com/package/@storybook/addon-docs)提供了`jest-transform-mdx`来完成这个任务。

```
// jest.config.js or "jest" field in package.json{
  "transform": {
    "^.+\\.mdx?$": "@storybook/addon-docs/jest-transform-mdx",
  }
}
```

现在，Storyshots 可以遍历所有的降价文件，并为所有的`Story`区块生成快照。

# 必需的功能道具

Storybook 的一个常见配置是为所有匹配`^on[A-Z].*`正则表达式的道具自动注入一个 [Storybook 动作记录器](https://www.npmjs.com/package/@storybook/addon-actions)函数。这个函数将记录对 Storybook actions 选项卡的每次调用，这样用户就可以了解它是何时以及如何被触发的。

```
// .storybook/preview.jsexport const parameters = {
  actions: { argTypesRegex: "^on[A-Z].*" },
}
```

不幸的是，这种注射不会发生在故事镜头中。这不是可选功能道具的问题，而是必需功能道具的问题(通过`PropTypes.func.isRequired`)。测试将失败，因为 PropType 检查失败。

为了解决这个问题，我们必须更新故事来手动添加值。

```
// stories/Header.stories.jsexport default {
  title: 'Example/Header',
  component: Header,
  args: {
    ...(process.env.NODE_ENV === 'test'
      ? {
          onLogin: () => {},
          onLogout: () => {},
          onCreateAccount: () => {},
        }
      : {}),
  },
};
```

通过检查`process.env.NODE_ENV`，我们可以有条件地添加值，只有当故事在测试中运行时，快照测试才能在测试环境中成功，动作记录器才能在故事书用户界面中工作。

# React 门户

如果您的任何组件使用 React Portals，您将需要模拟`createPortal`函数来从本质上禁用门户效应。Storyshots 对根 div ( `<div id=”root”>…</div>`)下的内容进行快照。如果您将内容导入到此之外的某个地方(如`document.body`)，Storyshot 将无法找到它，并且您的快照将会不完整。这段代码将模仿`createPortal`函数不执行门户效果，直接返回节点。

```
// Storybook.test.jsjest.mock('react-dom', () => {
  const original = jest.requireActual('react-dom');
  return {
    ...original,
    createPortal: node => node,
  };
});initStoryshots();
```

# 禁用/启用

遗憾的是，Storyshot 不能用于所有组件。例如，模式和工具提示组件只有在一些用户交互之后才可见。对这些组件的故事进行快照测试会得到交互元素(比如按钮)的快照，而不是模态和工具提示组件的快照，因此，这是一个没有意义的测试。为了防止这些，可以通过`parameters.storyshots.disable`在每个组件或故事的基础上禁用或启用故事镜头。

```
// stories/Page.stories.jsexport default {
  title: 'Example/Page',
  component: Page,
  parameters: {
    storyshots: { disable: true },
  },
};const Template = args => <Page {...args} />;export const LoggedIn = Template.bind({});
LoggedIn.args = {
  user: {},
};export const LoggedOut = Template.bind({});
LoggedOut.parameters = {
  storyshots: { disable: false },
};
```

请注意，即使对组件禁用了 Storyshots，您仍然可以为单个组件故事重新启用它。

# 其他配置选项

`initStoryshots`功能还可以采用额外的配置选项来定制 Storyshot 体验。以下是一些常见的配置:

**snapshotSerializer** 允许您传递自定义序列化程序的数组。如果因为 JS 框架(如样式化组件或情感)中的 CSS 而需要使用自定义序列化器，这是很有用的。

```
import initStoryshots from '[@storybook/addon-storyshots](http://twitter.com/storybook/addon-storyshots)';
import { styleSheetSerializer } from 'jest-styled-components/serializer';initStoryshots({
  snapshotSerializers: [styleSheetSerializer],
});
```

**测试**允许你为每个故事运行一个定制的测试功能。虽然对典型配置不是特别有用，但它可以与 Storyshot 的`multiSnapshotWithOptions`一起使用，为每个组件生成单独的快照文件，而不是为所有组件生成一个巨大的文件。

```
import initStoryshots, { multiSnapshotWithOptions } from '[@storybook/addon-storyshots](http://twitter.com/storybook/addon-storyshots)';initStoryshots({
  test: multiSnapshotWithOptions(),
});
```

**stories2snapsConverter** 允许你定制快照和故事的文件名和位置。例如:

```
import initStoryshots, { Stories2SnapsConverter } from '[@storybook/addon-storyshots](http://twitter.com/storybook/addon-storyshots)';initStoryshots({
  stories2snapsConverter: new Stories2SnapsConverter({
    snapshotsDirName: '__snapshots__',
    snapshotExtension: '.js.snap',
    storiesExtensions: ['.js', '.mdx'],
  }),
});
```

有关配置选项的完整列表，请参见 [Storyshot 文档](https://www.npmjs.com/package/@storybook/addon-storyshots#options)。

# 最后的想法

Storyshots 利用您所做的所有工作来创建您的故事书，并提供自动视觉测试。我的组件库有超过 50 个组件故事，每个组件故事有多达 12 个故事。总之，我在 5 分钟内生成了 300 多个测试。就这样，我的组件库得到了全面的测试。

# 资源

*   [官方故事书文档](https://storybook.js.org/)
*   [官方故事书 Storyshot 附加文档](https://www.npmjs.com/package/@storybook/addon-storyshots)
*   [故事书设置指南](https://medium.com/javascript-in-plain-english/storybook-is-your-new-ui-component-explorer-22e9e69b9d0f)
*   [本文 Github 回购](https://github.com/mjchang/medium/tree/master/storybook-storyshot)