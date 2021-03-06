---
title: Vue Router的使用
date: 2022-05-27 +/-TTTT
categories: [前端,Vue]
tags: []     # TAG names should always be lowercase
---

## 什么是路由和路由器
路由就是一组key-value的对应关系<br>
多个路由需要经过路由器进行管理

## vue-router的理解
Vue的一个插件库，专门用来实现SPA应用，其中vue-router就是路由器，而我们创建的一个个链接地址与Vue组件页的键值对就是一个个路由，这些路由被Vue进行管理，当我们访问某个链接时，vue-router就会将指定的Vue组件渲染到对应的位置；使用vue-router的流程图如下：<br>
![vue-router使用流程图](/blog/202205281506527.png "vue-router使用流程图")

## 对SPA应用的理解
1.单页Web应用（single page web application，SPA）<br>
2.整个应用只有一个完整的页面<br>
3.点击页面中的导航链接不会刷新页面，只会做页面的局部更新<br>
4.数据需要通过Ajax请求获取

## 安装Vue Router
1.npm下载：`npm install vue-router@3.5.3`<br>
2.Yarn下载：`yarn add vue-router@3.5.3`<br>

**注意：Vue2应该使用vue-router@3.X.X，这里推荐使用3.5.3版本的**

## 准备我们的组件
在src下创建views文件夹，这里放我们的组件

home.vue<br>
```js
<template>
  <div>Home</div>
</template>

<script>
export default {
    name: 'Home',
    data(){
        return {}
    }
}
</script>
```

user.vue<br>
```js
<template>
  <div>User</div>
</template>

<script>
export default {
    name: 'Home',
    data(){
        return {}
    }
}
</script>
```

## 注册路由
在项目下创建我们的router文件，这里放的是我们注册的路由，新建index.js文件如下：<br>
```js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from '@/views/Home'
import User from '@/views/User'

Vue.use(VueRouter);

export default new VueRouter({
    mode: "history",
    routes:
        [
            {
                path: '/home',
                name: 'Home',
                component: Home
            },
            {
                path: '/user',
                name: 'User',
                component: User
            }
        ]
})
````

## 创建好路由后再main.js配置路由
```js
import Vue from 'vue'
import Element from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue'
import router from '../router'

Vue.config.productionTip = false
Vue.use(Element);

new Vue({
  // 配置名就叫router，不要乱修改，也就是配置路由器
  // router:router,左右相同可以直接写成下面这样
  router,
  render: h => h(App),
}).$mount('#app')
````


## 预设组件的链接
通过点击不同的链接，跳转到不同的组件，当然这一系列擦操作是由路由完成的

在HelloWorld.vue中准备好跳转链接<br>
```js
<template>
  <div class="hello">
    // 其实与a标签类似
    // 不需要引入需要跳转的组件，毕竟我们也没有到，而这种不需要写标签的组件就被称为路由组件，通常被放在views中，而一般组件就被放在components中
    <router-link to="/home">
      <el-button>Home页面</el-button>
    </router-link>
    <router-link to="/user">
      <el-button type="primary">User页面</el-button>
    </router-link>
  </div>
</template>
```

## 选择展示组件的地方
在App.vue中<br>
```js
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld/>
    <router-view></router-view>
  </div>
</template>
```

`<router-view></router-view>`就是组件被展示的地方

## 使用vue-router需要注意的点
![需要注意的点](/blog/202205310057298.png "需要注意的点")