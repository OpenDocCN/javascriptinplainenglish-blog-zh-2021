# 使用 React Native Expo 和 NewsAPI 构建新闻应用程序

> 原文：<https://javascript.plainenglish.io/cryptocurrency-news-app-using-react-native-expo-and-newsapi-c3f96ca3be20?source=collection_archive---------4----------------------->

## 面向初学者和中间用户的 Android 开发和 IOS 开发项目

![](img/d0814db5a0cb14b0d335940142c5aa2a.png)

Photo by [Jievani Weerasinghe](https://unsplash.com/@jievani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

比特币、Dogecoin、Etherium 和许多其他加密货币是过去两年来的主要热门术语。每个人都想投资他们，因为他们的回报更高。但在投资任何硬币之前，你必须关注市场情绪、新闻和许多其他事情。许多社交媒体平台提供与加密相关的新闻。但你不能依赖他们，对吗？因为你自担风险投资了自己的钱。所以，还是控制在自己手里比较好。

因此，让我们使用 react native expo 制作一个加密货币新闻应用程序，在这里您可以从有效的来源获得所有与加密硬币相关的新闻。喝杯咖啡，让我们开始吧。

如果您正在寻找视频教程，那么它就在这里:

# 设置和安装

*   使用以下命令打开系统中的一个目录并启动一个 expo 项目:

```
expo init NewsApp
```

*   选择空白的 Javascript 模板并继续下载 Javascript 依赖项。
*   移动到新目录(“NewsApp”)
*   安装以下依赖项:

```
npm install axios
npm install react-native-paper
```

*   现在，在[新闻 API](https://newsapi.org/) 上创建您的帐户。从这个网站，你会得到你的 API 密匙。我们将使用这个 API 键来获取我们感兴趣的新闻

我们已经完成了项目设置和安装。让我们快速跳到代码部分。

# React Native Expo 中的新闻 App 代码

在父目录中创建两个文件夹。一个是组件，一个是屏幕。在组件文件夹中，我们将制作标题。

**组件/AppBar.js**

```
import * as React from 'react';
import { Appbar } from 'react-native-paper';const Header = () => {return (
    <Appbar.Header style={{marginTop:40, backgroundColor:'blue'}}>

      <Appbar.Content title="Home" />

    </Appbar.Header>
  );
};export default Header;
```

嗯，这是一个简单的标题。我用 react 本地纸做页眉。你也可以使用其他 javascript 库，如 native base 或其他。

**screens/index.js**

我们将为屏幕使用一个基于类的组件。但是首先，让我们导入所有需要的组件。

```
import React, { Component } from 'react'
import { View, Text, Image, ScrollView, Linking } from 'react-native'
import axios from 'axios'
import { Card, Title, Paragraph } from 'react-native-paper'import Header from '../../components/AppBar'
```

现在，在基于类的组件中，添加以下代码。

```
state = {
        articles: [],
        isLoading: true,
        errors: null
    };
```

定义各州。

```
getArticles() {
        axios
          .get(
            "[https://newsapi.org/v2/everything?q=Cryptocurrency&from=2021-09-08&sortBy=popularity&apiKey=API_KEY](https://newsapi.org/v2/everything?q=Cryptocurrency&from=2021-09-08&sortBy=popularity&apiKey=API_KEY)"
          )
          .then(response =>
            response.data.articles.map(article => ({
              date: `${article.publishedAt}`,
              title: `${article.title}`,
              url: `${article.url}`,
              description: `${article.description}`,
              urlToImage: `${article.urlToImage}`,
            }))
          )
          .then(articles => {
            this.setState({
              articles,
              isLoading: false
            });
          })
          .catch(error => this.setState({ error, isLoading: false }));
    }componentDidMount() {
        this.getArticles();
    }
```

现在使用 Axios 获取新闻。但是首先，**更新你的 API 密匙**。在这里，我以加密货币的形式发送查询，如果你想要板球相关的新闻，那么你可以将其改为板球。新闻 API 将为您获取板球新闻。

之后，具体说明我们的要求。在这种情况下，我们将获取日期、标题、URL、描述和 urlToImage。

成功提取后，更改状态。现在，我们的空数组状态将被我们获取的数据更新。成功提取后，loading 将被设置为 false。

```
render(){const{ isLoading, articles } = this.state;return (<View><Header/><ScrollView>{!isLoading ? (articles.map(article => {const {date, title, url, description, urlToImage} = article;return(<Card key={url} style={{marginTop:10, borderColor:'black', borderRadius:5, borderBottomWidth:1}}onPress={()=>{Linking.openURL(`${url}`)}}><View style={{flexDirection:'row',}}>{/*  Text */}<View style={{justifyContent:'space-around', flex:2/3, margin:10}}><Title>{title}</Title></View>{/*  Image */}<View style={{flex:1/3, margin:10}}><Image style={{width:120, height:120}} source={{uri: urlToImage}} /></View></View><View style={{margin:10}}><Paragraph>{description}</Paragraph><Text>Published At: {date}</Text></View></Card>);})) : (<Text style={{justifyContent:'center', alignItems:'center'}}>Loading...</Text>)}</ScrollView></View>)}
```

不用担心上面的代码，你会获得完整的 Github 代码访问权。

在卡片中，我们将呈现我们的数据。卡片是可点击的。当你点击一张卡片时，你的默认浏览器会打开一个指定的网址。

在手机屏幕上，你会看到，新闻标题，图片，新闻描述，发布时间。您可以自定义 UI 部件。我知道你是专业设计师。

但是现在，在 **App.js** 中导入这些屏幕

**App.js**

```
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';import HomeScreen from './screens/HomeScreen';export default function App() {
  return (
    <View style={styles.container}>
      <HomeScreen/>
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
  },
});
```

现在，打开命令提示符窗口或终端窗口，使用以下命令运行该项目:

```
npm start
```

用移动设备扫描二维码。你可以用 Android 和 IOS 设备扫描，因为这个项目在这两种设备上都可以正常工作。

在成功构建 javascript 依赖关系之后。您将在移动设备屏幕上看到类似这样的内容。

![](img/d9ea0088f2b38cec006cf74ffac256cb.png)

News App using react native expo

我知道 UI 没那么酷。可以自定义。

**天气 app 的 Github 代码是** [**这里的**](https://github.com/imrohit007/React-Native-Expo-News-App) **。**

就是这样。

感谢您的阅读。如果这篇文章内容丰富，请确保关注并与您的社区分享，并关注更多内容。

你好，我叫 Rohit Kumar Thakur。我对自由职业持开放态度。我构建了 **react 原生项目**，目前正在开发 **Python Django** 。随时联系我(**freelance.rohit7@gmail.com**)

*更多内容看* [*说白了就是*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*