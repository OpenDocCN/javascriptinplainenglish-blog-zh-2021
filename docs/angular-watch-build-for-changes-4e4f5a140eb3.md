# 角度:观察造型变化

> 原文：<https://javascript.plainenglish.io/angular-watch-build-for-changes-4e4f5a140eb3?source=collection_archive---------2----------------------->

## ***Angular CLI 提供的脚本中，*serve*脚本用于在开发环境中运行和测试应用。以及用于打包和部署的“构建”脚本。然而，也有在开发人员的机器上使用构建输出并观察变更的用例。探索场景！***

## **使用*构建-观察*脚本**

当开发人员对代码进行修改时，您可以使用 Angular build 上的 watch 选项来更新输出。它与 serve 非常相似，只是应用程序运行的 web 服务器不同于默认的 dev 服务器。

![](img/d813f3db43fefcdaf972d65f66a63f40.png)

# 背景

我们大多数人都会使用 Angular CLI 提供的 *ng serve* 命令。默认情况下，它在 *npm 启动*时运行。该命令构建并运行代码。注意 angular.json 文件中的以下配置，它使用@angular-devkit 的 build-angular 包并部署在一个开发服务器上。它在内部使用 Webpack。该设置用于在开发人员的机器上进行开发。

```
"serve": {
 **"builder": "**[**@angular**](http://twitter.com/angular)**-devkit/build-angular:dev-server",** "configurations": {
        "production": {
        "browserTarget": "memy:build:production"
    }, "development": {
        "browserTarget": "memy:build:development"
    }
  },
"defaultConfiguration": "development"
}
```

然而，当您构建和部署代码时，您使用 *ng build* 命令，该命令将应用程序打包到 */dist/application-name* 目录中的几个文件中。这适用于运输到诸如暂存或生产环境中。

# 在开发设置中使用生成输出

如前所述，默认选项在 Webpack 上部署代码。当您对代码进行修改时，它会被动态编译。您可以立即看到变化，验证和测试它们。如果您需要将代码部署在另一个 web 服务器上，该怎么办？比如安装在开发人员机器上的 Http-Server 或 Nginx。

考虑以下解决方案。使用构建命令上的 *- watch* 选项。请参见下面的片段。

```
"watch": "ng build **--watch** --configuration development",
```

当您对文件进行更改时，手表会重新编译并重新生成代码。使用最新代码更新 *dist/application-name* 目录。

> **注** : *使用* -配置*选项执行开发或生产构建。它们有什么不同？在一个示例中，开发配置使用与生产*不同的环境配置文件(environment.ts 或 environment.prod.ts)

# 为什么要在单独的 web 服务器上构建和部署

在一个示例用例中，想象创建一个可安装的渐进式 web 应用程序(PWA)。服务人员(在撰写本文时)不使用 Angular CLI 的 serve 命令。详见 GitHub [第 9869 期](https://github.com/angular/angular-cli/issues/9869)。因此，要验证和测试 progressive web 应用程序，需要使用 watch 脚本构建代码。

```
npm run watch
# (or)
# yarn watch
```

它在 *dist/application-name* 目录中创建构建输出(默认情况下，除非您在 Angular.json 中编辑)。

接下来，在 *dist* 目录下运行 Http-Server

```
http-server dist/application-name
# use npx if http-server is installed globally, at the machine level
# npx http-server dist/application-name
```

当您对应用程序进行更改时，监视脚本会重新构建应用程序。输出将被替换到*区*目录中。重新加载浏览器以查看更改。

渐进式 web 应用程序可以为运行在 Http-Server 上的应用程序注册服务工作者。它还显示桌面或移动设备上的安装按钮。使用 *- watch* 选项，您可以在每次对代码库进行更改时省去手动重建的步骤。

# 参考

*   服务人员入门的角度文档— [链接](https://angular.io/guide/service-worker-getting-started)
*   关于 *ng 构建的角度文档—* [链接](https://angular.io/cli/build)
*   Angular Github 问题—功能请求:ng 与服务人员一起服务— [链接](https://github.com/angular/angular-cli/issues/9869)

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯在这里***](http://newsletter.plainenglish.io/) ***。****