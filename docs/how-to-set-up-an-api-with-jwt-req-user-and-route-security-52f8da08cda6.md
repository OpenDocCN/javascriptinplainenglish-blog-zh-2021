# 如何设置一个与 JWT 的 API，请求。用户和路由安全性

> 原文：<https://javascript.plainenglish.io/how-to-set-up-an-api-with-jwt-req-user-and-route-security-52f8da08cda6?source=collection_archive---------3----------------------->

![](img/49899f86931266ca9305310abe7903c5.png)

Photo by [Anthony Riera](https://unsplash.com/@frenchriera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

阅读完本文后，您将理解如何在 Node.js/TypeScript 中创建一个 API，其函数如下:

*   在调用`/login`时，生成并返回一个承载/JWT 给用户
*   使用中间件解码认证报头(承载/JWT)
*   修改 Express 名称空间以添加对`req.User`的支持
*   增加路线的安全性(例如，“只有`Admin`可以访问这条路线”)

***PS:最后有一个工作 git 的链接。***

# 基本快速设置

对于已经被记录了一千次的东西，很少有令人兴奋的事情，但我们需要度过这一部分:

```
import Express from 'express';
import http from 'http';
import cors from 'cors';const PORT = process.env.PORT !== undefined ? parseInt(process.env.PORT) : 3001;let app: Express.Application | undefined = undefined;app = Express();app.use(cors({ exposedHeaders: 'Authorization' }));
app.use(Express.urlencoded({ extended: true }));
app.use(Express.json());**// -----> MORE CODE WILL BE ADDED HERE! <--------**http.createServer(app).listen(PORT, () => console.log(`Webserver running at [http://localhost:${PORT}/`](http://localhost:${PORT}/`)));
```

按照显示的顺序在上面显示的行中添加所有路线。将剩余的代码添加到其他地方。一些项目应该在它们自己的文件中。

# 解码 JWT

在路由的早期，应该找到解码报头的功能。如果存在真正的匿名路由(比如`/robots.txt`，那么这个函数应该在那之后出现)。

```
app.use(function JWTDecoderMiddleware(req: Express.Request, res: Express.Response, next: Express.NextFunction) { const authorization = req.headers.authorization;
  if (authorization && authorization.startsWith("Bearer ")) {
     const u = DecodeJWT(authorization.substring(7));
     if (u)
        req.User = u;
     else
        console.log("jwt found, but it was not valid.");
  }next();
    });
```

这个函数依赖于两个因素:正在修改的全局名称空间使`req.User`可用，以及`DecodeJWT`-函数(见下文)

## “用户”、“承载者”和“访问级别”类型

在继续之前，需要几个类型。在 API 端，我们将有某种类型的用户登录，并且需要处理其类型/接口。

下一个，来人。它将被发送到*客户端*并由客户端存储(以加密的 JWT 格式)。基本上，任何不敏感的东西都可以存储在 JWT 中，只要注意用户可以*轻松*解密 JWT(但是**他们不能修改它**)。在 https://jwt.io/[检查 JWT](https://jwt.io/)。

**types ts**

```
export type User = {
    ID: string,
    Name: string,
    AccessLevel: AccessLevel, /** Never ever store an clear-text pw like this! */
    Password: string
} export type Bearer = {
    Name: string,
    ID: string,
    AccessLevel: AccessLevel
}export type AccessLevel = "Admin" | "User" | "Anonymous";
```

❕ **以安全的方式存储用户凭证，不要像这个演示一样使用明文密码。**

**global.d.ts**

注意`global.d.ts`的命名。在[https://JavaScript . plain English . io/typescript-and-global-variables-in-node-js-59 C4 BF 40 CB 31](/typescript-and-global-variables-in-node-js-59c4bf40cb31)中阅读有关全局变量的更多信息

在添加`Express.User`的同时，我们添加了我们打算使用的环境变量的类型:

```
import { User } from './types';declare global { **namespace Express {
        interface Request {
            User: User
        }
    }** namespace NodeJS {
        interface ProcessEnv {
          JWTENCRYPTIONKEY: string;
          NODE_ENV: 'development' | 'production';
          PORT: string;  // All environment variables are strings
       }
    }
}export { };
```

❕确保你要么使用`.env`要么设置环境变量。

## DecodeJWT 函数

为了验证 JWT 没有被篡改，API 必须定义一个密钥。基本上解码为:

```
import * as jsonwebtoken from "jsonwebtoken";export function Decode<T extends object>(iJWT: string): T | undefined {
    try {
        return jsonwebtoken.verify(iJWT,
                process.env.JWTENCRYPTIONKEY) as T;
    } catch (e) {
        return undefined;
    }
}export function DecodeJWT(jwt: string): User | undefined { const decoded = Decode<**Bearer**>(jwt);
    if (decoded)
        return Users.find(u => u.ID === decoded.ID);
}
```

## 用户？

我们需要一些用户。

```
const Users: User[] = [
   { ID: "root", Name: "root", AccessLevel: "Admin", Password: "Banana1" },
   { ID: "foo", Name: "Foo", AccessLevel: "User", Password: "Bar" }
];
```

❕ **以安全的方式存储用户的凭证，不要像在这个演示中那样使用明文密码。**

# 路线/

让我们添加一些路线，从`/`开始。

```
app.get('/', function (req: Express.Request, res: Express.Response){
     res.status(200).json({
         "Foo": "Bar",
         "Time": new Date().toISOString()
     });
 });
```

# 路由/登录

这条路线将采用`{ "username": "Foo", "password" : "Bar" }`并试图找到一个匹配凭证的用户。如果找到，则生成一个 JWT 并发送给被调用方。

```
app.post('/login', function (req: Express.Request, res: Express.Response) { console.log(`U=${req.body.username}, Pwd=<hidden>`); const jwt = Login(req.body);
    if (jwt) {
      res.append('Authorization', jwt);
      res.status(200).json({ Success: true, JWT: jwt });
    }
    else
       res.status(200).json({ Success: false });});
```

## 注册

```
export function Login(arg: { username: string, password: string }): string | undefined { const user = Users.find(u => u.Name === arg.username 
     && u.Password === arg.password);
    if (user) { const result: Bearer = {
            ID: user.ID,
            Name: user.Name,
            AccessLevel: user.AccessLevel
        }; return Encode(result); }
}
```

## 编码功能

```
export function Encode<T extends object>(iPayLoad: T, iTimeoutSeconds = 3600 * 10): string {
    return jsonwebtoken.sign(
                     iPayLoad, 
                     process.env.JWTENCRYPTIONKEY, 
                     { expiresIn: iTimeoutSeconds }
                   );
}
```

# 到目前为止，一切顺利。

至此，我们已经实现了一个正在运行的 web 服务器，它公开了`/`、`/login`，可以解码任何有效的 JWT，并通过它返回一个用户。

现在事情变得有点复杂了。:)

# HasAccessLevel —作为函数实现

检查访问级别可以通过函数或中间件来完成。

## /me —具有检查访问级别的功能

```
app.get('/me', function (req: Express.Request, res: Express.Response) { ** if (!HasAccessLevel(req, res, ["User", "Admin"])) 
      return;  // Response has already been sent** res.status(200).json({ "UserName": req.User.Name });});
```

## HasAccessLevel 函数

AccessLevel 是一个类型，定义为`type AccessLevel = "Admin" | "User" | "Anonymous`。

```
function HasAccessLevel(req: Express.Request, res: Express.Response, iReqLevel: AccessLevel[] = []): boolean { let result = false;
    if (req.User)  // Has the middleware decoded the jwt properly?
        // Yes, does the user match?
        result = iReqLevel.includes(req.User.AccessLevel);
    else
       // No, but maybe "Anonymous" can access this function?
       result = iReqLevel.includes("Anonymous"); // Not allowed to access? Send 401!
     if (!result) {
        res.status(401).json(
                { Success: false, Error: "Access denied" });
        res.end();
    } return result;
}
```

# HasAccessLevelMiddleware —作为中间件实现

## /我—使用中间件

中间件必须有三个参数，但是使用下面的语法可以很容易地避免这一点:

```
app.get('/me2',
       **(rq, rs, n) => HasAccessLevelMiddleware(rq, rs, n, ["User", "Admin"]),** 
   (req: Express.Request, res: Express.Response) => { // Will only get here if HasAccessLevelMiddleware allows it
    res.status(200).json({ "UserName": req.User.Name });});
```

## HasAccessLevelMiddleware

中间件决定是否调用`next()`。

```
export function HasAccessLevelMiddleware(req: Express.Request, res: Express.Response, next: Express.NextFunction, iReqLevel: AccessLevel[] = []): void { let hasAccess = false;
    if (req.User)  // Has the middleware decoded the jwt properly?
       hasAccess = iReqLevel.includes(req.User.AccessLevel);
    else
       hasAccess = iReqLevel.includes("Anonymous"); **if (hasAccess)
       next();   // Continue executing**
    else {
       res.status(401).json({ Success: false, Error: "Denied" });
       res.end();
    }
}
```

# 错误处理程序

最后，添加错误处理程序。错误处理程序有四个参数，其中第一个是`err`。要让 TypeScript 大放异彩，最好将 err 定义为`Error & { status: number, message: string }`。`Error`是内置的错误对象，Express 增加了`status`和`message`。

```
app.use(function (**err: Error & { status: number, message: string }**, req: Express.Request, res: Express.Response, next: Express.NextFunction) {console.error(err.status);
  console.error(err.message);
  console.error(err.stack);
  res.status(500).json({ Error: "Internal error" });
  res.end();});
```

# 卷曲

这些命令是在 Windows 上编写的，进行必要的调整以在其他平台上运行:

```
# Login as user "Foo"curl -X POST -H "Content-Type: application/json" -d "{\"username\":\"Foo\",\"password\":\"Bar\"}" http://localhost:3001/login# Grab token from body or headers and do:set TOKEN=eyJhbGciOiJIUzI1NiIsIn.....# Use the tokencurl -H "Authorization: Bearer %TOKEN%" http://localhost:3001/me
```

# Git 回购

按下 VSCode 中的`F5`(或`nodemon`，或运行`node`)即可运行回购。阅读更多关于 https://github.com/tomnil/expressplate 的信息

# 享受:)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)