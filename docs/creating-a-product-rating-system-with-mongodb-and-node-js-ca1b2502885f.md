# 用 MongoDB 和 Node.js 创建一个产品评级系统

> 原文：<https://javascript.plainenglish.io/creating-a-product-rating-system-with-mongodb-and-node-js-ca1b2502885f?source=collection_archive---------1----------------------->

![](img/67a926e6545ebe2f90d682fd18bb5642.png)

Source: Getty

# 介绍

在本教程中，您将学习如何充分利用 Mongoose 模式混合类型、getters 和 setters 来操作 MongoDB 数据库中的数据

大多数产品评级系统，如亚马逊的系统，利用加权平均系统。加权平均值的计算方法与“正常”简单平均值几乎相同，只是总和中的每个单位都有一个乘数，称为权重。例如在五星评级系统中。一颗星的权重为 1，两颗星的权重为 2，依此类推。

# 例子

假设一个产品有以下星级评价。

一颗星— — 8 颗

两颗星--10 颗

三星--7 颗

四颗星--5 颗

五星— — 3 颗

简单的平均值是

```
const SA = (8+10+7+5+3) / 5
***console***.log(***Math***.round(SA)) // 2
```

加权平均值为:

```
const WA = ((1*8) + (2*10) + (3*7) + (5*3))/(10+8+7+5+3) 
***console***.log(***Math***.round(WA)) // 2
```

加权平均系统给出了更好的结果，因为它给出了消费者对该产品的看法的良好印象。

如何实现这一点？

在后台实现这一点意味着你不仅需要一个地方来存储每个产品的评分，还需要一个地方来存储每个 start 收到的数字。解决这个问题有不同的方法。就个人而言，我更喜欢 Mongoose 模式混合类型与 setters 和 getters 的组合。

要求

对于这个项目将只需要 Mongoose 作为我们的 MongoDB 驱动程序和一个本地 Mongo shell，并可选地为良好的可视化指南针。

首先，让我们创建一个简单的节点项目并安装 Mongoose。

```
npm install -s mongoose
```

创建一个文件 model.js 并启动本地 Mongo 客户端

```
const mongoose = ***require***('mongoose');

const connectDB = async () => {
     try{
         const conn = await mongoose.connect('mongodb://localhost:27017/myapp', {useNewUrlParser: true, useFindAndModify: false})
         ***console***.log(`MongoDb connected: ${conn.connection.host}`)
         return conn
     }
     catch (e) {
         ***console***.error(e);
         ***process***.exit(1);

     }
 };
```

接下来，让我们为产品集合创建一个基本的 mongoose 模式。它只有两个路径，一个是保存产品名称的字符串路径，一个是存储产品评级的混合路径对象。

```
const ProductSchema = new mongoose.Schema({
    name: ***String***,
    ratings:{
        type: mongoose.Mixed, 
 // A mixed type object to handle ratings. Each star level is represented in the ratings object
        1: ***Number***, //  the key is the weight of that star level
        2: ***Number***,
        3: ***Number***,
        4: ***Number***,
        5: ***Number***,
    default: {1:1, 2:1, 3:1, 4:1, 5:1}}
    }) 
```

因为我们使用 getters，所以请确保在 schema 对象中包含以下选项，以便在获取 JSON 或 JavaScript 对象时可以使用 getters

```
{toObject:{getters: true, }, toJSON:{getters: true}}
```

# Getter 函数

接下来，我们将编写一个 getter 函数，用于从评级路径中获取产品的评级。当我们在路径上调用 getter 函数时，它接受一个表示路径的参数。在这种情况下，它是一个普通的 JavaScript 对象，包含我们的明星评论。这简化了 getter 函数。如下图。

```
get: function(r){
    // r is the entire ratings object
    let items = ***Object***.entries(r); // get an array of key/value pairs of the object like this [[1:1], [2:1]...]
    let sum = 0; // sum of weighted ratings
    let total = 0; // total number of ratings
    for(let [key,value] of items){
        total += value;
        sum += value * parseInt(key); // multiply the total number of ratings by it's weight in this case which is the key
    }
    return ***Math***.round(sum / total)
},
```

# Setter 函数

此函数将处理评级路径的值设置。它将使我们有一个简单的界面来更新产品的评级。假设用户给产品的评分是 3，或者我们想用一个新的对象替换整个评分对象。我们希望能够用这样的简单在线更新产品的评级。

```
product.ratings = 3
product.ratings = {1:1, 2:1, 3:1, 4:1, 5:1}
Product.findByIdAndUpdate(id, {$inc:{'ratings.3': 1}})
Product.findByIdAndUpdate('61084b72b346c52e8482ed3b', {ratings: {1:3, 2:1, 3:1, 4:1, 5:1}}, {new: true})
```

前两个片段会将三星评级的数量更新 1。而另外两个将向评级路径分配新的对象。

```
set: function(r){
    if (!(this instanceof mongoose.Document)){
        // only call setter when updating the whole path with an object
        if(r instanceof ***Object***) return r
        else{throw new ***Error***('')}
    }else{
        // get the actual ratings object without using the getter which returns  an integer value
        // r is the ratings which is an integer value that represent the star level from 1 to 5
        if(r instanceof ***Object***){
            return r    // handle setting default when creating object
        }
        this.get('ratings', null, {getters: false})[r] = 1 + parseInt(this.get('ratings', null, {getters: false})[r])
        return this.get('ratings', null, {getters: false})} // return the updated ratings object
},
```

setter 函数有点复杂，因为我们需要获取该文档的 rating 对象，而不需要使用 getter 返回一个整数值。setter 函数的参数要么是我们想要更新的星级，要么是一个 JavaScript 对象，它包含作为键的星级，就像模式中指定的那样。Mongoose setters 在运行更新操作和直接分配路径时都会被调用。不同之处在于，当运行更新操作时，函数中的“this”指的是查询对象，而不是我们正在更新的 mongoose 文档的实例，这使得我们很难对子路径执行自定义更新操作，因为我们正在更新特定的子路径，而不是整个路径。因此，如果有人试图使用任何 Mongoose 模型更新方法用整数值更新整个路径，我们将抛出一个错误。

setter 函数中剩下的逻辑很简单，我们将简单地获取产品评级对象，而不使用 getters，然后使用 setter 函数的参数来更新特定的路径，之后我们将返回更新后的评级对象。

# 确认

添加一个验证器来防止一次增加一个以上的子路径值是很好的，但是，当使用增量运算符“$inc”时，Mongoose 验证器不会运行，因此，在将数据传递给数据库之前，由我们来验证数据。我们的验证器函数将简单地防止在我们的模式中指定的级别之外添加额外的星级。

```
validate:{
    validator: function(i){
        let b = [1, 2, 3, 4, 5] // valid star levels
        let v = ***Object***.keys(i).sort()
        return b.every((x, j) => (v.length === b.length) && x === parseInt(v[j]))
    },
    message: "Invalid Star Level"
},
```

# 测试

让我们创建一个产品，并在有和没有 getters 的情况下对其进行控制台日志记录，看看它是什么样子的。下面是我们的代码。然后我们可以复制产品 id 来测试我们的更新方法和验证器。

```
const create = async () => {
    let prod = await product.create({name: "Product One"})
    // display the newly created object with and without getters
    ***console***.log(prod)
    ***console***.log(prod.get( 'ratings', null, {getters: false}))
}
create()

// result without the getter
{
    ratings: 3,
        _id: 61069af7547cd8335409a926,
    ***name***: 'Product One',
    __v: 0,
    id: '61069af7547cd8335409a926'
}

// the ratings object
{ '1': 1, '2': 1, '3': 1, '4': 1, '5': 1 }
```

看到我们的吸气剂在工作。我们将尝试以几种不同的方式更新我们产品的评级，以测试我们的 setters。

让我们写一个代码给我们的产品一个五星评级。如您所见，只需将评分对象的值指定为 5，我们就可以将五星评价的数量从 1 更新为 2。平均评级仍然是 3，因为我们在获得评级时使用了加权平均计算。

```
const test1 = async () => {
    // increment a particular star level.
    // by assigning directly to the ratings object
    let prod = await product.findById('61084b72b346c52e8482ed3b')
    prod.ratings = 5
    prod.markModified('ratings')  // Add markModified because ratings is a mixed object type
    prod.save()
    ***console***.log(prod.get( 'ratings', null, {getters: false}))
    ***console***.log(prod)
}test1()

{ '1': 1, '2': 1, '3': 1, '4': 1, '5': 2 }

{
    ratings: 3,
        _id: 61084b72b346c52e8482ed3b,
    ***name***: 'Product One',
    __v: 0,
    id: '61084b72b346c52e8482ed3b'
}
```

# 结论

一如既往，在计算机科学中，有许多方法可以解决一个问题，有些方法比其他方法更直观。然而，找到一个适应性强、可维护、包含最少代码的解决方案总是更可取的。

完整的代码可以在 https://github.com/Ichinga-Samuel/Rating-System.git 找到

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)