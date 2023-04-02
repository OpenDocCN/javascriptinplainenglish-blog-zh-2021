# Next.js —在 getServerSideProps 中处理 Cookies

> 原文：<https://javascript.plainenglish.io/next-js-using-cookies-in-getserversideprops-89c03a216b0b?source=collection_archive---------1----------------------->

![](img/54f13e83cb31e66ab742be92c2e50203.png)

当我冒险在 Next.js 中构建一个认证工作流时，我发现自己在努力处理 **getServerSideProps 中的 cookies。**

# 问题是

在呈现页面之前，我想在服务器上获取我的用户数据，这意味着我首先需要验证访问令牌，该令牌在浏览器 cookie 中加密。我希望能够在呈现页面之前更新、删除和设置多个新的 cookies。

因为我需要重用验证用户令牌的功能，所以我需要能够在 getServerSideProps 函数范围之外的指定函数中处理 cookies。例如，从 getServerSideProps 内部向我的 API 发出请求。**这就是事情变得棘手的地方。**

在尝试这些 cookie 操作时，我很快意识到:

> 无论您是从 getServerSideProps 还是普通的 API 端点调用 cookie 处理函数，这都很重要。

我发现当通过 Postman 测试我的验证端点时，cookies 设置得很好。但是当我从getServerSideProps 加载页面时，它们并没有在浏览器中设置

为什么会这样呢？

您不像调用 API 路由那样从浏览器调用 getServerSideProps **，因此您不能使用相同的方法在浏览器中设置 cookies。我们必须使用 Next.js 的 [**上下文对象**](https://nextjs.org/docs/api-reference/data-fetching/getInitialProps#context-object) 而不是节点的请求对象。我们将在图书馆的帮助下完成这项工作。但是这些库不会为我们提供一个集成的方法来将 cookies 从函数传递到 getServerSideProps**

在我们进入服务器渲染之前，让我解释一下我是如何在一个普通的 API 请求中处理 cookies 的。

# 从客户端读取/写入 cookies

我决定模仿 Express 的 cookie 处理，并在我的响应对象上添加一个 res.cookie 函数。这样做的原因是，当在 vanilla Node.js 中工作时，我们必须通过以下方式设置 cookies:

```
res.setHeader(“set-cookie”, value)
```

正如[文件所述](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie):

> 要发送多个 cookies，应该在同一个响应中发送多个`**Set-Cookie**`头。

换句话说，您不能多次调用 res.setHeader 并期望最终的头包含您的所有 cookies。它只会将标头设置为您传递的最后一个值。

你要做的是将一个**序列化 cookie**的**数组**传递给头文件**。**

## 这是蓝图:

我希望有一个简单的、类似 express 的 **res.cookie** 函数，它将 cookie 添加到一个数组中，然后能够调用函数 **res.sendCookies** ，将 cookie 的数组实际写入标头。

## 使用包装

我们可以通过在包装器中导出函数，向本地 req 和 res 对象添加任何我们想要的函数。这是我们使用 res.cookie 的方式。

下面是使用包装器后的无服务器功能:

```
import wrapper from 'utils/wrapper';const handler = async (req, res, next) => {
    // code and such
};export default wrapper(handler);
```

这是包装纸里面的一瞥:

```
 import cookie from ‘utils/cookies’; const wrapper = handler => { return (req, res, next) => { res.cookieArray = []; res.cookie = (name, value, options) => {
         cookie(res, name, value, options);
       }; res.sendCookies = () => {
         res.setHeader('set-cookie', res.cookieArray);
       }; return handler(req, res, next); };
  };
```

## res.cookie()

这个函数根据**值**参数是否为空来设置或删除一个 cookie，方法是将它序列化并推送到我们的 res.cookieArray

```
import { serialize } from ‘cookie’;const cookie = (res, name, value, options) => {
  if (!options) options = {};
  options.path = ‘/’;
  const stringValue = (typeof value === ‘object’)
      ? ‘j:’ + JSON.stringify(value) 
      : String(value)if (‘maxAge’ in options) {
    options.expires = new Date(Date.now() + options.maxAge);
    options.maxAge /= 1000;
  };
  if (!value) {
    options.expires = new Date(Date.now() — 1000);
  };**// if we pass a value, it sets the cookie
**  if (value) {
    res.cookieArray.push(**serialize**(name, String(stringValue), options))**// if we do not pass an empty string as a value, it deletes the cookie
**  } else {
    res.cookieArray.push(**serialize**(name, ‘’, options))
  };}export default cookie;
```

有了这段代码，当您直接从浏览器或 Postman 调用 API 时，您应该能够处理写入和删除 cookies。

现在，在 getServerSideProps 中处理 cookies。

# *从服务器读取*cookie

这相当简单。依靠解析 Next.js 的上下文对象的外部库就足够了，而不是自己尝试。我使用 [next-cookies](https://www.npmjs.com/package/next-cookies) to **获取服务器上的** cookies:

```
import cookies from ‘next-cookies’;const c = cookies(context);const myAuthenticationCookie = c.authenticationToken;
```

现在是更棘手的部分:

# 从服务器写入 cookies

我们已经通过添加一个 **res.cookiess** 方法和一个 **res.cookieArray** 方法，为如何在控制器函数和 API 端点中处理 cookie 打下了基础。

从一开始就考虑我的情况。我从 getServerSideProps 向我的 API **上的一个端点发出一个获取请求。当它返回一个响应时，我将无法访问一直用来累积 cookies 的 res 对象。所以我只需要在我的回复中返回 cookieArray。**

```
return res.json({
  otherData: data,
  cookieArray: res.cookieArray
});
```

然后，在 getServerSideProps 中，我需要解析这个 cookieArray 并将每个 cookie 写到**上下文**对象上。我创建了一个像这样调用的函数:

```
parseCookies(res.data.cookieArray, context);
```

注意**上下文**是 Node.js 的原生对象，从这里开始:

```
export async function getServerSideProps(**context**) {};
```

最后，这里是我的 parseCookies 函数。为了完成向上下文对象写入的繁重工作，我依赖于 [next-cookie](https://www.npmjs.com/package/next-cookie) (与**next-cookie**相反)。

```
import { useCookie } from 'next-cookie';function parseCookies(array, context) {
  const cookie = useCookie(context);
    for (let string of array) {
      const arr = string.split(';') const options = {};
      const key = arr[0].split('=')[0];
      const value = arr[0].split('=')[1]; arr.shift();
      for (let option of arr) {
        let key = option.split('=')[0].slice(1);
        let value = option.split('=')[1]; if (key === 'Path') key='path'
        else if (key === 'Expires') key='expires'
        else if (key === 'HttpOnly') key='httpOnly', value=true;
        options[key] = value;
      }; if (value !== '') cookie.set(key, value, options)
    else cookie.remove(key);
  };
};export default parseCookies;
```

本质上，这将解析我传递给 cookieArray 的序列化 cookie 字符串，并使用从 next-cookie 导入的函数设置或删除每个字符串。

# 改进您的 Next.js 无服务器框架

我正在努力充分利用 Next.js 的 API，并使用一个类似 Express 的框架，这样我就可以将后端逻辑留给控制器，而不是将所有东西都塞进 Next.js 的无服务器函数中。如果你想达到类似的结果，看看我的文章[在 Next.js 中创建一个类似 Express 的框架](https://blog.usejournal.com/express-like-framework-in-next-js-27a884a0264d)