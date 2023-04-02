# 带有 Vue 3 和 Firebase 的 Ionic 框架——照片分享应用

> 原文：<https://javascript.plainenglish.io/ionic-framework-with-vue-3-and-firebase-photo-sharing-app-a3b8f948bbcb?source=collection_archive---------9----------------------->

## 第 3 部分—显示照片和地图

![](img/52661a0ee7ab3394dc459b7c560eafc9.png)

在第 2 部分中，我们介绍了如何利用本机设备特性，比如摄像头和 GPS。在这一部分，我们将看看如何展示这些照片。我们还将看看如何用大头针显示我们拍摄照片的地图。

# 制表符

我们要做的第一件事是改变标签图标和名称。对于选项卡 2，我们将显示一个图像图标，并将该选项卡命名为“图像”。对于选项卡 3，我们将其命名为“地图”并显示一个地图图标。为此，请访问 src/views/Tabs.vue。

在脚本标记的顶部，我们将用图像和地图图标替换椭圆和正方形图标:

```
*import* { **images**, **map**, cameraOutline } *from* 'ionicons/icons';
```

然后在设置方法中，我们将返回它们以便在模板中使用:

```
*setup*() {
 *return* {
  **images**,
  **map**,
  cameraOutline,
 }
}
```

在模板中，我们将用图标和名称替换标签。您的最终文件应该如下所示:

# 显示图像

接下来，我们将致力于显示图像。我们将在第二个选项卡上实现这一点。因此，请转到 src/views/Tab2.vue。我们要做的第一件事是导入我们需要的依赖项。

## 脚本

在脚本标记的顶部添加以下内容:

```
*import* { reactive, toRefs } *from* "vue";*import* {
 IonPage,
 IonHeader,
 IonToolbar,
 IonTitle,
 IonContent,
 **IonSpinner**,
 **IonLabel**,
 **IonCard**,
 **IonImg**,
} *from* "@ionic/vue";*import* { db, auth } *from* "../main";
```

在导出默认值中，我们将注册我们添加的组件:

```
components: {
 IonHeader,
 IonToolbar,
 IonTitle,
 IonContent,
 IonPage,
 **IonSpinner,
 IonLabel,
 IonCard, 
 IonImg,**
},
```

接下来，我们将创建我们的设置方法并添加我们的状态:

```
*setup*() {
 const *state* = *reactive*({
  *photos*:[] *as string*[],
  *loading*: *false*,
 });
}
```

现在，我们将在 setup 方法中创建从 Firebase 获取照片的方法:

```
const *fetchPhotos* = *async* ()=>{
 *state.loading* = *true*;

 const *user* = *auth.currentUser*; const *snap* = *await db
  .collection*("users")
  *.doc*(*user?.uid*)
  *.collection*("images")
  *.get*();

 if(!*snap.empty*){
  *snap.docs.forEach*((*doc*)=>{
   const *data* = *doc.data*();
   if(*data.image*){
    *state.photos.push*(*data.image*);
   }
  });
 } *state.loading* = *false*;
};
```

在 setup 方法中，我们需要做的最后一件事是调用 fetchPhotos 方法，以便它在页面加载时触发并返回状态:

```
*fetchPhotos*();*return* {
 ...*toRefs*(state),
};
```

## 模板

现在我们有了要传递给模板的照片和状态，我们可以构建模板了。我们要做的第一件事是删除 ion-content 标签中的所有内容，并删除 ExploreContainer 组件。如果我们正在获取照片，我们将显示加载器。

如果我们的方法已经完成，我们没有照片，我们将显示一条消息说明这一点。如果我们有照片，我们将通过使用 v-for 循环在屏幕上以卡片的形式显示它们。

我们还将添加一个带有“center”样式的样式标签，以在屏幕中央显示我们的微调器和标签。

您的最终文件应该如下所示:

# 地图

既然我们的照片已经显示在应用程序中，让我们把注意力放在地图选项卡上，并在我们拍照的位置显示大头针。你需要做的第一件事是获得一个谷歌地图 API 密匙。要得到一个，你可以按照这里的说明[。](https://developers.google.com/maps/documentation/javascript/get-api-key)

有了 API 键之后，转到 public/index.html，在结束 head 标记( *< /head >* )之前添加以下内容:

```
<script *src*="http://maps.google.com/maps/api/js?key=YOUR_API_KEY"></script>
```

接下来，转到 src/views/Tab3.vue。在脚本标记的顶部，我们必须告诉 eslint 和 Typescript 忽略所有错误，因为它不知道我们在 index.html 文件中导入了脚本:

```
// *@ts-nocheck* /* *eslint-disable* */
```

接下来，我们将导入一些 Vue 依赖项以及我们的 Firebase auth 和 db 实例:

```
*import* { ref, onMounted } *from* "vue";
*import* {db, auth} *from* '../main';
```

接下来，我们将创建我们的设置方法。我们将添加一个 ref，这样我们就可以访问模板中的一个 div，一个显示地图的方法，一个显示地图大头针的方法，并且在挂载时我们将触发这些方法。最后，您的脚本标记应该如下所示:

为了全屏显示我们的地图，我们还需要添加一个样式标签:

```
<style *scoped*>
#*map* {
 width: 100%;
 height: 100%;
}
</style>
```

我们需要做的最后一件事是编辑模板标签。在模板内部，删除 ion-content 标签中的所有内容，并删除 ExplorerContainer 组件。然后，在 ion content 标记中创建一个 id 为“map”、ref 为“mapRef”的 div。您的最终文件应该如下所示:

# 视频教程

Video Tutorial

# 结论

在这个由 3 部分组成的系列中，我们已经了解了如何编写一个完整的移动应用程序，该应用程序使用相机和 GPS 等本机功能。在第一部分中，我们建立了我们的火基和离子项目。在[第二部](https://diligentdev.medium.com/ionic-framework-with-vue-3-and-firebase-photo-sharing-app-4ddda0c992a3)中，我们用相机拍摄图像，用手机的 GPS 获取用户的位置。在这一部分，我们展示了这些图像和位置。

我希望你喜欢这个系列，并从中获得很多价值。我知道我很开心，也从组装过程中学到了很多。如果您有任何意见、问题或顾虑，请在下面留言。如果你从这个系列中得到任何价值，给我鼓掌。下次再见，祝编码愉快！