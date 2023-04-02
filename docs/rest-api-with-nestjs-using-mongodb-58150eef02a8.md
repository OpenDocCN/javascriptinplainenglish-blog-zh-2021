# 用 NestJS 和 MongoDB 构建一个 REST API

> 原文：<https://javascript.plainenglish.io/rest-api-with-nestjs-using-mongodb-58150eef02a8?source=collection_archive---------6----------------------->

![](img/2d28f270f19a18d196c42a02cf8a8865.png)

NestJS + MongoDB

嘿，伙计们，让我们创建一个 NestJS REST API，但是在继续之前，请确保您已经先阅读了[入门](/getting-started-with-nestjs-application-overview-installation-setup-288e0e83c889)文章。

在上一篇文章中，我们已经熟悉了基本的 NestJS 概念，让我们开始连接数据库并创建一个实际的 REST API。

## **概述**

对于数据库，您可以使用 MySQL、MongoDB 或 PostgreSQL 等，但对于本例，我们将使用 MongoDB，为了将其与我们的应用程序连接，我们将使用`mongoose`作为 ODM，这允许我们与数据库连接，并在模式构建和验证方面提供了更大的灵活性。

**先决条件**

*   以前的经验与 MongoDB，Mongoose 将是有益的
*   REST API 的基本知识
*   承诺的基本知识，异步等待。

# *我们开始吧！*

首先转到 MongoDB，创建一个帐户并创建第一个数据库集群。

一旦创建了数据库，让我们确保我们的 IP 地址在白名单中&我们有一个数据库用户可以从我们的 NestJS 应用程序无缝地访问数据库。

首先，我们需要创建一个 DB 用户和白名单 IP。

转到您的集群，然后单击`connect`，这将提示您创建一个用户并允许 IP 地址访问数据库。

![](img/ebcb6f751c019d3f3e2f2ae43b24a2fc.png)

MongoDB Cluster Options

点击`Add Your Current IP Address`，它会将你当前的 IP 地址列入白名单，并允许你使用当前的 IP 地址进行连接。

完成后，通过添加用户名和密码为您的数据库创建一个用户，您也可以自动生成密码，然后单击选择连接方法。

选择连接类型:

![](img/51b7862ee768e6816f6b983870dde406.png)

Connect your application

一旦看到该屏幕，您需要选择第二个选项`Connect your application`。

![](img/28e31342e06ba735d28dd9ec5c0870f9.png)

Mongo URI model

现在你将在这个屏幕上，它将向你显示一个 mongo 连接字符串，包含你的用户名和数据库的详细信息。

复制该字符串，用您的实际密码替换`<password>`，并将`myFirstDatabase`更改为适合您的用例的数据库名称。

*注意:如果您的密码包含特殊字符，您应该对它们进行 URL 编码，否则您在从 NestJS 应用程序建立连接时将会遇到问题。*

让我们从 Mongo URI 和 mongoose 创建数据库连接。为此，转到`app.module.ts`并添加以下代码:

```
...
import { MongooseModule } from '@nestjs/mongoose';@Module({ imports: [
    MongooseModule.forRoot('mongodb+srv://db-admin:v0PYTcgsc91oHPUn@cluster0.m3i8w.mongodb.net/api-demo?retryWrites=true&w=majority'),
],
  controllers: [AppController],
  providers: [AppService],
})export class AppModule {}
```

这将通知应用程序，我们希望与数据库连接，因为这是我们的应用程序包含导入的主要模块，这将确保应用程序一启动就连接到数据库。

现在，让我们来看看您的项目，为我们的 API 端点创建一些文件，它们是`*.controller.js`、`*.module.js`、`*.service.js`，因为我们需要定义模式，所以我们将使用`*.model.js`

转到`src`目录并创建一个`products`文件夹，并为该模块创建模型、模块、控制器和服务，一旦创建完成，将如下所示:

![](img/6b0f40e58323b95d6e8ab463a24e9e5d.png)

Product module

无论需要哪一个与产品相关的端点，我们都将在控制器中创建它，但是要这样做，我们首先需要定义我们的产品模式。

这是我们如何定义它的，在我们的例子中，我们的产品将有 3 个字段，名称、描述和价格，所以它将被定义如下，并且因为我们使用 typescript，让我们确保我们为产品定义了接口，以便在我们需要时验证产品。

```
import * as mongoose from 'mongoose';

export const ProductSchema = new mongoose.Schema({
  name: { type: String, required: true },
  description: { type: String, required: true },
  price: { type: Number, required: true },
});

export interface Product extends mongoose.Document {
  id: string;
  name: string;
  description: string;
  price: number;
}
```

让我们在`product.module.js`中添加代码，它包装控制器和服务，并在您的模块中导入所需的功能。

```
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';@Module({ imports: [
    MongooseModule.forFeature([
      { name: 'Product', schema: ProductSchema }
    ]),
  ],
  controllers: [],
  providers: [],
});
```

在这里，我们添加了 ProductSchema 作为这个特定特性的产品，并且我们通知模块，我们将在控制器、服务中需要这个模式，如果您的模块使用更多的模块、模式，您需要如上导入它们。

现在转到`products.service.ts`，让我们将模型注入到构造函数中，所以让我们添加这段代码

```
...
import { InjectModel } from '@nestjs/mongoose';
import { Product } from './product.model';@Injectable()
export class ProductsService {
  constructor(
   @InjectModel('Product') private readonly productModel: Model<Product>,
  ) {}
}
```

您需要确保您对`@InjectModel(‘Product’)`的命名与您在`product.module.js`中的命名相同。同样，这将是一个超模型模式，我们不会以任何方式修改它，我们保留了`private`和`readonly`。在`Model<>`中传递的`Product`不是 mongo 模式，它是我们已经定义的 typescript 接口。

我们几乎已经涵盖了创建第一个端点的所有内容，所以让我们开始吧。我们将创建第一个 POST 端点，这将允许我们创建产品。

转到`product.controller.ts`并添加以下代码:

```
import { Controller, Post, Body } from '@nestjs/common';@Controller('products')
export class ProductsController {
  constructor(private readonly productsService: ProductsService) {}

  @Post()
  async addProduct(
    @Body('title') prodTitle: string,
    @Body('description') prodDesc: string,
    @Body('price') prodPrice: number,
  ) {
    const generatedId = await this.productsService.createProduct(
      prodTitle,
      prodDesc,
      prodPrice,
    );
    return { product };
}
```

`Controller`、`Post`、`Body`是 NestJS 提供的装饰器，同样我们也有其他 REST API 方法装饰器，我们也有`Headers`和`Params`的装饰器，你也可以创建你的[自定义装饰器](https://docs.nestjs.com/custom-decorators)，这将允许你在任何你需要的地方使用它们。

让这个端点运行的最后一件事，正如你看到的，我们正在使用来自`productsService`的`createProduct`，但是我们还没有定义它，所以要定义它，请转到`product.service.ts`并在`constructor`下面添加`createProduct`函数。

```
...
async createProduct(title: string, desc: string, price: number) {
  const newProduct = new this.productModel({
    title,
    description: desc,
    price,
  });
  const result = await newProduct.save();
  return result;
}
```

现在，让我们将所有这些添加到我们的`product.module.ts`中，以便我们的应用程序知道从哪里为这些端点提供服务，以及应该调用哪些服务，为此，添加以下代码:

```
...
**import { ProductsController } from './product.controller';
import { ProductsService } from './product.service';**@Module({
  imports: [
    MongooseModule.*forFeature*([{ name: 'Product', schema: ProductSchema}]),
  ],
 **controllers: [ProductsController],
  providers: [ProductsService],** })
```

这就对了。您已经成功设置了您的第一个端点，现在让我们尝试使用来自 [Postman](https://www.postman.com/) 的这个端点。如果您还没有安装它，请先安装它并提出以下请求。

*(提示:Postman 可能会提示您创建一个帐户，但是您可以在不创建帐户的情况下使用它，检查窗口底部您会看到* `*Skip Sign in*` *选项。)*

## **创建第一个请求**

*   创建新请求
*   将方法更改为**帖子**
*   将 URL 改为指向您的 NestJS 服务器，在我们的例子中是`localhost:3000`
*   根据您的用途添加适当的端点，在我们的例子中是`/products`

![](img/d766216d27838866da5db9677a84e073.png)

POST /products

*   一旦你添加了所有这些细节，点击发送按钮，等待结果。如果您已经正确地添加了所有内容，适当地设置了数据库，您将看到以下结果。

![](img/45bb63d7eae8417608c769780077a076.png)

POST /products response

*(如果出现任何错误，请阅读错误，以了解问题并尝试调试该问题。如果您面临数据库连接问题，请确保您当前的 IP 地址在 MongoDB 集群上的白名单中。)*

让我们添加一个 **GET** 端点来检索我们添加的所有产品。

在`products.service.ts`中创建一个新服务:

```
async getProducts() {
  const products = await this.productModel.find().exec();
  return products;
}
```

*(提示:如果您想修改您的产品以具有特定的字段，您可以循环通过* `*products*` *并决定您需要哪些字段)*

现在添加一个控制器来利用这个服务，之后我们可以从邮递员那里调用它。在`product.controller.ts`中添加以下代码

```
...
@Get()
async getAllProducts() {
  const products = await this.productsService.getProducts();
  return products;
}
```

![](img/0f07619a28add162d3b66dbd7b411e6f.png)

现在，到 Postman 创建一个指向`localhost:3000/products`的 **GET** 请求，点击 **Send** 按钮查看响应，它应该是这样的:

![](img/0f07619a28add162d3b66dbd7b411e6f.png)

GET /products example

那么，下一步是什么？让我们尝试通过特定的 ID 来获取产品，并更新和删除产品。

要通过 ID 获取产品，请在`product.controller.ts`中添加以下代码:

```
@Get(':id')
getProduct(@Param('id') prodId: string) {
  return this.productsService.getProductById(prodId);
}
```

在这里查看 Params 的用法，我们从 Params 中提取 ID，并使用该 ID 来检索特定的产品。我们还需要添加一个`getProductById`服务，所以让我们将它添加到`product.service.ts`中

```
async getProductById(productId: string) {
  const product = await this.findProduct(productId);
}
```

您仍然需要定义`findProduct`函数来确保这个端点工作良好！所以让我们继续把它添加到`product.service.ts`里面

```
...
private async findProduct(id: string): Promise<Product> {
  let product;
  try {
    product = await this.productModel.findById(id).exec();
  } catch (error) {
    throw new NotFoundException(`Product with ID: ${id} does not exist.`);
  }
  if (!product) {
    throw new NotFoundException(`Product with ID: ${id} does not exist.`);
}
  return product;
}
```

一个新的错误`NotFoundException`，对吗？那是 NestJS 提供的错误处理，可以像下面这样导入:

```
import { NotFoundException } from '@nestjs/common';
```

还有许多其他可用的异常，您可以直接使用这些异常来为您处理那些错误案例！

现在，您可以点击来自 postman 的 API，让我们创建一个新的请求 **GET** `localhost:3000/products/<id>`，用您创建的最近的产品 ID 替换`<id>`，现在点击`SEND` 按钮，您应该会看到产品作为响应。

![](img/32ce170f04dc770c9ac7b476b885ef45.png)

GET /product/:id

现在让我们添加一个**补丁**请求:

当更新一个产品时，我们需要用一个特定的 ID 来更新产品，这个 ID 将出现在`params`中，新的数据将出现在`body`中，所以让我们使用这两个装饰器并创建一个**补丁**端点。

内部`product.controller.ts`:

```
...
@Patch(':id')
async updateProduct(
  @Param('id') productId: string,
  @Body('name') productName: string,
  @Body('description') productDesc: string,
  @Body('price') productPrice: number,
) {
  const result = await this.productsService.updateProduct(
    productId,
    productName,
    productDesc,
    productPrice,
  );
  return result;
}
```

内部`product.service.ts`:

```
...
async updateProduct(
  productId: string,
  name: string,
  desc: string,
  price: number,
) {
  const updatedProduct = await this.findProduct(productId);
  const result = await updatedProduct.update({
    $set: {
      name: name ? name : updatedProduct.name,
      description: desc ? desc : updatedProduct.description,
      price: price ? price : updatedProduct.price,
    },
  });
  if (result.n === 0) {
    throw new NotFoundException(`Product with ID: ${productId} does not exist.`,
    );
  }
  return {
    message: `A product with ID: ${productId} has been updated successfully`,
  };
}
```

很好，在使用这个 API 之前，让我们添加 **DELETE** 请求，一起尝试一下。

首先添加删除服务:

```
...
async deleteProduct(productId: string) {
  const result = await this.productModel.deleteOne({ 
    _id: productId
  }).exec();
  if (result.n === 0) {
    throw new NotFoundException(`Product with ID: ${productId} does not exist.`);
  }
  return {
    message: `A product with ID: ${productId} has been updated successfully`,
  };
}
```

现在为此添加一个控制器:

```
...
@Delete(':id')
async removeProduct(@Param('id') productId: string) {
  const res = await this.productsService.deleteProduct(productId);
  return res;
}
```

瞧啊。您已经完成了，现在让我们前往 postman，尝试这些端点，看看效果如何。

创建一个新的请求**补丁** `localhost:3000/products/<id>`，用您希望更新的产品 ID 替换`<id>`。转到`Body`选项卡，添加您希望更新的字段。在我们的例子中，我们正在更新名称和价格

![](img/35123870f44b2755301323c742a18145.png)

PATCH /products/:id

点击相同产品的 GET 请求，查看您的产品是否已更新:

![](img/0a74e1c437e365f80884d7cfa4b6e42d.png)

GET /products/:id

创建更多的产品并尝试使用 GET、PATCH 端点，然后让我们尝试删除端点:

创建新请求**删除** `localhost:3000/products/<id>`，用您希望删除的产品 ID 替换`<id>`，并点击发送按钮，这将从我们的数据库中删除该产品。

![](img/7e9a2c88bea18a0ee03b9ba3ee365dca.png)

DELETE /products/:id

您还可以尝试一个随机 ID 来检查它是否抛出异常，也可以对 PATCH 和 GET 端点进行同样的尝试！😉

万岁，就是这样！现在您可以自己创建一个简单的 REST API 了！

对于更大规模的应用程序，你应该使用额外的装饰器和函数来确保它是 ***安全，快速&可靠*** ！

# 结论

感谢你阅读这篇文章。如果这有助于您创建第一个 NestJS REST API，请在评论中告诉我。如果您正在寻找更多与开发相关的文章，请关注我！对于任何疑问，你可以在下面评论。

谢谢你，快乐阅读，并有一个好的！😄