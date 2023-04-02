# 如何在 React Native 中将图像上传到 Laravel API

> 原文：<https://javascript.plainenglish.io/how-to-upload-an-image-to-laravel-api-in-react-native-4176f1c00b97?source=collection_archive---------3----------------------->

![](img/aa2f4950701711354c91f094b34e7999.png)

Photo by [Daniel Korpai](https://unsplash.com/@danielkorpai?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在大多数移动应用程序中，将图像上传到服务器是一项非常常见的任务。这项任务对一些开发人员来说可能具有挑战性。本文将一步一步地向您展示如何将 React 本机应用程序上的图像上传到 Laravel API。

本文分为两部分。

*   拉勒韦尔 API
*   React 原生应用

## **第 1 部分:Laravel API**

**步骤 1:** 使用 composer 创建一个新的 Laravel 项目。你可以给它取任何名字，但是在这种情况下，我们将把它命名为 *ImageApi* 。

```
composer create-project --prefer-dist laravel/laravel ImageApi
```

**步骤 2:** 在 ImageApi 项目中创建一个迁移来创建一个 *images* 表。

```
php artisan make:migration create_images_table --create=images
```

**步骤 3:** 在迁移中添加图像字段 *Title* 和 *Uri。*

```
<?phpuse Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;class CreateImagesTable extends Migration
{

    public function up()
    {
        Schema::create('images', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->string('uri');
            $table->timestamps();
        });
    } public function down()
    {
        Schema::drop('images');
    }
}
```

**步骤 4:** 接下来，创建一个名为 Image 的模型

```
php artisan make:model Image
```

**步骤 5:** 在模型中，在可填充数组中添加图像字段和 Uri 字段。

```
<?phpnamespace App;use Illuminate\Database\Eloquent\Model;class Image extends Model
{
    protected $table = 'images'; protected $fillable = [
        'title', 'url'
    ];
}
```

第五步:接下来，创建一个控制器，命名为 ImageController。

```
php artisan make:controller ImageController
```

**第六步:**给图像控制器添加一个名为 *addimage 的函数。*

```
<?phpnamespace App\Http\Controllers;use App\Image;
use App\Http\Controllers\Controller;class ImageController extends Controller
{

    public function addimage(Request $request)
    { $image = new Image; $image->title = $request->title;

        if ($request->hasFile('image')) {

            $path = $request->file('image')->store('images'); $image->url = $path;
        } $image->save(); return new ImageResource($image);
    }
} 
```

**第七步:**最后在 api.php 文件的 routes 文件夹中

```
<?phpuse Illuminate\Http\Request; Route::resource('imageadd', 'Api\ImageController@addimage'); 
```

这将创建一个 Api 端点

> <domain-name>/api/imageadd</domain-name>

React 本机应用程序将访问这个 API 端点。

**第二部分:React 原生应用**

**步骤 1:** 使用 expo 创建一个新的 React 原生项目。称之为 imageUploaderApp。

```
expo init imageUploaderApp
```

**第二步:**然后把 formik 库安装到 app 上。点击阅读 Formik 文档[。](https://formik.org/docs/overview)

```
npm install formik --save
```

**第三步:**将 Expo image Picker 安装到应用程序中。点击阅读 Expo 图像拾取器文档[。](https://docs.expo.io/versions/latest/sdk/imagepicker/)

```
expo install expo-image-picker
```

**第四步:**接下来，安装 RN Blob Fetch 到 app。阅读 RN Blob 获取文档[此处](https://www.npmjs.com/package/rn-fetch-blob)。

```
npm install --save rn-fetch-blob
```

在 React 原生应用的 *App.js* 上

**步骤 5:** 使用 *useState 创建两个状态变量。*第一个变量将存储**图像文件**，第二个变量将存储**图像 URI** 。

```
const [fileContent, setFileContent] = useState(null);
const [fileUri, setFileUri] = useState(null);
```

**步骤 6:** 创建一个处理函数，从系统映像库中选择一个映像。

```
onChooseImagePress = async () => {
  let result = await ImagePicker.launchImageLibraryAsync();

  if (!result.cancelled){
    setFileContent(result.uri);
    setFileUri(result.uri.toString());
  }
}
```

**第 7 步:**然后使用 useFormik 状态钩子创建一个 formik 常量

```
const formik = useFormik({
  initialValues: { title: '' },
  onSubmit: values => {
    RNFetchBlob.fetch('POST', `<domain-name>/api/imageadd`, {

      'Content-Type' : 'multipart/form-data',
    }, 
[
  { 
     name : 'image', 
     filename : fileUri, 
     type:'image/jpeg', 
     data:    RNFetchBlob.wrap(fileContent)
  },
  { 
     name : 'title', 
     data : values.title
  },

    ]).then((resp) => {
      // ...
    }).catch((err) => {
      Alert.alert('An error occurred!', err.message, [{ text: 'Okay' }]);
    })
  }
});
```

最终的 app.js 文件应该如下所示:

```
import React, { useState, useEffect } from 'react';

import { StyleSheet, View, Text, Image, Alert} from 'react-native';

import { useFormik } from 'formik';
import * as ImagePicker from 'expo-image-picker';

import RNFetchBlob from 'rn-fetch-blob';const App = () => {const [fileContent, setFileContent] = useState(null);
const [fileUri, setFileUri] = useState(''); onChooseImagePress = async () => {
  let result = await ImagePicker.launchImageLibraryAsync();

  if (!result.cancelled){
    setFileContent(result.uri);
    setFileUri(result.uri.toString());
  }
}const formik = useFormik({
  initialValues: { title: '' },
  onSubmit: values => {
    RNFetchBlob.fetch('POST', `<domain-name>/api/imageadd`,{

      'Content-Type' : 'multipart/form-data',
    }, 
[
  { 
     name : 'image', 
     filename : fileUri, 
     type:'image/jpeg', 
     data:    RNFetchBlob.wrap(fileContent)
  },
  { 
     name : 'title', 
     data : values.title
  },

    ]).then((resp) => {
      // ...
    }).catch((err) => {
      Alert.alert('An error occurred!', err.message, [{ text: 'Okay' }]);
    })
  }
});return(
        <View>
          <Text>{fileUri}</Text>
          <TextInput
           onChangeText={formik.handleChange('title')}
           value={formik.values.title}
           label='Title'
           placeholder='e.g My Awesome Selfie'
          />

          <Button onPress={() =>    {onChooseImagePress()}} >Choose image...</Button>  
          <Button title='submit' onPress={formik.handleSubmit} >Enter Picture</Button>
        </View>

    )
}export default App;
```

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io/)