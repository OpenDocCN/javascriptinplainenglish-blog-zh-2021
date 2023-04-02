# remix——最热门的新 JavaScript 框架(2021 年冬季)

> 原文：<https://javascript.plainenglish.io/remix-the-hottest-new-js-framework-winter-2021-4bee22a0761d?source=collection_archive---------0----------------------->

## Remix 是一个类似于 Next.js 或者 Gatsby 的全栈 JavaScript 框架。

![](img/e135b0611bcdc4dc8bab2837cb2f9ca3.png)

如果你像我一样，新的 JavaScript 框架不会让你兴奋。似乎每周都会发布一个新的 JavaScript 框架，发布时大肆宣传，到了月底，每个人都进入了 JavaScript 领域的“下一个大事件”。

因此，我很自然地回顾了去年 Remix 的最初版本，当时创始人(也是 React 路由器的创造者)宣布了一种基于许可的模式，个人开发者许可费用为 **$250** 。

> Remix 是一个全栈 web 框架，让你专注于用户界面，并通过 web 基础工作，提供一个快速，灵活，有弹性的用户体验。

不，谢谢你。我会坚持我的观点，用反应和表达。

最近，Remix 的创始人带来了 Kent C. Dodds 并宣布他们将开源！潜水不再需要执照。好吧，那我们打球吧。

下面的文章将总结开发者博客教程的要点，并插入一些我个人的想法。

# 什么是混音？

Remix 是一个类似于 Next.js 或者 Gatsby 的全栈 JavaScript 框架。如他们的[登陆页面](https://remix.run)所述:

> Remix 是一个无缝的服务器和浏览器运行时，通过利用分布式系统和原生浏览器功能而不是笨重的静态构建，提供快速的页面加载和即时转换。

# Remix 开发者博客教程

马上，我遇到了一个错误，因为我使用了一个旧版本的 Node(必须≥ v14.0.0)。在升级了我的 local node.js 包之后，我们使用`npx` 创建了一个新的 Remix 项目，类似于“create-react-app ”,但是有相当多的内置选项/支持。我将使用默认的带有 TypeScript 的 Remix 应用服务器。

## **路由**

混音应用程序的文件结构包括一个“路线”文件夹，您可以在其中为每条路线创建文件夹。例如，localhost:3000/posts 呈现了`my-app/routes/posts/index.tsx`文件中的任何内容。这在某些方面类似于 HTML 和 PHP 开发的老方法。这将是一个反复出现的主题。

## **数据加载**

Remix 使用“加载器”的概念来获取 React 组件要使用的数据。

> 加载器是组件的后端“API ”,它已经通过`useLoaderData`为你连接好了。在混合路线中，客户机和服务器之间的界限是多么模糊，这有点令人难以置信。

`useLoaderData` 允许我们用从`loader`函数返回的数据合成 react 组件。我们所需要的就是创建一个名为`loader`的函数，并在该函数中执行数据库查询，然后返回一个数据数组。

帖子路径的`index.tsx`可以是这样的:

```
import { Link, useLoaderData } from "remix";
import { getPosts } from "~/post";
import type { Post } from "~/post";export let loader = () => {
  return getPosts();
};export default function Posts() {
  let posts = useLoaderData<Post[]>();
  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {posts.map(post => (
          <li key={post.slug}>
            <Link to={post.slug}>{post.title}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

`useLoaderData`函数自动找到加载器函数并将数据交给 react 组件！如果你问我，我觉得很好。我唯一的不满是这一切的含蓄。我更喜欢非常显式可读的代码，如果你不知道`useLoaderData`需要一个名为`loader`的函数，代码会变得混乱。

## **动态路由和嵌套路由**

我们可以通过创建一个以`$`开头的文件来创建带参数的动态路由，例如:`my-app/routes/posts/$slug.tsx`将负责类似`localhost:3000/posts/this-is-a-slug`的路由。我们用文件名中放在`$`后面的东西来命名参数，所以在这个例子中，参数名是`slug`。默认情况下，该路径的加载器函数接受一个对象，其中一个值是 params，因此我们可以有一个类似如下的文件`my-app/routes/posts/$slug.tsx`:

```
import { useLoaderData } from "remix";export let loader = async ({ params }) => {
  return params.slug;
};export default function PostSlug() {
  let slug = useLoaderData();
  return (
    <div>
      <h1>Some Post: {slug}</h1>
    </div>
  );
}
```

嵌套路由有点棘手，但本质上，你的主路由文件，比如说:`my-app/routes/admin.tsx`可以使用 remix 所称的`Outlet`，它允许呈现该路由文件夹的索引文件。所以`my-app/routes/admin.tsx`可以使用一个`Outlet`来呈现`my-app/routes/admin/index.tsx`和管理文件夹中的任何其他嵌套文件，比如包含一个表单的`new.tsx`来创建一个新帖子。一开始这一切都很复杂，老实说，我现在还没完全理解这个概念，所以我敦促你在[混音文档](https://remix.run/docs/en/v1/tutorials/blog#index-routes)或其他教程中自己钻研这个。

## **形式和动作**

> 如果你像我们一样喜欢 HTML，你应该会非常兴奋。如果你一直在做大量的`<form onSubmit>`和`<button onClick>`，你将会被 HTML 弄得神魂颠倒。对于这样的功能，您真正需要的是一个从用户那里获取数据的表单和一个处理数据的后端操作。在混音中，这就是你所要做的。

教程的最后一个主要部分集中在表单和表单提交上，在我看来非常酷。在路由中，`/admin/new`我们可以在 react 组件中呈现一个基本的 HTML 表单。如您所见，没有指定`onSubmit`或`onClick`功能。

```
import { Form } from "remix";

export default function NewPost() {
  return (
    <Form method="post">
      <p>
        <label>
          Post Title: <input type="text" name="title" />
        </label>
      </p>
      <p>
        <label>
          Post Slug: <input type="text" name="slug" />
        </label>
      </p>
      <p>
        <label htmlFor="markdown">Markdown</label>
        <br />
        <textarea rows={20} name="markdown" />
      </p>
      <p>
        <button type="submit">Create Post</button>
      </p>
    </Form>
  );
}
```

我们只需要写一个`action`函数。类似于`loader`的想法，这个函数必须命名为`action`。

```
import { useActionData, Form, redirect } from "remix";
import invariant from "tiny-invariant";export let action: ActionFunction = async ({ request }) => {
  let formData = await request.formData();

  let title = formData.get("title");
  let slug = formData.get("slug");
  let markdown = formData.get("markdown");

  let errors = {};
  if (!title) errors.title = true;
  if (!slug) errors.slug = true;
  if (!markdown) errors.markdown = true;

  if (Object.keys(errors).length) {
    return errors;
  }

  invariant(typeof title === "string");
  invariant(typeof slug === "string");
  invariant(typeof markdown === "string");
  await createPost({ title, slug, markdown });

  return redirect("/admin");
};

export default function NewPost() { 
let errors = useActionData();
return (
    <Form method="post">
      <p>
        <label>
          Post Title: <input type="text" name="title" />
        </label>
      </p>
      <p>
        <label>
          Post Slug: <input type="text" name="slug" />
        </label>
      </p>
      <p>
        <label htmlFor="markdown">Markdown</label>
        <br />
        <textarea rows={20} name="markdown" />
      </p>
      <p>
        <button type="submit">Create Post</button>
      </p>
    </Form>
  );
}
```

action 函数将负责表单提交，并处理数据库中的脏活，如果出错，将返回错误或重定向回`/admin`(来自`/admin/new`)。这个神奇的`action`函数会自动被调用，并有效地作为一个附加的后端 API 用于任何数据突变或表单提交。

现在你知道了。以上是我对新的全栈 JavaScript 框架 **Remix 的要点总结。从这篇文章发表到现在已经将近一个星期了，所以和往常一样，事情会有变化。我喜欢学习这个新的框架，但我不认为这会很快爬上梯子并拿下 Next.js。**

这种类型的框架适用于包含大量页面的 web 应用程序和数据密集型应用程序，这些应用程序包含不同的数据，具体取决于特定的路径。我认为随着 Remix 的发展，它将适合更多的用例。

感谢你花时间阅读这篇文章。在不久的将来，我将开始做更多的软件工程和更具体的全栈 web 开发帖子，所以请继续关注我在 Medium 上的帐户，以确保您看到我的帖子。请评论您可能有的任何问题或顾虑，因为我将 100%回复所有评论！

如果你喜欢这篇文章并且不是 Medium.com 的会员，请考虑加入我的链接，每月只需 5 美元。你帮我赚几个钱，就可以获得无限的媒体文章:[*https://medium.com/@jameschnebly/membership*](https://medium.com/@jameschnebly/membership)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**