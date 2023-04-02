# 如何在 Vue.js/Vuetify 导入客户端文本文件

> 原文：<https://javascript.plainenglish.io/importing-client-text-files-in-vue-vuetify-a9ef0a76c821?source=collection_archive---------7----------------------->

![](img/c4a2b3a517c25b87bc886437d66079c4.png)

我在做一个 Vue.js/Vuetify 网站项目。该项目为用户提供了从文件导入 JSON 数据的能力。根据我在 90 年代的“老派”经验，我对这种情况的默认反应是让服务器参与进来，但我决定研究更新的可能性。

我很快找到了[这个](https://www.delftstack.com/howto/javascript/read-text-file-in-javascript/) HTML/JS 方法，但是我不确定它会如何使用 Vue，所以我做了一些实验。因为我也在使用 Vuetify，所以我使用了带有`@change`属性的`<v-file-input>`,并将其路由到一个方法。结果，它接收用户在本地机器上指定的文件的文件对象。

这意味着我可以使用`.text()`方法来读取文件的内容。使用 Vuetify，这也意味着，我可以使用“隐藏输入”属性，只得到一个打开文件浏览器对话框的可点击图标。我还使用了“prepend-icon”属性来更改默认的回形针图标。

为了使它看起来合适，我做了一些调整，但是我最终得到了一个标准的图标按钮，当点击它时，会打开一个文件浏览器对话框。一旦他们选择了一个文件，它就会被导入到工具中，并且可以被查看/修改。

“上传”按钮的单页组件(带有工具提示)如下所示:

```
<template>
  <div>
    <v-tooltip bottom>
      <template #activator="{ on }">
        <v-btn icon>
          <v-file-input class="pl-3"
            clearable 
            @change="loadFile"
            hide-input
            prepend-icon="mdi-database-arrow-up-outline"
            v-on="on"
          ></v-file-input>
        </v-btn>
      </template>
      <span>Upload / Import Data</span>
    </v-tooltip>
  </div>
</template><script>
import { mapActions } from "vuex";
export default {
  props: ["value"],
  computed: {
    visible: {
      get() {
        return this.value;
      },
      set() {
        this.$emit("close");
      }
    }]
  },
  methods: {
    ...mapActions(["import"]),
    loadFile(file) {
      if (!file) return;
      file.text()
        .then(JSON.parse)
        .then(this.import);
    }
  }
  };
</script>
```

我的 Vuex 存储中的“import”功能实际上将 JSON 数据集成到应用程序中。

我喜欢这种方法，因为它不需要向/从服务器发送/接收数据，这意味着对用户来说非常快。

## 只有 Vue 一个人

单独使用 Vue，您可以获得相同的功能，但它需要多几行代码(至少在我第一次使用时是这样的):

```
<input type="file" @change="showFile" />
```

在方法中:

```
showFile(e){
  e.target.files[0]
    .text()
    .then(JSON.parse)
    .then(this.import);
}
```

也有可能创建它，这样只有一个按钮是可见的，触发文件浏览器对话框，但它会更复杂，这就是为什么我喜欢使用 Vuetify(或类似的)。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***