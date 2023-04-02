# 如何设置对 Ruby on Rails 项目的反应第 1 部分-设置

> 原文：<https://javascript.plainenglish.io/how-to-set-up-react-js-with-a-ruby-on-rails-project-dd8558fea7e?source=collection_archive---------9----------------------->

![](img/cca83361a40223242ca54ebdf8ece9fb.png)

Ruby on Rails 是一个非常好的工作框架。但是，使用嵌入式 Ruby()。erb)和 ajax 来构建具有动态前端的应用程序可能很痛苦。

这就是像 reactor、Angular 和 Ember 这样的前端框架的发挥作用的地方。由于反应是现在最热门的话题，我们将使用它。

但是，您如何在 Ruby on Rails 应用程序中设置反应呢？这就是我在本文中要讨论的内容

您需要做的第一件事是创建您的 Ruby on Rails 应用程序，并告诉它您将使用 reactor。为此，请键入以下代码:

```
rails new react-rails --database=postgresql --webpack=react
```

在这个应用程序中，我还使用 Postgres 作为数据库。

现在我们已经建立了这个项目，我们需要添加一些代码，这样我们的应用程序就知道如何使用 React 作为前端。

让我们转到 config/routes.rb 的路由文件。

你要在这里做一些和你的路线有点不同的事情。您将把对后端的所有调用包装在一个 API 名称空间中。

在这个项目中，我们将有一个帖子模型。所以你应该这样写你的路线:

```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html

  root 'pages#index'

  namespace :api do
    namespace :v1 do
      resources :posts
    end
  end
```

我还添加了一个到我们的页面控制器的根路由。当你进行后端调用来访问你的控制器时，你会有像“/API/v1/post”这样的路径来获取你的帖子。

现在，我们需要告诉我们的应用程序将其他路线发送到我们的主反应应用程序。我们将把它添加到我们的路由文件的底部:

```
get '*path', to: 'pages#index', via: :all
```

您的文件路由文件应该如下所示:

```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html

  root 'pages#index'

  namespace :api do
    namespace :v1 do
      resources :posts
    end
  end

  get '*path', to: 'pages#index', via: :all
```

让我们设置我们的 index.jsx 文件。

转到 app/JavaScript/packs/hello _ reactor . jsx，并将该文件的名称重命名为 index.jsx。删除那里的大部分内容，并使该文件看起来像这样。

```
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router, Route } from 'react-router-dom'
import App from '../src/components/App'

document.addEventListener('DOMContentLoaded', () => {
  ReactDOM.render(
    <Router>
      <Route path="/" component={App}/>
    </Router>,
    document.body.appendChild(document.createElement('div')),
  )})
```

如果您以前使用过“反应”，这应该很熟悉。我们正在导入 React、ReactDom 和 React rowitdom。然后，我们导入我们的主应用程序。然后，我们在 DOM 中创建一个节点，并插入我们的应用程序。

在我们遗忘之前，让我们用纱线添加反应路由器。转到您的终端并键入:

```
yarn add react-router-dom
```

我们几乎可以在前端看到我们的应用程序。让我们去设置我们的 App.js 文件。

创建文件“app/JavaScript/src/components/app . js”。我们将得到根路径来显示我们的帖子。在“常规的 rails 应用程序”中，这将是我们帖子视图文件夹中的索引页面。

无论如何，App.js 文件应该是这样的:

```
import React from 'react'
import { Route, Switch } from 'react-router-dom'
import Posts from '../components/Posts/Posts'

const App = () => {
  return (
    <Switch>
      <Route exact path="/" component={Posts} />
    </Switch>>
  )
}export default App
```

让我们在“app/JavaScript/src/componeets/Posts/Posts . js”中创建这个帖子页面。这是我的样子。

```
import React from 'react'

const Posts = () => {
  return (
    <div>
      <h1>Posts</h1>
      <p>This is our posts page.</p>
    </div>
  )
}export default Posts
```

现在，我们需要告诉我们的视图渲染我们的反应应用程序。转到“app/view/layout/application . html . erb”并添加以下标签:

```
<%= javascript_pack_tag 'index' %>
```

布局文件应如下所示:

```
<!DOCTYPE html>
<html>
  <head>
    <title>ReactRails</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'index' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

在这里，我正要启动我的服务器，但是我遇到了一个“active record::connection setsed”没有提供密码的错误，因为我没有在“config.database.yml”中设置数据库密码，所以请确保设置了您的数据库设置。

我还必须运行 rails db:create 来创建我的数据库

用 Rails 设置 Postgresql 不在本教程的范围内，抱歉！

再走一步！我们必须设置我们的页面控制器及其视图。

去“app/controllers/pages _ controller”里创建一个 PagesController。我们只需要一个指数行动。

```
class PagesController < ApplicationController
  def index

  endend
```

以及你在“app/views/pages/index.html.erb”中的视图文件。我的文件是一个空白文件，因为我们只是加载布局。

现在运行“rails s ”,您应该会看到以下内容:

![](img/7c7d920207cc66dbd148e13901810341.png)

现在我们已经在 Rails 应用程序上设置了 React。恭喜你，这是一大步！

继续关注连接前端和后端以及添加 Redux。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)