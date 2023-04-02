# 通过 google-translate-api 在 Node.js 应用中使用 Google Translate API

> 原文：<https://javascript.plainenglish.io/using-google-translate-api-in-our-node-js-app-with-google-translate-api-3d4a3cf26d39?source=collection_archive---------11----------------------->

![](img/6c49856a3a3ccc6842f95f5ef13e3f9d.png)

Photo by [Gilly Stewart](https://unsplash.com/@gillystewart?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`google-translate-api`模块让我们在服务器端 JavaScript 应用中使用 Google Translate API。

在本文中，我们将研究如何在 Node.js 应用程序中使用这个包。

# 装置

我们可以通过运行以下命令来安装该软件包:

```
npm install @vitalets/google-translate-api
```

# 使用

我们可以使用这个模块附带的`translate`函数来进行翻译。

例如，我们可以写:

```
const translate = require('@vitalets/google-translate-api');

(async ()=>{
  try {
    const res = await translate('je parle français', { to: 'en' })
    console.log(res.text);    
    console.log(res.from.language.iso);
  }
  catch (error){
    console.log(error)
  }
})()
```

`translate`以结果回报承诺。

第一个参数是我们要翻译的文本。

第二个参数有`to`属性，它是我们要翻译的语言的代码。

`res.text`有由此产生的文字。

而`res.from.language.iso`拥有第一个参数中文本的语言代码。

谷歌翻译 API 可以处理有错别字的文本。

例如，我们可以写:

```
const translate = require('@vitalets/google-translate-api');

(async ()=>{
  try {
    const res = await translate('I spea French', { from: 'en', to: 'fr' })
    console.log(res.text);    
    console.log(res.from.text.autoCorrected);    
    console.log(res.from.text.value);    
    console.log(res.from.text.didYouMean);
  }
  catch (error){
    console.log(error)
  }
})()
```

我们传入有错别字的`‘I spea French’`。

`from`有原文的语言 oif。

`res.text`有没有错别字的翻译结果。

`res.from.text.autoCorrected`具有布尔值，表明原始文本是否被自动更正。

`res.from.text.value`有文本的自动修正版本。

`res.from.text.didYouMean`是`true`表示 API 建议对源语言进行更正。

所以我们得到:

```
je parle français
true
I [speak] French
false
```

从 4 个控制台日志中。

我们也可以在列表中添加我们自己的语言。

例如，我们可以写:

```
const translate = require('@vitalets/google-translate-api');
translate.languages['sr-Latn'] = 'Serbian Latin';(async ()=>{
  try {    
    const res = await translate('I spea French', { to: 'sr-Latn' })
    console.log(res.text);    
  }
  catch (error){
    console.log(error)
  }
})()
```

然后我们得到:

```
Говорим француски
```

从控制台日志中。

# 代理人

我们可以通过这个库的代理发出请求。

为此，我们写道:

```
const translate = require('@vitalets/google-translate-api');
const tunnel = require('tunnel');(async ()=>{
  try {    
    const res = await translate('I spea French', { 
      to: 'fr',
      agent: tunnel.httpsOverHttp({
        proxy: { 
          host: '138.68.60.8',
          proxyAuth: 'user:pass',
          port: '8080',
          headers: {
            'User-Agent': 'Node'
          }
        }
      })
    })
    console.log(res.text);    
  }
  catch (error){
    console.log(error)
  }
})()
```

我们使用`tunnel`库通过代理发出请求。

我们使用代理选项和凭证调用`tunnel.httpOverHttp`方法，通过代理发出翻译请求。

# 结论

我们可以使用`google-translate-api`模块，让我们在服务器端 JavaScript 应用程序中使用 Google Translate API。

*阅读更多尽在* [***说白了. io***](https://plainenglish.io/)