# 用 Node.js 和 TypeScript 创建 Reddit 帖子

> 原文：<https://javascript.plainenglish.io/post-to-reddit-using-its-api-32b7baf708b2?source=collection_archive---------17----------------------->

![](img/51eaf976701930ca39af2a03800452f8.png)

> 这篇文章是写给我的 [#100DaysOfCode](https://twitter.com/hashtag/100DaysOfCode?src=hashtag_click) 的**第二天**的。在这篇文章中，我将讨论如何使用 Node.js 和 TypeScript 以编程方式向 Reddit 发布内容。

## 获得认证

获取 Reddit 的身份验证令牌很复杂。

如果你有一个**业务**并计划用这个代币创收，请遵循[这个表格](https://docs.google.com/forms/d/e/1FAIpQLSezNdDNK1-P8mspSbmtC2r86Ee9ZRbC66u929cG2GX0T9UMyw/viewform)。

对于**个人**使用，导航至您的 Reddit [应用](https://www.reddit.com/prefs/apps)并滚动至页面底部。您应该会看到一个灰色按钮，上面写着“创建另一个应用程序…”。点击按钮并填写表格。成功提交此表单应该会生成

![](img/75ea0f73310c5ce9f2c8149ccc0ff8b5.png)

## 为您的应用奠定基础

Github Repo 跟进

*确保你已经安装了*[*node . js*](https://nodejs.org/en/)

**我更喜欢* [*纱*](https://yarnpkg.com/) *，但是如果你更喜欢*也可以用 npm 代替*

*复制这个`package.json`文件并运行`yarn install`来安装依赖项。*

```
*{
  "name": "reddit-post",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "dev": "ts-node index.ts"
  },
  "devDependencies": {
    "ts-node": "^10.1.0",
    "typescript": "^4.3.5"
  },
  "dependencies": {
    "dotenv": "^10.0.0",
    "snoowrap": "^1.23.0"
  }
}*
```

## *包装说明:*

*   *ts-node 是一个方便的工具，用于执行类型脚本文件，而不必先编译成 Javascript。*
*   *Javascript 的类型脚本超集。我只是用它来试着在日常项目中变得更舒服。*
*   *安全地管理。env 变量和您的 auth 令牌。*
*   *[snoowrap](https://github.com/not-an-aardvark/snoowrap) 提供了一个简单的接口来访问每个 reddit API 端点。*

## *创建一个. env 文件*

*。env 文件被用作远离 GitHub 的秘密密钥(比如我们的认证令牌)的最佳实践。确保有一个`.gitignore`文件，并在其中添加`.env`。*

*`.env`文件应该是这样的:*

```
*username = '<REDDIT USERNAME>'
password = '<REDDIT PASSWORD>'
clientId = 'CLIENT_ID'
clientSecret = 'CLIENT SECRET'*
```

*只要确保用 Twitter 提供的令牌替换掉`<>`文本。*

*确保你没有犯错误。env 文件到 Github 或任何其他版本控制系统。这些令牌非常重要，不应与任何人共享！*

## *执行 POST 请求*

1.  *在项目根目录下创建一个 index.ts 文件*
2.  *导入您之前安装的软件包*

```
*const snoowrap = require('snoowrap')
require('dotenv').config()*
```

1.  *创建配置对象来组织 Reddit 配置变量*

```
*const config = {
  username: process.env.username,
  password: process.env.password,
  clientId: process.env.clientId,
  clientSecret: process.env.clientSecret,
}*
```

1.  *创建一个向 [Reddit 的端点](https://www.reddit.com/dev/api#POST_api_submit) `/api/submit`发送 POST 请求的函数，该函数带有 title、link 和 subreddit 参数。*

```
*function postLink(title: string, link: string, subreddit: string) {
  const r = new snoowrap({
    userAgent: 'Whatever',
    clientId: config.clientId,
    clientSecret: config.clientSecret,
    username: config.username,
    password: config.password,
  })
  r.getSubreddit(subreddit).submitLink({
    title: title,
    url: link,
    sendReplies: true,
  })
}*
```

## *解释道:*

```
*const r = new snoowrap({
  userAgent: 'Whatever',
  clientId: config.clientId,
  clientSecret: config.clientSecret,
  username: config.username,
  password: config.password,
})*
```

*这段代码创建了一个新的连接到 Reddit 服务的`snoowrap`实例。*

```
*r.getSubreddit(subreddit).submitLink({
  title: title,
  url: link,
  sendReplies: true,
})*
```

*`getSubreddit`:生成一个`Subreddit`对象。你可以在这里阅读关于这个物体[的更多信息。](https://not-an-aardvark.github.io/snoowrap/Subreddit.html)*

*`submitLink`:在这个 subreddit 上创建一个新的链接提交，带有提供的标题、链接的 URL 和 snoowrap API 允许的任何其他选项，比如`sendReplies`选项，允许对帖子的回复将回复发送到认证用户的收件箱。*

1.  *提出请求*

*现在添加*

```
*postLink(
  'Post to Reddit with NodeJS and Typescript',
  'https://codybontecou.com/post-to-reddit-with-nodejs-and-typescript.html',
  'webdev'
)*
```

*在`index.ts`底部有你要用的参数。*

*一旦你准备好了，输入`yarn dev`到你的项目终端。如果一切顺利，你应该可以看到你的帖子现在在 Reddit 上了！*

## *奖金*

*通过在一个数组中迭代多个子元素，使其更加动态:*

```
*const url =
  'https://codybontecou.com/post-to-reddit-with-nodejs-and-typescript.html'
const title = 'Post to Reddit using its API'
const subreddits = ['webdev', 'learnjavascript', 'typescript', 'programming']

subreddits.forEach(subreddit => postLink(title, url, subreddit))*
```

*我希望这篇文章对你有帮助，如果你有任何问题、评论或建议，请告诉我*

**更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****