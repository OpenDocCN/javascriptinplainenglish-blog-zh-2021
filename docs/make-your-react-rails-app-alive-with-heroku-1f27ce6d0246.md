# 使用 Heroku 让您的 React/Rails 应用变得生动

> 原文：<https://javascript.plainenglish.io/make-your-react-rails-app-alive-with-heroku-1f27ce6d0246?source=collection_archive---------14----------------------->

![](img/b631812a0e8e00e580692ee1c6ba86e0.png)

Photo by [freestocks](https://unsplash.com/@freestocks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是漫长的一年，我在熨斗营学到了很多。我的最后一个项目是一个具有 React 前端和 Rails 后端的应用程序。一旦我通过了最后的评估，我只有一个问题要问我的导师——“我如何让它变得生动？”他建议使用 Heroku，所以我认为这将是一个有趣的话题。

有 3 个先决条件:

1.  您应该在 Rails 后端使用 **PostgreSQL** 数据库。
2.  **app 的前端**和后端**应该有自己的 git **库**。**
3.  使用 **Yarn** 作为你的 Node.js 包管理器。

现在您需要更新代码并为部署做准备。先说后端。你需要更新 **cors.rb** 文件。在我们的开发版本中，我们允许来自本地应用程序的请求。

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'http://localhost:3000/' resource '*',
      headers: :any, methods: [:get, :post, :put, :patch, :delete]
  end
end
```

现在，我们需要指向我们新的实时应用程序。我们的 live 应用程序名称将为“ **fixer-tube** ”，因此 Heroku URL 将为“https://fixer-tube . Heroku app . com”。因此，让我们将代码修改如下。

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'https://fixer-tube.herokuapp.com' resource '*',
      headers: :any, methods: [:get, :post, :put, :patch, :delete]
  end
end
```

在前端，我们也需要一些更新。在您的前端根目录中，让我们创建一个 **static.json** 并添加以下代码

```
{ "root": "build/", "routes": { "/**": "index.html" } }
```

由于我们的后端现在将在线托管，我们将需要更新我们的获取请求。我们加载数据的开发代码如下所示:

```
export const loadData = () => {
    return (dispatch) => {
        fetch('http://localhost:3001/main_categories')
        .then(resp => resp.json())
        .then(data => dispatch({type: LOAD_DATA, payload: data}))
    }
};
```

现在，我们需要为我们的后端 API 取一个名字，让我们称之为 **fixer-tube-API** ，因此我在 Heroku 上的 APIs URL 将是——'https://fixer-tube-api.herokuapp.com/main_categories'。

```
export const loadData = () => {
    return (dispatch) => {
        fetch('https://fixer-tube-api.herokuapp.com/main_categories')
        .then(resp => resp.json())
        .then(data => dispatch({type: LOAD_DATA, payload: data}))
    }
};
```

文件更新已经完成，请确保将所有更改都推送到 Github。

在 Heroku 网站上注册。

根据您的操作系统，使用此处的说明安装 Heroku CLI。

现在，我们将首先从后端开始实际部署。

1.  导航到后端应用程序目录并登录 heroku `heroku login`。
2.  创建 Heroku 项目— `heroku create fixer-tube-api`
3.  初始化 Heroku git 仓库— `git remote add heroku git@heroku.com:fixer-tube-api.git`
4.  向存储库添加文件`git add .`
5.  提交文件`git commit -m "1st heroku commit"`
6.  并按下`git push heroku master`
7.  是时候迁移数据库了`heroku run rake db:migrate`
8.  如果您想在 seeds.rd `heroku run rake db:seed`中查看一些数据

我们的后端已经完成，我们可以在这里查看—[https://fixer-tube-api.herokuapp.com/main_categories.](https://fixer-tube-api.herokuapp.com/main_categories.)

现在，让我们部署前端。

1.  导航到我们的前端文件夹
2.  创建 Heroku 应用程序集以创建-反应-应用程序-构建`heroku create fixer-tube --buildpack [https://github.com/mars/create-react-app-buildpack.git](https://github.com/mars/create-react-app-buildpack.git)`
3.  初始化 Heroku 遥控器`git remote add heroku git@heroku.com:fixer-tube.`
4.  向资源库添加文件`git add .`
5.  提交文件`git commit -m "heroku app created"`
6.  并按下`git push heroku master`
7.  现在让我们看看它是否能与`heroku open`一起工作

如果一切正常，您将被重定向到[https://fixer-tube.herokuapp.com/.](https://fixer-tube.herokuapp.com/.)

现在，您的项目在线直播，而不仅仅是在您的计算机上！

你可以在关于[“React 中的前端表单验证”](https://nicksolonyy.medium.com/front-end-form-validation-in-react-33595dec8d6f?sk=b6a12799b8a6076aa51715f92f6088e9)的帖子中阅读更多关于我在这个项目中的发现，查看 [GitHub](https://github.com/nicksolony/fixer-tube) 并观看下面的快速演示。

Fixer-Tube Demo

*请在以下社交网络上查看我，我很乐意收到您的来信！——*[*LinkedIn*](https://www.linkedin.com/in/nick-solonyy/)*，* [*GitHub*](https://github.com/nicksolony) ， [*脸书*](https://www.facebook.com/nick.solony) *。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)