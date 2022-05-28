---
title: Element-Ui初体验
date: 2022-05-27 +/-TTTT
categories: [项目,Vue通用后台管理系统]
tags: []     # TAG names should always be lowercase
---

## Element-UI在网页中使用

### CDN引入Element-UI
1.引入样式<br>
```html

<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
```

2.引入js<br>
```html
<!-- Vue必须在element-ui之前引入，因为element-ui.js是基于Vue的 -->
<script src="https://unpkg.com/vue@2/dist/vue.js"></script>
<!-- import JavaScript -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

### 打开对话框示例
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <!-- import CSS -->
    <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
    <title>对话框</title>
</head>

<body>
    <div id="app">
        <el-row>
            <el-button @click="open">打开对话框</el-button>
        </el-row>
        <el-dialog title="标题" :visible.sync="dialogVisible" width="30%">
            <span>内容</span>
            <span slot="footer" class="dialog-footer">
                <!-- 3.取消或关闭操作， dialogVisble=false -->
                <el-button @click="dialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>

    </div>
</body>

<!-- 在element-ui.js引入之前引入Vue.js -->
<script src="https://unpkg.com/vue@2/dist/vue.js"></script>
<script src="https://unpkg.com/element-ui/lib/index.js"></script>

<script>
    new Vue({
        el: '#app',
        data: function () {
            // 1.dialogVisble，对话框是否显示
            return { dialogVisible: false }
        },
        methods: {
            // 2.open方法，dialogVisible=true
            open() {
                this.dialogVisible = true;
            }
        }
    })
</script>

</html>
```

## Element-Ui在脚手架中使用

### element-ui完整引入和按需引入
1.安装模块：`npm i element-ui -S`<br>
2.完整引入：在main.js中写入以下内容<br>
```js
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

3.按需引入：如果只需要引入Button，Select组件，像下面这样就可以使用了，当然也需要在main.js中操作<br>
```js
import Vue from 'vue';
import { Button, Select } from 'element-ui';
import App from './App.vue';

Vue.use(Button)
Vue.use(Select)

new Vue({
  el: '#app',
  render: h => h(App)
});
````

按需引入避免了引入大量不需要的组件，能够大幅节省程序空间


