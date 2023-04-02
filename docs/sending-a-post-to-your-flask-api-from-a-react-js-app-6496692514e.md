# 如何从 React 应用程序向 Flask API 发送 POST 请求

> 原文：<https://javascript.plainenglish.io/sending-a-post-to-your-flask-api-from-a-react-js-app-6496692514e?source=collection_archive---------1----------------------->

![](img/a486299f4a8f3eb5d33d3cdd69fed1e0.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近一直在学 Flask。我最近在开发一个应用程序时，也一直在处理 POST 请求。Python、Flask 和 SQL 之间的关系使得“数据操作”变得非常容易。虽然我一开始确实很挣扎，但我确实喜欢让自己痛苦，不使用资源，直到我不再能搞清楚事情并向前迈进。

因此，这篇博客文章将帮助初学者和新手从他们的 React 应用程序向 Flask API 发出这些 post 请求。虽然这看起来有点“可怕”或者不是你想尝试的事情，但它实际上非常简单——你只需要有一些方向。

这将是我上一篇博文的延续。因此，如果你不知道如何将 React 应用程序连接到 Flask API，我建议在这里查看我的上一篇博文。

您首先要做的是在文件中定义路由，并将 POST 传递给方法以允许 HTTP 方法被传递。我正在使用 Flask 给我的蓝图，我只是将我的应用程序名称定义为 main。

```
@main.route('/add_todo', methods=['POST'])
```

接下来，您将拥有一个函数，该函数允许从请求中发送的数据存储到 SQL 数据库中，并显示回前端。首先，定义函数并设置一个与请求相等的变量，然后调用内置函数 get_json()。

```
def add_todo():todo_data = request.get_json()
```

这允许您从表单或请求中获取发送的数据，并创建发送数据的新实例。我用内容属性构建了一个名为 Todo 的模型。

```
class Todo(db.Model):id = db.Column(db.Integer, primary_key=True)content = db.Column(db.String)
```

您可以使用为请求设置的变量，并创建该类的新实例。

```
new_todo = Todo(content=todo_data['content'])
```

这里我在 Todo 类的一个实例上设置了另一个变量。我将内容属性设置为前端发送的属性。有了这些数据之后，您希望将它提交给数据库，这样它就被存储起来，您可以将它发送回前端进行显示。

```
db.session.add(new_todo)db.session.commit()return 'Done', 201
```

我调用的 db 变量。会话，。添加、和。commit on 只是我通过调用`db = SQLAlchemy()`创建的一个变量。我将 new_todo 变量传入 add 函数，将 todo 实例添加到数据库中，然后调用 commit 来调用 SQL server 的 commit 语句。

```
@main.route('/add_todo', methods=['POST'])def add_todo():todo_data = request.get_json()new_todo = Todo(content=todo_data['content'])db.session.add(new_todo)db.session.commit()return 'Done', 201
```

现在你有了一个完整的路由来发送数据到你的 Flask API，我个人使用 Postman 来检查我的路由完整性，以确保一切运行良好。这就是我返回“Done”和 201 来验证我的路由运行良好的原因。如果您不想返回任何内容，那么您应该返回 204，这是稍后删除请求所需要的。

完成这个设置后，您可以移动到前端，设置要发送到 Flask API 的表单。发送 POST 请求时需要做的两件主要事情是发送 POST 和在完成后更新状态。

首先，创建一个带有输入字段和按钮的表单，用于输入您的内容，然后将其发送到后端。您还需要使用 state 和 onChange 函数来查看您正在输入的信息。我个人使用钩子，因为它让个人编写代码更容易。如果你不熟悉 Reacts hooks，我有一篇关于它的博文，你可以点击这里查看。

```
<form><input type="text" value={content} onChange={e => setContent(e.target.value)} /><button 
type="submit" 
value="Add Todo"></button></form>
```

这是一个简单的表格。现在，您将需要在按钮单击或表单提交时调用一个 fetch。我个人使用了点击按钮，但这是一个偏好的问题。所以我将创建一个函数，并将其传递给按钮上的 onClick。我也使用 async 和 await，这也是我的偏好。

```
<form><input type="text" value={content} onChange={e => setContent(e.target.value)} /><button 
type="submit" 
value="Add Todo"
onClick={async () => {
const todo = { content };
const response = await fetch("/add_todo", {
method: "POST",
headers: {
'Content-Type' : 'application/json'
},
body: JSON.stringify(todo)
})if (response.ok){
console.log("it worked")}></button></form>
```

这个 onClick 事件处理程序将 POST 请求发送到“/add_todo”路由，并将“内容”传递到上面的输入中。然后我设置了一个名为 response 的变量来检查响应是否被发送，然后记录“它工作了”来验证这一点。

从父组件，我传递了一个名为 onNewTodo 的函数，在其中我更新了状态。然后，我可以在 onClick 事件处理程序中调用它。该函数如下所示:

```
*onNewTodo*={todo => setTodos(currentTodos => [...currentTodos, todo])}
```

我接受正在传递的 todo，并使用我创建的 setTodos 函数将 todo 传递到当前的 Todos 状态。然后，在您的条件中调用这个函数，传入您设置为等于输入内容的 todo 变量，并通过将 content 设置回 nothing 来清除输入。

```
if (response.ok){
 console.log("it worked")
onNewTodo(todo)
setContent('')}
```

您的最终表单应该如下所示:

```
<form><input type="text" value={content} onChange={e => setContent(e.target.value)} /><button 
type="submit" 
value="Add Todo"
onClick={async () => {
const todo = { content };
const response = await fetch("/add_todo", {
method: "POST",
headers: {
'Content-Type' : 'application/json'
},
body: JSON.stringify(todo)
})if (response.ok){
 console.log("it worked")
onNewTodo(todo)
setContent('')}></button></form>
```

现在，您应该有一个可以向 Flask API 发送 POST 请求的表单。我真的建议查看一些帮助我提出其他类型请求的资源，以及更深入的描述。

## 资源

*   Miguel Grinberg 如何创建一个 React + Flask 项目—【https://blog.miguelgrinberg.com/post/how-to-create-a-react —Flask-Project
*   Klebber Correia 用 Python、Flask、React 搭建一个简单的 CRUD App——[https://developer . okta . com/blog/2018/12/20/CRUD-App-with-Python-Flask-React](https://developer.okta.com/blog/2018/12/20/crud-app-with-python-flask-react)

[*更多内容看 plainenglish.io*](http://plainenglish.io/)