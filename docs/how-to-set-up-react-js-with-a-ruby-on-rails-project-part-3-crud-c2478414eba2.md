# 如何设置 Rails 上的 Ruby 项目第 3 部分——CRUD

> 原文：<https://javascript.plainenglish.io/how-to-set-up-react-js-with-a-ruby-on-rails-project-part-3-crud-c2478414eba2?source=collection_archive---------22----------------------->

![](img/027b6234d18748604473049999dde17f.png)

欢迎来到我的《对 Rails 上的 Ruby 作出反应》(对 Rails 作出反应？，RX3？罗，罗？).今天，我们将在应用程序中添加 CRUD 功能。我们已经在后端安装了它，现在我们只需要连接我们的前端。这应该相对容易。

下面是我们的 API 在“app/javascript/src/api/api.js”中的代码

```
import axios from 'axios'const ROOT_PATH = '/api/v1'
const POSTS_PATH = `${ROOT_PATH}/posts`export const getPosts = () => {
  return axios.get(POSTS_PATH)
}export const getPost = (postId) => {
  return axios.get(`${POSTS_PATH}/${postId}`)
}export const createPost = (postParams) => {
  return axios.post(POSTS_PATH, postParams)
}export const destroyPost = (postId) => {
  return axios.delete(`${POSTS_PATH}/${postId}`)
}export const updatePost = (postId, postParams) => {
  return axios.put(`${POSTS_PATH}/${postId}`, postParams)
}
```

这些是我们将连接到数据库的 CRUD 函数。我认为这些很能说明问题。唯一值得注意的是，使用 createPost()和 updatePost()时，需要确保将参数作为第二个参数传入。

现在，让我们转到我们的类型文件，确保我们的动作创建者和减少者有正确的类型。这在“app/JavaScript/src/types/index . js”中。

```
export const GET_POSTS = "GET_POSTS"
export const GET_POST = "GET_POST"
export const CREATE_POST = "CREATE_POST"
export const DESTROY_POST = "DESTROY_POST"
export const UPDATE_POST = "UPDATE_POST"
```

现在，我们只需要去我们的动作创建器，确保我们向 rails 后端发出请求，同时向我们的 reducers 发送动作类型。该文件为“app/JavaScript/src/actions/post . js”。

```
import * as api from '../api/api'
import { GET_POST, GET_POSTS, CREATE_POST, UPDATE_POST, DESTROY_POST } from '../types/index'export const getPosts = () => async (dispatch) => {
  try { 
    const { data } = await api.getPosts()
    dispatch({
      type: GET_POSTS,
      payload: data.data
    })
  } catch (error) {
    console.log(error)
  }
}export const getPost = (postId) => async (dispatch) => {
  try {
    const { data } = await api.getPost(postId)
    dispatch({
      type: GET_POST,
      payload: data.data
    })
  } catch (error) {
    console.log(error)
  }
}export const createPost = (postParams) => async (dispatch) => {
  try {
    const { data } = await api.createPost(postParams)
    dispatch({
      type: CREATE_POST,
      payload: data.data
    })
  } catch (error) {
    console.log(error)
  }
}export const updatePost = (postId, postParams) => async (dispatch) => {
  try {
    const { data } = await api.updatePost(postId, postParams)
    dispatch({
      type: UPDATE_POST,
      payload: data.data
    })
  } catch (error) {
    console.log(error)
  }}export const destroyPost = (postId) => async (dispatch) => {
  try {
    const { data } = await api.destroyPost(postId)
    dispatch({
      type: DESTROY_POST,
      payload: postId
    })
  } catch (error) {
    console.log(error)
  }
}
```

让我们看看其中一个函数，看看它到底在做什么。让我们看看 createPost()函数。

```
export const createPost = (postParams) => async (dispatch) => {
  try {
    const { data } = await api.createPost(postParams)
    dispatch({
      type: CREATE_POST,
      payload: data.data
    })
  } catch (error) {
    console.log(error)
  }
}
```

在这里，我们创建了一个名为 createPost 的函数，该函数接受 postParams 的参数。然后，我们声明这是一个异步函数，我们想使用 redux-thunk。

接下来，我们开始尝试捕捉块。我们使用我们的 API 对后端进行调用，获取输出并将其放入 const 数据中。

然后，我们告诉所有的缩减器，我们正在创建 CREATE_POST 操作并传递数据，以便缩减器可以使用后端的数据来更新我们的 redux 存储。

最后，我们会记录任何错误。

现在，我们需要用减速器来处理这些动作。让我们从 GET_POST 操作类型开始。这设置了当前的帖子，所以我们需要为它创建一个减肥法。

创建文件“app/JavaScript/src/reduce/post . js”并将其放在那里。

```
import { GET_POST } from '../types/index'export default (post = null, action ) => {
  switch (action.type) {
    case GET_POST:
      return action.payload
    default:
      return post
  }
}
```

我们将初始帖子设置为空，然后我们告诉这个减压器，每当它看到 GET_POST 动作时，获取该有效负载，并将其分配给 redux 存储上的帖子密钥。请确保将此 reducer 添加到您的“app/JavaScript/src/reduce/index . js”文件中。

```
import { combineReducers } from 'redux'
import posts from './posts'
import post from './post'export default combineReducers({
  posts,
  post
})
```

我们将制作一个帖子#show page，但在此之前，我们需要设置我们的路由器。在“app/JavaScript/src/components/app . js”中，我们需要导入我们将要制作的 Page 组件，然后告诉路由器在我们转到/post/id 时呈现该组件。

添加代码后，您的 App.js 应该如下所示:

```
import React from 'react'
import { Route, Switch } from 'react-router-dom'
import Posts from '../components/Posts/Posts'
import Post from '../components/Posts/Post'const App = () => {
  return (
    <Switch>
      <Route exact path="/" component={Posts} />
      <Route exact path="/posts/:id" component={Post} />
    </Switch>
  )
}export default App
```

在我们的帖子列表项组件中，我们将添加到各个帖子组件的链接。由于我们正在与 React Router Dome 合作，我们不能只使用标签。相反，我们必须从反应路由器导入链路。该组件应如下所示:

```
import React from 'react'
import { Link } from 'react-router-dom'const PostListItem = ({post}) => {
  return(
    <div>
      <Link to={`/posts/${post.id}`}>
        <h2>{post.attributes.title}</h2>
      </Link>
      <p>{post.attributes.body}</p>
    </div>
  )
}export default PostListItem
```

我们现在无法运行应用程序，因为我们正在导入不存在的帖子组件。让我们制作一个快速组件，以便了解现在是否一切正常。

# 阅读

在“app/JavaScript/src/components/Post/Post”处制作一个包含以下内容的组件:

```
import React from 'react'const Post = () => {
  return(
    <div>
      <h1>This is the Post Component</h1>
    </div>
  )
}export default Post
```

转到"[http://localhost:3000/posts/123 "](http://localhost:3000/posts/123%E2%80%9D)，您应该会看到新的 Post 组件。

你也可以去 [http://localhost:3000/](http://localhost:3000/) 查看我们放在那里的链接，链接到特定的 Post 组件。

我们已经有了 Post 组件，现在让我们将它连接到我们的 api。我们将设置我们的组件，以便在组件呈现时获取 post，然后一旦它获得数据，它将再次呈现，这次使用新数据。

这将为我们的组件设置它需要的正确数据:

```
import React, { useEffect } from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { getPost } from '../../actions/posts'const Post = ({match}) => {
  const dispatch = useDispatch()
  const post = useSelector(state => state.post)
  const postId = match.params.id useEffect(() => {
    dispatch(getPost(postId))
  }, []) return(
    <div>
      <h1>This is the Post Component</h1>
    </div>
  )
}export default Post
```

这里，我们从 URL 获取 id，然后使用该 Id 从后端获取文章数据。关于 useDispatch 和 useSelector 的更多解释，[见第 2 部分](/how-to-set-up-react-js-with-a-ruby-on-rails-project-part-2-redux-31ac07638f34)。

注意，如果你正在跟随我以前的教程，我放错了一个“结束”在我的控制器里。我必须在继续前进之前解决这个问题。

现在，只需要用我们帖子中的信息填充页面。

```
import React, { useEffect } from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { getPost } from '../../actions/posts'const Post = ({match}) => {
  const dispatch = useDispatch()
  const post = useSelector(state => state.post)
  const postId = match.params.id useEffect(() => {
    dispatch(getPost(postId))
  }, []) if (!post) { return <div>Loading....</div>} return(
    <div>
      <h1>{post.attributes.title}</h1>
      <p>{post.attributes.body}</p>
    </div>
  )
}export default Post
```

现在你知道了！那是 CRUD 的 R。现在，让我们继续从前端创建记录。

# 创造

首先，我们需要在“app/JavaScript/src/components/Posts”中创建表单。新”。表单看起来是这样的:

```
import React, { useState } from 'react'
import { useDispatch } from 'react-redux'
import { createPost } from '../../actions/posts'
import { useHistory } from "react-router-dom";const New = () => {
  const dispatch = useDispatch()
  const history = useHistory()
  const [formData, setFormData] = useState({
    title: "",
    body: ""
  }) const handleSubmit = (e) => {
    e.preventDefault()
    dispatch(createPost({post: formData}))
    history.push("/")
  } return (
    <div>
      <h1>New Post</h1>
      <form onSubmit​={handleSubmit}>
        <label htmlFor="title">Title</label>
        <input onChange​={(e) => setFormData({...formData, title: e.target.value})} type="text" name="title" id="title" value={formData.title} />
        < br />
        <label htmlFor="body">Body</label>
        <textarea onChange​={(e) => setFormData({...formData, body: e.target.value})}  name="body" id="body" cols={30} rows={10} value={formData.body}></textarea>
        < br />
        <input type="submit" value="Create Post" />
      </form>
    </div>
  )
}export default New
```

如果这段代码让你感到困惑，我有一篇关于在 React 中使用表单的文章。

在这个表单中，我们创建一个新的 Post 对象，然后重定向回主页。如果你现在尝试把它发送到你的后台，你会遇到一个错误。您需要转到您的 posts_controller.rb 并添加以下内容:

用::null_session 防止伪造

让我们将最后一部分添加到我们的减速器中。这只是更新我们 Redux 存储中的 posts 键。

```
import { GET_POSTS, CREATE_POST } from '../types/index'export default (posts = [], action ) => {
  switch (action.type) {
    case GET_POSTS:
      return action.payload
    case CREATE_POST:
      return [...posts, action.payload]
    default:
      return posts
  }
}
```

如果到目前为止你已经完成了所有的工作，它应该可以工作了，现在我们已经在 CRUD 中完成了创建。

# 破坏

现在是时候摧毁我们的模型了。我们已经设置了动作创建器。我们需要配置我们的减速器。首先，我们需要在 Redux 存储中使用 DESTROY_POST 操作类型从 posts 键中删除帖子，如下所示:

```
import { GET_POSTS, CREATE_POST, DESTROY_POST } from '../types/index'export default (posts = [], action ) => {
  switch (action.type) {
    case GET_POSTS:
      return action.payload
    case CREATE_POST:
      return [...posts, action.payload]
      case DESTROY_POST:
        return posts.filter(post => post.id != action.payload)
    default:
      return posts
  }
}
```

我们正在浏览我们的帖子，并过滤掉刚刚删除的帖子。接下来，让我们在 post reducer 中将我们的 post 设置为 null:

```
import { GET_POST, DESTROY_POST } from '../types/index'export default (post = null, action ) => {
  switch (action.type) {
    case GET_POST:
      return action.payload
    case DESTROY_POST:
      return null
    default:
      return post
  }
}
```

我这样做的原因是，当我们删除文章时，文章也被设置为 Redux 存储中的文章关键字。

接下来，让我们用下面的代码在“app/JavaScript/src/components/Posts/edit . js”创建一个新组件

```
import React, { useEffect } from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { getPost, destroyPost } from '../../actions/posts'
import { useHistory } from "react-router-dom"; const Edit = ({ match }) => {
  const dispatch = useDispatch()
  const history = useHistory()
  const post = useSelector(state => state.post)
  const postId = match.params.id const handleClick = () => {
    dispatch(destroyPost(postId))
    history.push("/")
  } useEffect(() => {
    dispatch(getPost(postId))
  }, []) if (!post) { return <div>Loading...</div>} return (
    <div>
      <h1>{post.attributes.title}</h1>
      <button onClick​={handleClick}>Delete me</button>
    </div>
  )}export default Edit
```

现在，您应该对这些很熟悉了—我们只是删除了这一次。并确保将路线添加到您的 App.js 文件中。

```
import React from 'react'
import { Route, Switch } from 'react-router-dom'
import Posts from '../components/Posts/Posts'
import Post from '../components/Posts/Post'
import New from '../components/Posts/New'
import Edit from '../components/Posts/Edit'const App = () => {
  return (
    <Switch>
      <Route exact path="/" component={Posts} />
      <Route exact path="/posts/new" component={New} />
      <Route exact path="/posts/:id" component={Post} />
      <Route exact path="/posts/:id/edit" component={Edit} />
    </Switch>
  )
}export default App
```

这就是我们要做的——摧毁已经完成。再来一个，我们就完了！

# 更新

我们将使用刚刚为删除操作创建的 Posts/Edit.js 组件。在这个组件中，我们只需要设置一个表单，就像创建一个新帖子一样。

您的 Posts/Edit.js 文件应该如下所示:

```
import React, { useEffect, useState } from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { getPost, destroyPost, updatePost } from '../../actions/posts'
import { useHistory } from "react-router-dom"; const Edit = ({ match }) => {
  const dispatch = useDispatch()
  const history = useHistory()
  const post = useSelector(state => state.post)
  const postId = match.params.id const handleClick = () => {
    dispatch(destroyPost(postId))
    history.push("/")
  }
  const [formData, setFormData] = useState({
    title: '',
    body: ''
  }) useEffect(() => {
    dispatch(getPost(postId))
  }, []) useEffect(() => {
    if (post) {
      setFormData({
        title: post.attributes.title || '',
        body: post.attributes.body || ''
      })
    }
  }, [post]) if (!post) { return <div>Loading...</div>} const handleSubmit = (e) => {
    e.preventDefault()
    dispatch(updatePost(postId, {post: formData}))
    history.push("/") } return (
    <div>
      <form onSubmit​={handleSubmit}>  
        <h1>{post.attributes.title}</h1>
        <label htmlFor="title">Title</label>
        <input onChange​={(e) => setFormData({...formData, title: e.target.value})} type="text" name="title" id="title" value={formData.title} />
        <br />
        <label htmlFor="body">Body</label>
        <textarea onChange​={(e) => setFormData({...formData, body: e.target.value})} name="body" id="body" cols={30} rows={10} value={formData.body}></textarea>
        <br />
        <button onClick​={handleClick}>Delete me</button>
        <input type="Submit" value="Save" />
      </form>
    </div>
  )}export default Edit
```

这类似于我们的 create 方法——我们有一个表单设置，并使用我们的动作创建器 updatePost()。唯一看起来奇怪的是这部分:

```
useEffect(() => {
    if (post) {
      setFormData({
        title: post.attributes.title || '',
        body: post.attributes.body || ''
      })
    }
  }, [post])
```

看到那张[海报]了吗？每当 post 值改变时，这个 useEffect()钩子就会运行。这意味着在我们联系后端并用 post 更新 Redux 存储之后，这个函数运行并为我们的表单设置默认值。

我们要做的最后一件事就是在 Redux store 中发布我们的帖子。在“app/JavaScript/src/reducers/posts . js”中添加 UPDATE_POST:

```
import { GET_POSTS, CREATE_POST, DESTROY_POST, UPDATE_POST } from '../types/index'export default (posts = [], action ) => {
  switch (action.type) {
    case GET_POSTS:
      return action.payload
    case CREATE_POST:
      return [...posts, action.payload]
    case DESTROY_POST:
      return posts.filter(post => post.id != action.payload)
    case UPDATE_POST:
      let updatedPosts = posts.map(post => {
        if (post.id === action.payload.id) {
          return action.payload
        } else {
          return post
        }
      })
      return updatedPosts
    default:
      return posts
  }
}
```

在这里，我们只是映射我们的帖子，并找到我们刚刚更新的帖子。然后我们用新帖子替换旧帖子。

现在我们有了。我们现在已经在 React on Rails 应用程序中实现了 CRUD 函数。我计划下一步做认证。一定要在 Twitter 上关注我，这样我发布的时候你就知道了。

*更多内容尽在*[plain English . io](http://plainenglish.io/)