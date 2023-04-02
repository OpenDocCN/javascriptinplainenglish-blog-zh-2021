# 如何使用 Node.js 将文件上传到亚马逊 S3

> 原文：<https://javascript.plainenglish.io/file-upload-to-amazon-s3-using-node-js-42757c6a39e9?source=collection_archive---------2----------------------->

![](img/1d1d0ae058a8fce8bcd52260a82e3647.png)

在本文中，我们将了解如何使用 Node.js 和 Express 将文件推送到 AWS S3。

# 先决条件:

1.  一个 [AWS 账户](https://ap-south-1.console.aws.amazon.com/console/home?region=ap-south-1)。
2.  基本快速设置将使用 Multer 在后端上传文件。如果想了解 Node.js 中基本的文件上传，可以阅读[这个](/uploading-files-in-node-js-using-multer-754526aa6817)。

本文将分为两个部分:

1.创建 AWS S3 存储桶并赋予其适当的权限。

2.使用 JavaScript 从 AWS S3 上传和读取文件。

# 1.创建 AWS S3 存储桶并赋予其适当的权限

**a .创建 S3 桶**

→登录 AWS 控制台，搜索 S3 服务

![](img/456544966544ab85531f552c3b7a4e1e.png)

→创建一个桶。单击创建存储桶。

![](img/dbc59be8fa370f6db824accaceaf5ecc.png)

→写下您的**桶名**和 **AWS 区域**。单击创建存储桶按钮

![](img/30fc0816feaf49bf54f4dfe8fa0b82ff.png)![](img/09f175bdc3eb603e52fc58ad84bbc1d0.png)![](img/f43fc0fcf109fd4e5acdff14f34a22f5.png)

→桶已成功创建。我们将使用 Node.js 将文件上传到这个桶中

→在 Node.js 应用程序中，我们需要存储桶名称和区域。

![](img/09ecdfc283288e3b1aac340e1156ea7f.png)

→由于我们是这个 S3 存储桶的创建者，我可以从 AWS 控制台读取、写入、删除和更新。如果我们想在快递服务器上做。我们需要使用 IAM 策略授予一些权限。

**b .创建 IAM 策略:**

→转到 AWS 中的 IAM 服务

![](img/60f15e51ebeb481fccf41ff94d37a466.png)

→点击政策

![](img/af1707f326bca8d9593bdd6d331ae702.png)

→点击创建策略按钮

![](img/4571baee0f0aa8d67571046c9e65a6d7.png)

→我们现在将创建我们的策略。这是我们新创建的 bucket 所特有的。

→点击选择服务并选择 S3

![](img/6f3c5ef369081b6c52df75f958e22998.png)![](img/c49cf38509ff3d4f5cd5be9bdd2c54b6.png)

→我们可以给予桶许多 S3 权限。对于上传和阅读以下权限将足够了

> getObject —从 S3 阅读
> 
> putObject —给 S3 写信
> 
> 删除对象—从 S3 删除

→点击写入并选择**放置对象**和**删除对象**

![](img/f86fd206c4d2ec240a8b630f45c1bc18.png)![](img/400cf018f77ad64c5dc469080fbe5070.png)

→点击读取并选择 getObject

![](img/f8c7a3b166564c511b47636a31582a6d.png)

→下一步是添加 ARN。ARN 的意思是你斗身份

```
 arn:aws::s3:::<your_bucket_name>       // ARN SYNTAX
```

arn:was::S3::::AWS-每日销售

→我们选择特定的 ARN，因为这些规则将应用于特定的 S3 时段。

→点击添加 arn

![](img/ab32f1433e401904258a441bc8504bb3.png)![](img/2fad5dbe0d2e4b65ea1162e6ea941536.png)

→粘贴您的存储桶名称，并勾选任何对象名称。

![](img/2afb4b6d80024945cde2e3c69a336d87.png)

→我们现在加热几个下一步按钮

![](img/fe794d0e2351281cf5720865249ddac7.png)

→点击**创建策略**

![](img/9f248b713e29773e5a72bd3ef0822364.png)![](img/b8ae01f33b3173803e9f18f5d28694c5.png)

→我们现在看到我们的策略已创建。它具有读取、写入和删除权限。

**c .创建一个 IAM 用户:**

→这可以是访问 S3 桶的物理用户或代码。

→点击 IAM 左侧浏览器中的用户

![](img/0026cd063266b8a6748c536b34e981af.png)

→点击添加用户

![](img/a0e604b847919751543b53fba216ba9b.png)

→写下用户的名字。因为我们的快速应用程序将访问 S3。

给予**编程访问**意味着**代码/服务器**是**用户**将访问它。对于我们的 case Node.js 应用

![](img/313b874131d163b3916c8f1c29003e9d.png)

→最后，我们将获得在 JavaScript 应用程序中使用的**访问密钥 Id 和密钥**，如下所示:

![](img/a0f076840a73e330e12c2c97ab66d013.png)

→在第三个选项卡中，我们附加了上面创建的 IAM 策略。我们现在单击几个“下一步”按钮

![](img/e8a2d1bda0d3dc9082f8deb2c169a09c.png)![](img/ceaebd5047f1a257a8e00877b875b762.png)![](img/93acf0ed9c2ca9f5ea846d15243b1302.png)

→点击创建用户按钮

![](img/c2815a460a38ca5cd4da368f09d7cd60.png)

→我们获得**访问密钥 Id 和密钥**(出于安全原因，不要与任何人共享您的密钥)

![](img/dc1b7250806ca6d67e94235236351b89.png)

→粘贴您的。应用程序的 env 文件

![](img/f4cb9da573dd4fa1233be415abd8c7d4.png)

→下一步是写一些 javascript 代码，向 S3 读写代码。

# 2.使用 JavaScript 从 AWS S3 上传和读取文件

**a .文件上传概要(使用 Multer):**

→ Express 有两种发布路径——单条和多条，分别使用 Multer 上传单幅和多幅图像。

→图像保存在服务器/公共/图像中。

→利用前端调用两条路线的客户端应用程序

完整文章请在这里[阅读。](/uploading-files-in-node-js-using-multer-754526aa6817)

**b .将 AWS 与 Express 集成**

→创建。env 文件并粘贴您的 AWS 凭证

```
AWS_BUCKET_NAME="aws-daily-files"
AWS_BUCKET_REGION="ap-south-1"
AWS_ARN=arn:aws:s3:::aws-daily-files
AWS_ACCESS_KEY=AKIAS3D3V2NC4EJAMEEZ
AWS_SECRET_KEY=3WE************************pcH
```

→使用以下命令安装 AWS SDK

```
npm install aws-sdk dotenv
```

→在应用程序中创建 s3.js 文件

c.给 S3 写信:

```
**require**("dotenv").**config**();const **S3** = **require**("aws-sdk/clients/s3");const **fs** = **require**("fs");const bucketName = process.env.AWS_BUCKET_NAME;const region = process.env.AWS_BUCKET_REGION;const accessKeyId = process.env.AWS_ACCESS_KEY;const secretAccessKey = process.env.AWS_SECRET_KEY;const s3 = new **S3**({ region, accessKeyId, secretAccessKey,}); *// UPLOAD FILE TO S3*function **uploadFile**(file) { const fileStream = **fs**.**createReadStream**(file.path); const uploadParams = { Bucket: bucketName, Body: fileStream, Key: file.filename, };return s3.**upload**(uploadParams).**promise**(); // this will upload file to S3}module.exports = { **uploadFile** };
```

![](img/41f31daec572c2a8e2257f258dc29070.png)

→现在转到您的路线文件

服务器/路由器/索引. js

```
var **express** = **require**("express");var router = **express**.**Router**();const upload = **require**("../common");const { **uploadFile** } = **require**("../s3");const **fs** = **require**("fs");const **util** = **require**("util");const **unlinkFile** = **util**.**promisify**(**fs**.**unlink**); router.**post**("/single", upload.**single**("image"), async (req, res) => { console.**log**(req.file); *// uploading to AWS S3* const result = await **uploadFile**(req.file);  // Calling above function in s3.js console.**log**("S3 response", result); *// You may apply filter, resize image before sending to client* *// Deleting from local if uploaded in S3 bucket* await **unlinkFile**(req.file.path); res.**send**({ status: "success", message: "File uploaded successfully", data: req.file, });});module.exports = router;
```

→我们创建了一个[基本前端](https://github.com/AmirMustafa/upload_file_nodejs/blob/master/client/src/App.js),它发送数据以表示后多部分数据

![](img/56a947316cae02acb8e5c60fc75e56b2.png)![](img/c27eb1d315e92ea37f95d641e990c002.png)![](img/8d764c8e76ad3ebeca11b2885a0fb161.png)![](img/3a1bb4a40646861097a1c470a2544f99.png)

→从 S3 读取数据并在客户端打印如下。现在，我们将看到数据将被上传，也是在自动气象站控制台的 S3 桶。

上传前的 AWS 控制台

![](img/397b63e5fd5b2b710e5f958ec5fb4142.png)

→点击发送到后端按钮

→在 Node.js 服务器终端中，我们看到从 S3 打印的响应。这里的关键字是文件名，路径是文件的位置。

![](img/8c1063f1652422ec11be5116ae439fdd.png)![](img/71a4b5c8d087e98ad2dcb0833af4d986.png)

→让我们检查一下 S3。我们看到 S3 上传了一个新文件

![](img/0f0e6010e1f260579224e450fdd3fdef.png)![](img/a266843efad6f390a6ab9298dc488dc0.png)

d.正在从 S3 读取文件:

→我们从上图中看到，新图像反映了来自 S3 的客户端。让我们为它编写代码。

server/s3.js

```
**require**("dotenv").**config**();const **S3** = **require**("aws-sdk/clients/s3");const **fs** = **require**("fs");const bucketName = process.env.AWS_BUCKET_NAME;const region = process.env.AWS_BUCKET_REGION;const accessKeyId = process.env.AWS_ACCESS_KEY;const secretAccessKey = process.env.AWS_SECRET_KEY;const s3 = new **S3**({
  region,
  accessKeyId,
  secretAccessKey,
});*// DOWNLOAD FILE FROM S3*function **getFileStream**(fileKey) { const downloadParams = { Key: fileKey, Bucket: bucketName,};return s3.**getObject**(downloadParams).**createReadStream**();}module.exports = { **uploadFile**, **getFileStream** };
```

![](img/18533d3c3cd3982d4ba104c059b0ccb4.png)![](img/9d24296f16bcc6996ab332256a7ad6fd.png)

→使用此功能路线

服务器/路由/索引. js

```
var **express** = **require**("express");var router = **express**.**Router**();const upload = **require**("../common");const { **uploadFile**, **getFileStream** } = **require**("../s3");const **fs** = **require**("fs");const **util** = **require**("util");const **unlinkFile** = **util**.**promisify**(**fs**.**unlink**); router.**get**("/images/:key", (req, res) => { const key = req.params.key; console.**log**(req.params.key); const readStream = **getFileStream**(key); readStream.**pipe**(res);  // this line will make image readable});// eg <serverurl>/images/[1636897090753-Coffee_book.jpeg](https://s3.console.aws.amazon.com/s3/object/aws-daily-files?region=ap-south-1&prefix=1636897090753-Coffee_book.jpeg) // to be used in client
```

![](img/af655a5a813b66886623c0d0e2cf9c53.png)![](img/fcb9b96e65f3fd678f67d4d2c1af2ae4.png)

→在前端，我们将利用 **S3 响应键**并在客户端使用

![](img/56a947316cae02acb8e5c60fc75e56b2.png)

# 视频:

[https://secure . vidyard . com/organizations/1904 214/players/pkyercdjvxuobrcn 8 tcgs？edit = true&npsRecordControl = 1](https://secure.vidyard.com/organizations/1904214/players/pkYErcDdJVXuoBrcn8Tcgs?edit=true&npsRecordControl=1)

# 存储库:

[https://github.com/AmirMustafa/upload_file_nodejs](https://github.com/AmirMustafa/upload_file_nodejs)

# 结束语:

我们已经学习了如何从 AWS S3 存储桶上传和读取文件。

> 谢谢你一直读到最后🙌。如果您喜欢这篇文章或学到了新东西，请点击下面的分享按钮来支持我，与更多的人联系，和/或在 [Twitter](https://twitter.com/amir__mustafa) 上关注我，查看我学到的其他技巧、文章和事情，并在那里分享。

[](https://twitter.com/amir__mustafa) [## 关注 Amir Mustafa 的 JavaScript、TypeScript 和 AWS 内容。

### twitter.com](https://twitter.com/amir__mustafa) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)