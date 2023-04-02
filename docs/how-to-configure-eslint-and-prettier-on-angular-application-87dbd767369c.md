# 如何在角度应用中配置更小更漂亮

> 原文：<https://javascript.plainenglish.io/how-to-configure-eslint-and-prettier-on-angular-application-87dbd767369c?source=collection_archive---------1----------------------->

![](img/c1990f4cdde93aa211e5967a5a353140.png)

这是“开始一个角度项目”之前要做的事情”系列的最后一篇文章。

我们已经看到了如何充分利用角度配置，以及如何在使用角度工具处理项目之前为自己做好准备。在这最后一部分，我们将讨论如何从 TSLint 迁移到 eslit，如何在 Angular 项目上配置 eslit 和漂亮点，以及如何通过 Husky 实现预提交和预推送林挺和格式化过程的自动化。

我们还在等什么？让我们编码——呃，让我们配置！

## 从 TSLint 迁移到 ESLint

随着 Angular 11 的发布，宣布 TSLint(在 2019 年被弃用)已被 eslit 取代，并且有第三方解决方案允许您通过使用 *schematics* 轻松地从 TSlint 迁移到 eslit。

在运行迁移过程之前，您需要安装**convert-t lint-eslit**schematics。为此，只需在要迁移的角度项目的根中运行以下命令:

```
ng add @angular-eslint/schematics
```

然后，您需要使用以下命令启动迁移过程:

```
ng g @angular-eslint/schematics:convert-tslint-to-eslint your_project_name
```

上述命令将解析*TSLint . JSON*文件，并尝试通过创建一个新的 *.eslintrc.json* 文件来匹配 t lint 规则和 ESLint 规则。该命令还负责删除*t lint . JSON*文件，并删除*t lint*和*共析器*的依赖关系。迁移过程完成后，您的应用程序就可以使用 ESLint 了。

## 配置更小更漂亮

ESLint 的真正力量在于其定制化的可能性。

通过 *.eslintrc.json* 文件，可以使用“共享”配置或设置自定义林挺规则。规则一旦设置，如果代码不遵守规则集，将允许我们显示警告。

在查看我在本文中推荐的配置文件之前，让我们完成漂亮的**安装**，它将负责根据*【漂亮的 文件中设置的规则格式化代码。*

```
npm install prettier eslint-plugin-prettier eslint-config-prettier --save-dev
```

这个命令，除了安装更漂亮，还负责安装两个软件包，禁用一些 ESLint 规则，以避免与更漂亮的冲突。一旦安装完成，我们就可以配置林挺和格式规则了。使用以下配置在项目根内创建*. pretierrc . JSON*文件:

```
{
  "singleQuote": true,
  "trailingComma": "none",
  "endOfLine": "auto"
}
```

如果您想以不同的方式配置更漂亮，请参考[可用选项列表](https://prettier.io/docs/en/options.html)。

一旦完成了更漂亮的配置，现在让我们通过在项目根内创建*. ESLintrc . JSON*文件来配置 eslit，配置如下:

```
{
  "root": true,
  "ignorePatterns": [
    "projects/**/*"
  ],
  "overrides": [
    {
      "files": [
        "*.ts"
      ],
      "parserOptions": {
        "project": [
          "tsconfig.json",
          "e2e/tsconfig.json"
        ],
        "createDefaultProgram": true
      },
      "extends": [
        "eslint:recommended",
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "plugin:prettier/recommended"
      ],
      "rules": {
        "@angular-eslint/component-selector": [
          "error",
          {
            "prefix": "app",
            "style": "kebab-case",
            "type": "element"
          }
        ],
        "@angular-eslint/directive-selector": [
          "error",
          {
            "prefix": "app",
            "style": "camelCase",
            "type": "attribute"
          }
        ],
        "sort-imports": [
          "error",
          {
            "ignoreCase": false,
            "ignoreDeclarationSort": false,
            "ignoreMemberSort": false,
            "memberSyntaxSortOrder": ["none", "all", "multiple", "single"],
            "allowSeparatedGroups": false
          }
        ]
      }
    },
    {
      "files": [
        "*.html"
      ],
      "extends": [
        "plugin:@angular-eslint/template/recommended"
      ],
      "rules": {}
    }
  ]
}
```

我想注意的部分是:**扩展**和**规则**。

由于安装了第三方包，第一个声明了“共享”规则，而后者显示了自定义规则。

我觉得必须添加到列表中的唯一规则是 **sort-imports** ，如果导入的 ES6 模块没有正确排序，就会导致编译时错误。注意插件和规则的声明顺序很重要。这里是 ESLint 配置规则的完整[列表。](https://eslint.org/docs/rules)

最后，如果你想忽略一些文件的林挺，创建*。项目根目录中的 eslintingnore*文件:

```
*package.json
package-lock.json
dist
e2e/**
karma.conf.js
commitlint.config.js*
```

在结束之前，让我们在 *package.json* 中添加脚本，以便从命令行执行林挺和代码格式化:

```
...
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "npx eslint 'src/**/*.{js,jsx,ts,tsx,html,css,scss}' --quiet --fix",
    "format": "npx prettier 'src/**/*.{js,jsx,ts,tsx,html,css,scss}' --write",
    "e2e": "ng e2e"
  }
...
```

瞧啊。我们已经完成了 ESLint 和 Prettier 的安装和配置。

## 配置 Husky

这是本文的最后一部分:在将变更发送到远程存储库之前，我们如何自动化林挺和格式化过程？

简单地说**使用 Husky** ，它通过 Git 挂钩允许您在*预提交*阶段执行命令。

要配置自动*预提交*林挺和格式化过程，您必须首先安装 **lint-staged** :

```
npx mrm@2 lint-staged
```

一旦命令被执行，*。哈斯基*文件夹将在项目根目录下创建。打开这个文件夹你会找到*。预提交*文件。打开文件，编辑如下:

```
*#!/bin/sh*
. "$(dirname "$0")/_/husky.sh"
​
npx lint-staged -c .lintstagedrc.js
```

这样，我们将为 **lint-staged** 指定配置文件，以自动化林挺和格式化过程。此时，剩下的工作就是在项目根目录下创建 *.lintstagedrc.js* 文件:

```
const { ESLint } = **require**('eslint')
​
const **removeIgnoredFiles** = async (files) => {
  const eslint = new ESLint()
  const isIgnored = await Promise.**all**(
    files.**map**((file) => {
      return eslint.**isPathIgnored**(file)
    })
  )
  const filteredFiles = files.**filter**((_, i) => !isIgnored[i])
  return filteredFiles.**join**(' ')
}
​
module.exports = {
  'src/**/*.{js,jsx,ts,tsx,html,css,scss}': async (files) => {
    const filesToLint = await **removeIgnoredFiles**(files)
    return [`npx prettier --write ${filesToLint}`, `npx eslint ${filesToLint}`]
  },
}
```

该文件用于指示 **lint-staged** 忽略*中指定的文件。eslintingnore*。最后，我们已经完成了配置，我们可以测试一切都正常工作。打开终端并运行命令

```
npm run format && npm run lint
```

您将有可能运行格式化和林挺脚本。

此外，如果您的同事在每次提交之前忘记运行这些命令，那么您的盟友 Husky 和 Lint Staged 会立即验证文件的格式和 Lint 是否正确，如果不正确，就会阻止提交。

## 结论

这里是“开始角度项目前要做的事情”系列的最后一部分。在开始任何角度的项目之前，我们已经一起看到和学习了我所采用的工具和实践。

在下一篇文章中，我将讨论一个话题，在过去的几周里，这个话题让我对这个框架以及其他方面有了更多的了解。我们将讨论**领域驱动的设计和前端，以及如何在这个领域使用 DDD 方法的某些方面**。

关注 [**Devmy**](https://devmy.it/) **—软件工厂&学习**关于[媒体](https://medium.com/acadevmy)， [Twitter](https://twitter.com/DevmyFactory) ，[脸书](https://www.facebook.com/Devmy.it/)和 [YouTube](https://www.youtube.com/c/devmy) 联系我们或让您了解前端、移动和 DevOps 开发的最新动态。

## 进一步阅读

[](https://plainenglish.io/blog/create-an-employee-satisfaction-survey-using-angular-and-store-results-in-a-mongodb-collection) [## 使用 Angular 创建员工满意度调查，并将结果存储在 MongoDB 集合中

### 一步一步的教程来建立一个员工满意度调查使用 Angular 和 SurveyJS，一个免费的，开源的…

简明英语. io](https://plainenglish.io/blog/create-an-employee-satisfaction-survey-using-angular-and-store-results-in-a-mongodb-collection) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW)*****。*******

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*