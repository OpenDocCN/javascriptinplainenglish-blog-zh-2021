# MongoDB 领域无服务器化:React 版本

> 原文：<https://javascript.plainenglish.io/going-serverless-with-mongodb-realm-react-js-version-44b095832d59?source=collection_archive---------10----------------------->

![](img/db4d22325f0d55b7c00a40f8237b19a0.png)

无服务器架构是一种无需管理基础设施即可运行和构建应用程序和服务的模式。它涉及在服务器上运行的应用程序和服务，但是所有的服务器管理都是由云提供商完成的。

这篇文章将讨论使用 [MongoDB](https://www.mongodb.com/) 、 [MongoDB Realm](https://www.mongodb.com/realm) 和 [React](https://reactjs.org/) 构建一个全栈用户管理应用程序。在本教程的最后，我们将学习如何在 MongoDB 上创建一个数据库，使用 MongoDB Realm 将无服务器功能作为我们的端点，并在 React 应用程序中使用端点。

MongoDB Realm 是一个开发平台，旨在构建移动、web、桌面和物联网应用程序。它提供数据同步、无服务器功能、触发器、用户认证等服务。我们可以使用以下任何一种方法在 MongoDB 领域上构建和维护应用程序:

*   [Realm UI](https://docs.mongodb.com/realm/manage-apps/deploy/manual/deploy-ui/#std-label-deploy-ui) :创建和维护应用程序的基于浏览器的选项
*   [Realm CLI](https://docs.mongodb.com/realm/manage-apps/deploy/manual/deploy-cli/#std-label-deploy-cli) :基于 CLI 的选项，用于定义和部署应用程序
*   [Github 部署](https://docs.mongodb.com/realm/manage-apps/deploy/automated/deploy-automatically-with-github/#std-label-deploy-github):使用 GitHub 上的配置文件从 GitHub 仓库部署应用程序
*   [Admin API](https://docs.mongodb.com/realm/admin/api/v3/#std-label-admin-api) :管理应用程序的基于 HTTP 的请求。

在这篇文章中，我们将使用 [Realm UI](https://docs.mongodb.com/realm/manage-apps/deploy/manual/deploy-ui/#std-label-deploy-ui) 来构建我们的应用程序。

您可以通过克隆这个存储库(**主分支** ) [这里](https://github.com/Mr-Malomz/react-realm)来进行编码。如果您喜欢查看完整的代码，请查看同一个存储库的 **dev** 分支。

在本教程中，我们将只关注实现。已经用 [TailwindCSS](https://tailwindcss.com/) 设置了项目 UI。

你可以在这里查看 Vue.js 版本[。](https://medium.com/javascript-in-plain-english/going-serverless-with-mongodb-realm-vue-js-version-c0f7afae8719)

# 先决条件

这篇文章中的以下步骤需要 JavaScript 和 React 经验。不要求有使用 TypeScript 的经验，但是有这样的经验是很好的。

我们还需要一个 [MongoDB 帐户](https://www.mongodb.com/)来托管数据库并创建无服务器功能。 [**报名**](https://www.mongodb.com/cloud/atlas/register) **完全免费**。

# 让我们编码

## 运行项目

要开始，我们需要导航到项目位置，打开我们的终端并安装项目依赖项，如下所示:

`npm install`

完成后，我们可以使用下面的命令启动开发服务器:

`npm start`

![](img/85aff3028543f6d48510da2b18e30d50.png)![](img/96aaed6a5e9fe85fb014045d9f84a16f.png)

# 设置 MongoDB

首先，我们需要登录或注册我们的 [MongoDB](http://) 账户，并遵循适用于我们的选项:

**对于新账户(注册)** 首先，我们需要回答几个问题来帮助 MongoDB 帮助设置我们的账户。然后点击**完成。**

![](img/1ed5058ad6e26e486446c45524ef21b2.png)

选择**共享**作为数据库类型。

![](img/8c75d1c846d0ed442b93960ae1252253.png)

点击**创建**来设置集群。这可能需要一些时间来设置。

![](img/6abbac3727d586da24eb324e7fe48a14.png)

接下来，我们需要通过输入**用户名**、**密码**来创建一个从外部访问数据库的用户，然后点击**创建用户**。我们还需要添加我们的 IP 地址，以便通过点击**添加我当前的 IP 地址**按钮安全地连接到数据库。然后点击**完成并关闭**保存更改。

![](img/5dc38540611e5e6ed4eec885c6a9a920.png)![](img/e7cbbaaa856f31ee48c680f76f738ec2.png)

保存更改后，我们应该会看到一个数据库部署屏幕，如下所示:

![](img/c6edbe5516831896841cb4f22bcc3473.png)

**对于现有账户(登录)** 点击项目下拉菜单，点击**新建项目**按钮。

![](img/c88ea066ddca5d4741fee699f4e09f5e.png)

输入`reactRealm`作为项目名称，点击**下一个**然后点击**创建项目**

![](img/597f47b592e97fd508ff1c33b3be7872.png)![](img/9921ec4b85493c31651d0162757ece86.png)

点击**建立数据库**

![](img/ac320139fa7ca2157463c50e62310770.png)

选择**共享**作为数据库类型。

![](img/3689a935b29360e40bdce67771f97e95.png)

点击**创建**来设置集群。这可能需要一些时间来设置。

![](img/e0968b7a901e8c0f34fd10e46bf06e40.png)

接下来，我们需要通过输入**用户名**、**密码**，然后点击**创建用户**，来创建一个从外部访问数据库的用户。我们还需要添加我们的 IP 地址，以便通过点击**添加我当前的 IP 地址**按钮安全地连接到数据库。然后点击**完成并关闭**保存更改。

![](img/96c8fa158b8bd0faa8c5066882778ac9.png)![](img/ec6010ebb7890fb9569c2258afd07388.png)

保存更改后，我们应该会看到一个数据库部署屏幕，如下所示:

![](img/356788021499dba7d2ea15c1deab6786.png)

# 加载样本数据

接下来，我们需要用用户的样本数据填充数据库。为此，点击**浏览收藏**按钮

![](img/7b714af780d21aee5983ecdf809523e1.png)

点击**添加我自己的数据**，输入`reactRealmDB`和`reactRealmCol`作为数据库和集合名称，点击**创建**。

![](img/e9f260baab89e2ecda8116708d97392b.png)![](img/c024a59e2fad0376d1fed9a451dfdca9.png)

接下来，我们需要插入这些样本数据:

为此，点击**插入文件**按钮，填写上面的详细信息并点击**插入**进行保存。

![](img/648a81424c0bb7933f09be7ba56a9381.png)![](img/1bfa92963f1e6dbbde5542dcb3b42642.png)![](img/2ab11cef020abd321fe71921df64a61b.png)

# 创建和配置 MongoDB 领域应用程序

填充数据库后，我们需要创建无服务器函数来对数据库执行创建、读取、更新和删除(CRUD)。为此，选择**领域**标签，点击**构建你自己的应用**。然后点击**创建领域应用**来设置我们的应用。

![](img/00e88a04da98caf217e740ed023923d4.png)![](img/cef59a9a008b6b5ea3a15c1b3c2e1298.png)

MongoDB Realm 还附带了模板，我们可以使用这些模板快速构建我们的应用程序。对于本教程，我们将从头开始构建。

接下来，我们需要为我们的函数设置权限和规则。为此，关闭弹出向导点击**规则**，选择**反应栏**并点击**配置集合**。

![](img/f1aa4ace0ade8d1ec7342e8dcc6ce4a8.png)

MongoDB Realm 的保存和部署完成后，MongoDB Realm 将向我们展示一个说明保存和部署概念的小部件。

![](img/a98d0e11c69624106169fd4e77afc2e1.png)

当编写一个无服务器功能时，点击**保存**创建一个开发草案，我们可以测试和试验。同时， **Deploy** 将我们的更改公开给另一个应用程序使用(在我们的例子中是 React)。

点击**下一个**，然后**拿到**继续。

接下来，我们需要允许**读取**和**写入**权限，然后**保存。**

![](img/d813b06ef31212082603f9e24d7cdd3e.png)

接下来，导航到**认证**标签，点击**允许用户匿名登录**，打开**保存草稿**。

![](img/8b663b95894a510cfeb8a3404d569d60.png)![](img/06ecb3da1df4df23a2394284d61eca07.png)

MongoDB Realm 还附带了几个身份验证选项，我们可以研究一下。对于本教程，我们将使用匿名选项。

# 在 MongoDB 领域上创建无服务器功能

**获取所有用户无服务器函数** 配置完成后，我们现在可以创建一个返回用户列表的无服务器函数。为此，导航至**功能**选项卡，点击**创建新功能**，并输入`getAllUsers`作为功能名称

![](img/0963d4ff088c95f542c3af9a3c800ce7.png)![](img/12f1e677be8f64af82de8cec6e76e90b.png)

接下来，选择**功能编辑器**选项卡，将功能修改如下:

上面的代码片段执行了以下操作:

*   创建一个集合变量来访问`reactRealmDB`数据库和`reactRealmCol`集合
*   返回集合中的文档列表。

接下来，我们可以通过点击**运行**按钮查看用户列表来测试我们的功能。

![](img/a2439d9b05afe0fad1ea88709fe07d8e.png)

最后，我们需要复制任何返回的用户的`_id`并保存在某个地方；我们下一个活动需要它。然后点击**保存草稿**为我们的功能创建一个部署草稿。

![](img/20802e0b6681128cd5f8d32496656775.png)

**获取用户无服务器功能** 为此，点击**功能**标签，点击**创建新功能，**并输入`getSingleUser`作为功能名称

![](img/42dcba9c7fc3d928eec001a115ad6962.png)![](img/b7062aae836d658bc43e6db04838e334.png)

接下来，选择**功能编辑器**选项卡，将功能修改如下:

上面的代码片段执行了以下操作:

*   创建一个集合变量来访问`reactRealmDB`数据库和`reactRealmCol`集合
*   通过按 _id 查找返回单个用户。因为 MongoDB 将文档保存在 [BSON](https://en.wikipedia.org/wiki/BSON#:~:text=BSON%20(%2F%CB%88bi%CB%90s,a%20computer%20data%20interchange%20format.&text=It%20is%20a%20binary%20form,originated%20in%202009%20at%20MongoDB.) 中，所以我们需要使用`BSON.ObjectId`将`arg`解析为 BSON。

为了测试我们的功能，导航到**控制台**选项卡，用我们之前复制的用户`_id`替换**导出**功能中的`Hello world!`，然后点击**运行。**

![](img/16488f448da2562cf5da9886b26553d4.png)

最后，我们需要点击**保存草稿**按钮来保存我们的功能。

**编辑用户无服务器功能** 为此，我们需要遵循与上面相同的步骤。

首先，点击**功能**选项卡，点击**创建新功能，**并输入`editUser`作为功能名称。

![](img/d3cd600abc43e9d21acd606809eed386.png)

接下来，选择**功能编辑器**选项卡，将功能修改如下:

上面的代码片段执行了以下操作:

*   修改函数以接受`id`、`name`、`location`和`title`参数
*   创建一个`collection`变量来访问`reactRealmDB`数据库和`reactRealmCol`集合
*   创建一个通过`_id`找到文档的更新变量，更新集合字段并设置一个`returnNewDocument`标志来返回更新后的文档。

接下来，我们可以通过导航到控制台选项卡来测试我们的函数，用必需的参数( **_id、名称、位置和标题**)替换**导出**函数中的`Hello world!`，单击**运行**，然后**保存草稿**。

![](img/fd95d4b9e8ceba3578048cb225586328.png)

**创建一个用户无服务器功能** 要做到这一点，我们需要遵循与前面相同的步骤。

首先，点击**功能**标签，点击**创建新功能，**并输入`createUser`作为功能名称。

![](img/fb6465354389d7da192988b491fe4f94.png)

接下来，选择**功能编辑器**选项卡，将功能修改如下:

上面的代码片段执行了以下操作:

*   修改函数以接受`name`、`location`和`title`参数。
*   创建一个`collection`变量来访问`reactRealmDB`数据库和`reactRealmCol`集合。
*   通过插入参数并返回用户来创建新用户。

接下来，我们可以通过导航到控制台选项卡来测试我们的函数，用必需的参数(**名称、位置和标题**)替换**导出**函数中的`Hello world!`，单击**运行**，然后**保存草稿**。

![](img/322633319631e832faba19524cff89dc.png)

**删除一个用户无服务器功能** 要做到这一点，我们需要遵循和以前一样的步骤。

首先，点击**功能**标签，点击**创建新功能，**并输入`deleteUser`作为功能名称。

![](img/115243cd49e1f4797eb40a43652cbfe5.png)

接下来，选择**功能编辑器**选项卡，将功能修改如下:

上面的代码片段执行了以下操作:

*   修改函数以接受参数。
*   创建一个`collection`变量来访问`reactRealmDB`数据库和`reactRealmCol`集合。
*   创建一个`deleteUser`变量，由`_id`删除。

接下来，我们可以通过导航到控制台选项卡来测试我们的函数，用所需的参数替换**导出**函数中的`Hello world!`，单击**运行**，然后**保存草稿**。

![](img/79c1ca99713f3ec52779b153a2daf2b9.png)

# 部署无服务器功能

要开始在我们的应用程序中使用无服务器功能，我们需要部署它们。为此，点击**审阅草稿&部署**按钮，向下滚动，然后点击**部署**。

![](img/e3fda00cb078f950309ae17b104c8fbb.png)![](img/0e46b3a54f1fe61942c2419661789623.png)

我们应该得到一个提示，显示我们的部署状态。

# 终于！与 React 集成

要将 MongoDB 领域集成到我们的应用程序中，我们需要安装以下依赖项:

`npm i realm-web`

`realm-web`是一个[库](https://github.com/realm/realm-js/tree/master/packages/realm-web#readme)，用于从 web 浏览器访问 MongoDB 领域。

**设置一个环境变量** 首先，我们需要在项目根目录下创建一个`.env`文件，在这个文件中，添加下面的代码片段:

`REACT_APP_REALM_APP_ID=<your-realm-app-id>`

要获取我们的**领域应用 ID** ，我们需要点击复制图标，如下所示:

![](img/29277f9ed7e0fd912e0a4ea47d222fdb.png)

**设置 MongoDB Realm** 接下来，我们需要在`src`文件夹中创建一个`utils`文件夹，在这个文件夹中，创建一个`mongo.client.ts`文件并添加下面的代码片段:

上面的代码片段执行了以下操作:

*   导入所需的依赖项。
*   创建一个变量来存储**领域应用 ID** 。
*   创建并导出 MongoDB 领域的实例，并传递应用程序 ID。REALM_APP_ID 前面的 bang `!`告诉编译器放松非空约束错误(意味着参数不能为空或未定义)
*   创建并导出我们将用于此应用的凭据类型。我们在前面配置了这个身份验证选项。

**获取所有用户** 要获取所有用户，我们需要创建一个接口来描述响应属性。为此，我们需要在`src`文件夹中创建一个`models`文件夹，在这个文件夹中，创建一个`user.interface.ts`文件，并添加下面的代码片段:

**PS**:****_ id****前面的问号告诉 TypeScript 这个属性是可选的，因为是 MongoDB 自动生成的。**

*接下来，我们需要用下面的代码片段来修改`App.tsx`:*

*上面的代码片段执行了以下操作:*

*   *导入`IUser`接口、`app`和`credentials`。*
*   *创建状态变量来管理用户列表。*
*   *在`useEffect`钩子中创建一个`getUsers`函数，使用导入的`credentials`来验证我们的应用程序，通过访问我们之前创建的`getAllUsers`无服务器函数来获取用户列表，然后更新用户的状态。*

> ***PS** :调用的无服务器函数( **getAllUsers** 在我们的例子中)必须与 MongoDB 领域中定义的相同。*

*   *更新标记以显示用户列表。*

***完成 App.tsx***

***创建用户
我们还需要添加状态作为对`useEffect`钩子的依赖；以便在进行更改时，它会刷新页面并加载最新的用户列表。最后，我们需要用状态函数更新`Modal`组件来更新值。***

***PS:** *TypeScript 会抱怨* `*Modal.tsx*` *组件没有****setuser value****属性。我们会解决的。**

*接下来，导航到`components`文件夹中的`Modal.tsx`文件，更新界面，并创建一个用户。*

*上面的代码片段执行了以下操作:*

*   *导入所需的依赖项。*
*   *修改`handleSubmit`函数，使用导入的`credentials`来验证我们的应用程序。通过访问我们之前创建的`createUser`无服务器函数来创建一个用户，传递所需的参数(**名称**、**位置、**和**标题**，然后更新`userValue`和表单状态。*

***编辑用户** 要编辑用户，我们首先要通过创建一个状态变量来管理我们想要编辑的用户的`_id`，从而修改`App.tsx`。我们还更新了`onClick`事件来更新状态变量，并将其作为道具传递给`Modal`组件。*

*接下来，我们需要在点击**编辑**按钮时填充表单。为此，打开`Modal.tsx`并更新，如下所示:*

*上面的代码片段执行了以下操作:*

*   *导入所需的依赖项。*
*   *修改界面和道具，加入`editingId`*
*   *使用`useEffect`有条件地检查它是在编辑还是在创建，使用`getSingleUser`无服务器函数获取所选用户的详细信息，然后更新表单值。`getSingleUser`函数还要求我们使用`BSON.ObjectID`函数将`editingId`转换成字符串。*
*   *通过将窗体状态更新为空字符串来清除效果。*

*接下来，我们需要更新`handleSubmit`函数，通过有条件地检查它是否是更新操作来更新用户的详细信息。接下来，我们需要调用`editUser`无服务器函数并传入所需的参数。最后，更新`userValue`，将表单恢复为默认并关闭模态组件。*

***完成 Modal.tsx***

***删除用户** 要删除用户，我们需要通过创建如下所示的`handleDelete`函数来修改`App.tsx`:*

*上面的代码片段执行了以下操作:*

*   *导入所需的依赖项。*
*   *创建一个将`id`作为参数的`handleDelete`函数，使用`credentials`验证我们的应用程序。使用`deleteUser`无服务器功能删除选定的用户，并更新`userValue`状态。*

***完成 App.tsx***

*最后，我们可以通过启动开发服务器并执行 CRUD 操作来测试应用程序。*

*![](img/f9213fb2ab0ae7e79996802542440559.png)*

# *结论*

*本文讨论了如何在 MongoDB 上创建数据库，使用 MongoDB 领域创建和部署无服务器功能，以及在 React 应用程序中使用端点。*

*您可能会发现这些资源很有帮助:*

*   *[MongoDB 领域](https://docs.mongodb.com/realm/)。*
*   *[尾翼](https://tailwindcss.com/)。*
*   *[Realm-Web SDK](https://github.com/realm/realm-js) 。*
*   *[无服务器计算](https://en.wikipedia.org/wiki/Serverless_computing)。*
*   *[BSON](https://www.mongodb.com/json-and-bson)*

**更多内容看* [*说白了就是*](http://plainenglish.io/) *。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。**