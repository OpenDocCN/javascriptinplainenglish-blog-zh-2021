# React-Native:补偿没有
标签

> 原文：<https://javascript.plainenglish.io/react-native-compensating-for-no-br-tag-5c44cd03f3d5?source=collection_archive---------8----------------------->

![](img/1686d2a9765d6e7a33ff5d9250c54841.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我使用 React Native 将 web 开发扩展到了智能手机开发领域，我遇到了一些已经很熟悉的开发技术的替代方法。

在制作网站时，虽然定义边距和填充可能更干净，但我经常使用`<br />`标签来快速定义垂直呼吸空间，并发现自己震惊地看到 React Native 没有这一功能。

> 我们是怎么分开的？

事实证明，用更好的东西来补偿它非常简单！我介绍:

没错。B 是大写的。但是通过下面的实现，我们有了更多的功能:

```
import React from "react";
import { StyleSheet, View } from "react-native";interface BrProps {
  double?: boolean;
  triple?: boolean;
  quad?: boolean;
};const baseHeight = 6;const makeStyles = ({
  double,
  triple,
  quad,
}: BrProps) => StyleSheet.create({
  br: {
    height: quad ?
    ? 4 * baseHeight
    : triple
      ? 3 * baseHeight
      double
        ? 2 * baseHeight
        : baseHeight
  }
});const Br: React.VFC<BrProps> = ({
  double,
  triple,
  quad,
}) => {
  const styles = makeStyles({
    double,
    triple,
    quad
  });
  return (
    <View style={styles.br}></View>
  );
}export default Br;
```

没错。我们制作了一个具有类似功能的标签，但是引入了双重、三重和四重属性，因此我们不必做这样的事情:

```
<Header>Wow, welcome to this site</Header>
<Br/>
<Br/>
<Br/>
<Text>Nice to see you managed to navigate here.</Text>
<Br/>
<Br/>
<Text>...I honestly didn't expect that!</Text>
```

相反，我们可以这样做:

```
<Header>Wow, welcome to this site</Header>
<Br triple/>
<Text>Nice to see you managed to navigate here.</Text>
<Br double/>
<Text>...I honestly didn't expect that!</Text>
```

![](img/4d826403654014018b704a44e9912584.png)

Photo by [Andre Tan](https://unsplash.com/@andredantan19?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 哇，这么大的进步！

# 空间大！

等等。

这可能是我在 Medium 上写过的最懒的帖子，但是我仍然想分享这个简单的组件，它实际上为我当前的项目节省了大量的工作。

因为如果这个世界上有一样东西我们已经够用了，那就是空间。如果地球上没有足够的水，那么太空中肯定有足够的空间。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)