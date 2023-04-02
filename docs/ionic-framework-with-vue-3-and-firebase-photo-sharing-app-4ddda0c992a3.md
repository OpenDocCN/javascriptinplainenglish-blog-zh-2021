# 带有 Vue 3 和 Firebase 的 Ionic 框架——照片分享应用

> 原文：<https://javascript.plainenglish.io/ionic-framework-with-vue-3-and-firebase-photo-sharing-app-4ddda0c992a3?source=collection_archive---------6----------------------->

## 第 2 部分—相机和保存照片

![](img/2b74513d6265a4aaf6c605192311fb97.png)

Image by [Free-Photos](https://pixabay.com/photos/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=801891) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=801891)

在[第一部分](https://diligentdev.medium.com/ionic-framework-with-vue-3-and-firebase-photo-sharing-app-9aad3df14908)中，我们复习了如何用 [VueJs](https://vuejs.org/) 建立一个 [Ionic Framework](https://ionicframework.com/) 移动应用。我们还配置了我们的 [Firebase](https://firebase.google.com/) 特性，包括认证、Firestore 和存储。在本文中，我们将介绍如何利用本机设备功能，如摄像头和 GPS。

# 电容器

## 装置

为了给我们的应用添加本地特性，我们将使用[电容器](https://capacitorjs.com/)。要在我们的应用程序中启用 capacitor，请在应用程序的根目录中打开一个终端，并运行以下命令:

```
ionic integrations enable capacitor
```

## 初始化

然后，我们需要在应用程序中初始化电容器。为此，您需要命名您的应用程序，并拥有一个应用程序 id。你的应用 id 应该是唯一的。最佳做法是使用应用程序的名称和网站的域名。com . diligent dev . photosharingapp 就是一个例子。

确定应用程序名称和应用程序 id 后，在项目根目录下打开终端并运行以下命令:

```
npx cap init [appName] [appId]
```

## 建筑物

接下来，我们需要构建我们的应用程序。为此，请运行以下命令:

```
ionic build
```

## 添加平台

现在，我们需要添加我们的平台。如果你想开发 iOS，你需要一台 Mac。对于 Android，你可以在 Windows 或 Mac 上构建。根据您想要构建的版本，您需要在终端中运行以下程序:

```
// Adding iOS (mac only)
npx cap add ios// Adding Android
npx cap add android
```

## 实时重装

为了在模拟器上立即看到我们的变化，我们需要安装 [Ionic 的实时重新加载](https://capacitorjs.com/docs/guides/live-reload)。为此，您需要 Ionic CLI(安装在第 1 部分)和它们的本地运行插件。打开终端并运行以下命令:

```
npm install -g native-run
```

安装后，您可以执行以下命令来运行您的应用程序:

```
// Run iOS
ionic cap run ios -l --external// Run Android
ionic cap run ios -l --external
```

这个 ***应该*** 启动 Andriod Studio 或者 XCode。如果它没有启动它们，请打开。启动后，你可以在各自的 ide 中打开 ios 或 android 文件夹。然后，通过单击 IDE 顶部的播放(运行)按钮运行您的应用程序。

# 选项卡图标和名称

我们将使用第一个选项卡启动相机并保存照片。为了让用户明白这一点，我们将选项卡的图标和名称改为 camera。为此，我们可以删除三角形图标，导入 cameraOutline 图标，并将其返回到模板。

```
*// top of script tag
import* { ellipse, square, **cameraOutline** } *from* 'ionicons/icons';// in export default
*setup*() {*return* {
 ellipse,
 square,
 **cameraOutline**,
 }
}
```

然后，我们将更改模板中选项卡上的图标和标题。您的文件应该如下所示:

Tabs.vue

# 燃料库

回到 src/main.ts，我们需要导入 Firebase 存储，这样我们就可以用它来保存我们的映像。在文件的顶部，将存储模块导入到其他 firebase 导入项下:

```
*import* firebase *from* 'firebase/app';
*import* 'firebase/auth';
*import* 'firebase/firestore';
***import* 'firebase/storage'**
```

然后，在其他 Firebase 导出下面，导出一个存储实例:

```
*export* const *auth* = *firebase.auth*();
*export* const *db* = *firebase.firestore*();
***export* const *storage* = *firebase.storage*();**
```

# 摄像头和 GPS

既然我们的应用程序已经在仿真器上运行，我们就可以访问本地设备特性了。我们将针对的第一个本机功能是拍照并保存到 firebase。为此，导航到 src/views/Tab1.vue。

删除 ion-content 标签中的所有内容，并将 ion-title 重命名为 Camera。我们将该选项卡布局为在屏幕中间有一个按钮来启动相机。我们也会给这个按钮一个图标。

为此，请从@ionic/vue 导入 IonButton 和 IonIcon。我们还需要导入相机图标。

```
*import* {
 IonPage,
 IonHeader,
 IonToolbar,
 IonTitle,
 IonContent,
 **IonButton**,
 **IonIcon**,
} *from* "@ionic/vue";***import* { camera } *from* "ionicons/icons";**
```

接下来，我们需要导入我们的 Firebase 存储实例 Firestore，auth。我们还需要从电容器本地相机和地理定位插件。

```
import {storage, auth, db} from '../main';
import { Plugins, CameraResultType } from '@capacitor/core'; const { Camera, Geolocation } = Plugins;
```

现在我们准备创建保存图像的方法。我们要做的第一件事是创建一个方法来生成一个可以用作文件名的 GUID。这将使得几乎不可能得到冲突的文件名:

```
function *uuidv4*() {
 *return* "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx"
  *.replace*(/[xy]/g, function (c) {
   const *r* =(*Math.random*()*16)|0,
   *v* = *c* =="x"? *r* :(*r* &0x3)|0x8;
   *return* v*.toString*(16);
 });}
```

接下来，在导出默认值中，创建一个设置方法。在其中，我们将创建一个方法来拍摄图像并保存它和 Firestore 中的位置。最后，我们将返回模板所需的所有内容。

```
*setup*() {
 const *takePicture* = *async* ()=>{
 const *image* = *await Camera.getPhoto*({
  *quality*:90,
  *allowEditing*: *false*,
  *resultType*: *CameraResultType.Base64*,
 });

 if(*image?.base64String*){
  //*get user* const *user* = *auth.currentUser*;

  //*create guid* const *guid* = *uuidv4*();

  //*create file path* const *filePath* =`${*user?.uid*}*/images/*${*guid*}*.*${*image.format*}`; //*save to storage* const *storageRef* = *storage.ref*();

  *await storageRef.child*(*filePath*)
   *.putString*(*image.base64String*,'base64'); //*get download url to save in firestore* const *url* = *await storageRef.child*(*filePath*)*.getDownloadURL*(); //*get location* const *loc* = *await Geolocation.getCurrentPosition*(); //*save in firestore
  await db
   .collection*("users")
   *.doc*(*user?.uid*)
   *.collection*("images")
   *.add*({
    *image*: *url*,
    *location*:{ *lat*: *loc.coords.latitude*, *lon*: *loc.coords.longitude* },
   });
  }
 }; *return* {
  camera,
  takePicture,
 };
}
```

我们需要做的最后一件事是编辑模板，以便用户可以与应用程序进行交互。我们只是在屏幕中间有一个按钮供用户拍照。您的最终文件应该如下所示:

Tab1.vue

# 视频教程

Video Tutorial

# 结论

在第 2 部分中，我们设法拍摄了一张照片，获得了用户的位置，并使用最少的代码将其保存在 Firestore 中。在第 3 部分中，我们将重点关注在应用程序中显示图像。所以，如果你还没有的话，一定要关注我，让我通知你。下次再见，祝编码愉快！