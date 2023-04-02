# 在 React Native 中生成带有标题的 Get 请求以呈现图像

> 原文：<https://javascript.plainenglish.io/react-native-making-get-request-to-display-the-image-f75d4338c5e2?source=collection_archive---------6----------------------->

React 本地移动开发人员经常会有这样的需求，即必须通过发出 get 请求来完成图像渲染，该请求包含一些标头以提供额外的安全性。

![](img/d9f45e19172b1772b9d6b43a789be29a.png)

Soure — [https://unsplash.com/](https://unsplash.com/)

React native 提供了通过网络调用渲染图像的灵活性，下面是解释它的最简单的代码片段。

```
<Image  
source={{    
uri: 'https://reactjs.org/logo-og.png',
method: 'POST',
headers: 
{
Pragma: 'no-cache'
},
body: 'Your Body goes here'  
}} 
style={{ width: 400, height: 400 }}/>
```

如果您有任何自定义标头，如 auth token、userId 等，则在标头部分传递它，如果需要，您可以将请求类型更改为 GET(如下所示)。

```
<Image  
source={{    
uri: 'https://reactjs.org/logo-og.png',
method: 'GET',
headers: 
{
auth: 'YOUR_TOKEN_GOES_HERE',
userId : 'YOUR USER ID GOES HERE'
},
body: 'Your Body goes here'  
}} 
style={{ width: 400, height: 400 }}/>
```

但是上面的代码看起来有点乱，如果你在一个容器组件中有多个图像标签，那么你的代码行数会因此而增加。我们可以通过创建实用方法来优化它，以获得标题和正文。(如下图所示)。

```
<Image  
source={{    
uri: 'https://reactjs.org/logo-og.png',
method: 'GET',
headers: yourUtitlityClass.getHeaders(),
body: yourUtitlityClass.getBody()
}} 
style={{ width: 400, height: 400 }}/>
```

现在有另一个场景，更大尺寸的图像可能需要时间来加载，在这种情况下，我们需要显示一个加载器，直到图像被加载。但是如何知道图像何时开始下载，何时完成加载？为了解决这个问题，Image 标签公开了接受函数的 **onLoadStart** 和 **onLoadEnd** prop。我们可以用它来显示 loader，直到图像被加载。下面的片段解释了它，

```
...
const [showImageLoader, setShowImageLoader] = useState(true);
...<View >
  <Image  
   source={{    
   uri: 'https://reactjs.org/logo-og.png',
   method: 'GET',
   headers: yourUtitlityClass.getHeaders(),
   body: yourUtitlityClass.getBody()
   }} 
   style={{ width: 400, height: 400 }}
   onLoadStart={() => setShowImageLoader(true)}
   onLoadEnd={() => setShowImageLoader(false)}
/>{showImageLoader && <Spinner small />}</View>
```

现在只有优秀程序员才会意识到这一点，如果 API 调用失败了怎么办？？由于网络问题或服务器停机，如何处理这种情况？在这种情况下，上面的代码片段将永远显示加载程序。为了避免图像标记，还会给出一个适当错误，该错误可用于处理 API 故障。下面的片段(最后一个)包含它。(您可以扩展这个示例，以便在 API 失败时显示一些错误 UI。)

```
...
const [showImageLoader, setShowImageLoader] = useState(true);
...<View >
  <Image  
   source={{    
   uri: 'https://reactjs.org/logo-og.png',
   method: 'GET',
   headers: yourUtitlityClass.getHeaders(),
   body: yourUtitlityClass.getBody()
   }} 
   style={{ width: 400, height: 400 }}
   onLoadStart={() => setShowImageLoader(true)}
   onLoadEnd={() => setShowImageLoader(false)}
   onError={() => setShowImageLoader(false)}
/>{showImageLoader && <Spinner small />}</View>
```

参考 react 本地官方[链接](https://reactnative.dev/docs/images#network-requests-for-images)了解更多关于图像标签的信息。

**同一作者的更多文章:**

1.  [JavaScript 中的一切都是对象吗？](https://mevasanth.medium.com/how-everything-is-object-in-javascript-a4164d7e6a2d)
2.  [异步 Await 函数返回值的问题](/problem-with-returning-values-from-async-await-function-javascript-e99c94a47ca5)
3.  [JavaScript 中的提升:访谈热点](https://mevasanth.medium.com/hoisting-in-javascript-hot-topic-for-interview-43b463a6a77?source=follow_footer---------0----------------------------)
4.  [JavaScript 中的记忆化——采访热门话题](https://mevasanth.medium.com/memoization-in-javascript-hot-topic-for-interview-815475544ab0)

在这里阅读作者[的所有文章。](https://mevasanth.medium.com/)