# 反应中的复合组分模式

> 原文：<https://javascript.plainenglish.io/compound-component-pattern-in-react-13ee74b819f8?source=collection_archive---------5----------------------->

## React 中的组件模式指南

![](img/9e2ed23e18cfa69b162a9d41625ac5b8.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/reactjs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

*注意:很好地理解*[*React Context API*](https://reactjs.org/docs/context.html)*以便能够理解这一部分是很有用的。*

看看下面这段来自 react UI 库 [Ant Design](https://ant.design/) 的代码片段。 [*菜单*](https://ant.design/components/menu/) 组件具有看似特殊的属性，称为*项目*和*子菜单*。

```
<Menu>
  <Menu.Item>Menu</Menu.Item>
  <Menu.SubMenu title="SubMenu">
    <Menu.Item>SubMenuItem</Menu.Item>
  </Menu.SubMenu>
</Menu>
```

这种创建组件的方式被称为复合组件模式。这个想法本质上是，这个例子中的组件*菜单*具有一些逻辑，这些逻辑在这个例子中的属性*项目*和*子菜单*之间共享。想想 HTML 中的 select 和 option 标签。他们打算一起工作。

为了便于解释，让我们举一个简单的例子，看看 Ant design 如何在*菜单*组件中使用复合组件模式来为*菜单*提供主题。Ant Design 使用的默认主题是 light，如下图所示。

```
**Default Props provided to the *Menu* component** ([Source](https://github.com/ant-design/ant-design/blob/756a1dffea3b8f00876e61fd13f7ceb9ddc561b1/components/menu/index.tsx#L26))**.**static defaultProps: Partial<MenuProps> = {
    className: '',
    ***theme: 'light', // or dark***
    focusable: false,
  };
```

实现复合组件模式的方法是使用上下文 API。*菜单*组件使用上下文提供程序，并提供必须与*项目*和*子菜单*组件内部共享的值。此外，*项目*和*子菜单*组件消耗上下文，这导致状态在组件之间共享。

让我们看看*菜单的*组件是如何使用上述方法创建复合组件的。

```
**Creating the context in *Menu* component** ([Source](https://github.com/ant-design/ant-design/blob/756a1dffea3b8f00876e61fd13f7ceb9ddc561b1/components/menu/index.tsx#L74))<MenuContext.Provider
  value={{
    inlineCollapsed: this.getInlineCollapsed() || false,
    ***antdMenuTheme: theme,***
    direction,
  }}
>**Consuming the context in *SubMenu* Component** ([Source](https://github.com/ant-design/ant-design/blob/d5eda4f87e4c1bb605d08a2acea76c8eb7163a4d/components/menu/SubMenu.tsx#L57))<MenuContext.Consumer>
  {({ inlineCollapsed, ***antdMenuTheme*** }: MenuContextProps) => (
    <RcSubMenu
      {...omit(this.props, ['icon'])}
      title={this.renderTitle(inlineCollapsed)}
      popupClassName={classNames(
        rootPrefixCls,
        ***`${rootPrefixCls}-${antdMenuTheme}`,***
        popupClassName,
      )}
    />
  )}
</MenuContext.Consumer>
```

注意*菜单*组件创建了一个上下文并提供了*主题的值。*该值随后在*子菜单*组件中被消耗。因此，复合组件模式是使用上下文 API 创建的。

这里是 [React Bootstrap](https://react-bootstrap.github.io/) 使用的复合组件模式的另一个例子。这个例子使用了带有[模态](https://react-bootstrap.github.io/components/modal/)的模式。

```
**Compound component in React Bootstrap** ([Source](https://react-bootstrap.github.io/components/modal/))<Modal.Dialog>
  <Modal.Header closeButton>
    <Modal.Title>Modal title</Modal.Title>
  </Modal.Header>
  <Modal.Body>
    <p>Modal body text goes here.</p>
  </Modal.Body>
  <Modal.Footer>
    <Button variant="secondary">Close</Button>
    <Button variant="primary">Save changes</Button>
  </Modal.Footer>
</Modal.Dialog>
```

React bootstrap 还利用上下文 API 来实现该模式。

# 为什么要复合成分？

我确信这种模式一定引起了你的兴趣，但是你可能仍然想知道这种模式的必要性。

*   让我们假设 React Bootstrap 为 Modal 提供了一个类似这样的 API

```
**Alternative internal implementation of the Modal Component**const Modal = ({title, body}) => {
  return(
    <div className="modal">
      <div className="modal-title">{title}</div>
      <div className="modal-body">{body}</div>
    </div>
  )
}**Consuming the Modal component**<Modal title={...} body={...}/>
```

当用户传递所需的道具时，它肯定会工作。然而，当显示模式时，API 有一个非常严格的方法。使用复合组件方法，用户可以灵活选择是否显示*模态。标题*。用户还可以灵活选择显示顺序。不管出于什么原因，仍然可以显示*模态。正文*在*情态之前。标题*。

*   让我们再举一个例子，其中的用例是在点击按钮时切换内容。这个想法是利用组件之间隐式共享的状态。

```
**Creating the Compound Component Pattern**import React, { useContext, useState } from "react";*// creating the context*
const TogglerContext = React.createContext();const Toggler = ({ children }) => {
  // this state will be shared
  const [value, setValue] = useState(false); const toggle = () => {
    setValue((prevValue) => !prevValue);
  }; return (
    *// using context to share the state between the components* <TogglerContext.Provider value={{ value }}>
      <div>
        <div role="button" onClick={toggle}>
          Toggle Description
        </div>
        {children}
      </div>
    </TogglerContext.Provider>
  );
};const Data = ({ children }) => {
  *// Consuming the context*
  const TogglerContextConsumer = useContext(TogglerContext);
  return TogglerContextConsumer.value && <>{children}</>;
};**Using the Compound Component Pattern**<Toggler>
  <Data>
    <p>I will get toggled when you click the button.</p>
  </Data>
</Toggler>
```

注意*数据*组件如何利用 *Toggler* 组件中定义的状态变量来[有条件地呈现](https://reactjs.org/docs/conditional-rendering.html)的子组件。本质上，这两个组件之间存在内部状态共享，这为最终用户提供了一个灵活的 API。上面的代码片段是一个非常基本的例子来说明这个想法。

您一定已经注意到，与复合组件模式相关联的组件通常被声明为*模态*、*模态。标题*，*模态。标题*，等等。这种符号有助于在相关组件之间建立心理联系。让我们快速地将我们的例子从*托格勒*修改为*托格勒.数据.*

```
// Add the following line just after the Data component.
Toogler.Data = Data;**Using the Modified Compound Component Pattern**<Toggler>
  <Toggler.Data>
    <p>I will get toggled when you click the button.</p>
  </Toggler.Data>
</Toggler>
```

# 结论

复合组件模式允许我们表达组件之间的关系。组件共享状态，这意味着状态被所涉及的组件内部使用和操纵。该模式提供了一个更简洁的 API，并使用 react 上下文实现。

既然你已经理解了这个模式，让我们开始使用它吧！