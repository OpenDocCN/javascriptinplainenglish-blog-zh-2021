# 用类型脚本清除 React 中的 API

> 原文：<https://javascript.plainenglish.io/a-cleaner-api-for-react-ts-components-47d0704a508c?source=collection_archive---------1----------------------->

![](img/35981b38f715829892e54b3f6eba66c7.png)

Photo by [Danny Howe](https://unsplash.com/@dannyhowe?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我希望这篇文章能对如何利用 TypeScript 构建更好的 React 组件有所启发。这篇文章是致力于建立关注隐私的人工智能画廊[](https://taggr.ai/)**的成果。**

**在构建 [**taggr**](https://taggr.ai/) **，**的时候，我更深入地研究了 TypeScript，到目前为止，我很喜欢在编译时注释类型和捕捉错误的新增功能，而不是在运行时关闭。**

**起初，注释每个组件和功能可能会让人感到畏惧和额外的工作，但是随着代码库的规模和复杂性的增长，好处开始显现。**

**正确地输入组件和业务逻辑代码，可以为领域的实体保留唯一的真实来源，从而最大限度地减少跨应用程序层的人为错误。**

**另外，可以从 [OpenAPI](https://github.com/drwpow/openapi-typescript) 、 [GraphQL 模式](https://graphql-code-generator.com/docs/plugins/typescript) …中自动生成类型脚本定义，这是一个双赢的局面🎉**

**在构建 React 组件时，我尽量保持它们的 API 尽可能紧密和干净。🧹💨**

**边界清晰的组件易于重用、扩展，而且总体来说很好使用。**

**让我们分析一个具体的例子，说明如何使用 TypeScript 来实现更简洁的组件 API，好吗？**

# ****不要从组件中** *暴露* `*Prop*` *类型😧***

```
// paragraph.tsx
export type Props = {
  text: string; 
}const Paragraph = ({text}: Props) => <p>{text}</p>// title.tsx
// Title is now tightly coupled to paragraph.txs > Props
import {Props} from './paragraph' const Title = ({text}: Props) => <h1>{text}</h1>
```

## **为什么这样不好？**

*   **当直接公开**道具**类型时，没有什么能阻止其他开发者(甚至是你未来的自己😂)在应用程序的其他部分导入和扩展这些类型。这会破坏组件的封装，并在组件之间创建不必要的依赖关系。**
*   **对原始组件的属性类型的更改可能会破坏应用程序的其他部分💥**
*   **一个混乱的 API，模块导出组件和类型。这可以很快变成组件文件导出多种类型，所以要小心🧐**

# **更好的方法✅**

**不要直接公开组件属性类型。**不要**。**

**如果想要访问另一个组件的属性，这样我就不用重新声明特定于域的类型了，该怎么办？**

**组件的**属性**定义了组件与应用程序其余部分(或世界)的接口🌎).**

**如果你有一个`UserProfile`组件并且**道具**声明了一个`User`类型，你想在你的应用程序的其他地方使用它，它应该从`UserProfile`T10 中提取出来。**

**将特定领域的类型提取到`./types`中，以便它们可以在整个应用程序中重用。**

```
// user-types.ts
export interface User {
 name: string,
 age: number;
};// user-profile.tsx
import {User} from './user-types';type Props = {
 user: User,
 date: string, // other props
};const UserProfile = ({user, date}: Props) => ...
export default UserProfile;// user-list.tsx
import {User} from './user-types';type Props = {
 users: User[],
};const UserList = ({users}: Props) => ...
export default UserList;
```

## **如果我需要从其他地方访问组件的属性，该怎么办？**

**它们是想要访问组件类型的有效理由，比如用 [HOC](https://medium.com/javascript-scene/do-react-hooks-replace-higher-order-components-hocs-7ae4a08b7b58) s 增强组件。**

**让我们检查下一部分来解决这个问题！**

# **属性类型查找✨**

**我们可以利用 TypeScript 类型解析来实现正确的类型查找。**

1.  **设置属性类型查找帮助程序，“GetComponentProps ”:**

```
// utils.ts
export type GetComponentProps<T> = T extends
| React.ComponentType<infer P>
| React.Component<infer P>
? P
: never;
```

**2.定义我们想要扩展的组件，`Title`:**

```
// title.tsx
type Color = "RED" | "BLUE" | "GREEN";type Props = {
 title: string;
 color: Color;
};const Title = ({ title, color }: Props) => (
  <h1 style={{ color }}>{title}</h1>
);
export default Title;
```

**3.伸出`Title`组件，同时保持**全类型安全**:**

```
// title-wrapper.tsx
import Title from './title';
import {GetComponentProps} from './utils';type Props = GetComponentProps<typeof Title> & {
 onClick: () => void;
};const TitleWrapper = ({onClick, ...rest}: Props) => (
  <button onClick={onClick}>
    <Title {...rest} /> 
  </button>
);
export default TitleWrapper;// index.ts
import TitleWrapper from 'title-wrapper';// Full type safety and autocompletion! 🎉
const App = () =>  (
 <TitleWrapper
  title="Hello there"
  color="GREEN"
  onClick={() => window.alert("title pressed")} 
 />
);
```

**我们设法从`TitleWrapper`访问了`Title`的属性，没有手动暴露它们，也没有破坏封装，太棒了！🎉**