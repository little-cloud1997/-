### 前端路由

在早期的前后端不分离时，每次请求 URL，后端都会返回一个 HTML。所以早期的网站开发，整个 HTML 页面是由服务器来渲染的，服务器直接生产渲染好的 HTML 页面，返回给客户端进行提示。但一个网站有很多的页面，服务器要如何处理呢？

+ 一个页面有自己对应的网址，也就是 URL；
+ URL 会发送到服务器，服务器会通过正则对该 URL 进行匹配，并且交给最后一个 Controller 进行处理；
+ Controller 处理之后，最终生成 HTML 或者数据，返回给前端；

上面的这种操作就是后端路由，当页面中需要请求不同的路径内容时，直接交给服务器来处理，服务器渲染好整个页面，并返回给客户端。这种情况下渲染好的页面，不需要单独加载任何的 CSS 和 JavaScript，可以直接交给浏览器进行展示，也利于 SEO 的优化。

但后端路由有个缺点，就是后端人员要学会编写 HTML 代码，或者前端人员要懂后端语言。而且 HTML 代码和数据以及对应而逻辑会混合在一起，编写和维护都是非常糟糕的事情。

于是便有了前后端分离，每次请求涉及到的静态资源，都从静态资源服务器中获取。这些资源包括 HTML、CSS、JavaScript，然后在前端对这些请求回来的资源进行渲染，此时后端只返回数据。这样做的最大优点就是前后端责任清晰，后端专注于数据上，前端专注于页面展示、交互和可视化上。

但这么做还有路由切换的问题，于是便有了前端路由，也就是前端来维护一套路由规则。而前端路由的核心说白了就是改变 URL，但是页面不进行整体刷新。

那么问题来了，前端路由是如何做到 URL 和内容的映射呢？答案是监听 URL 的改变。URL 有一个 hash 属性，也就是锚点（#），本质上就是改变 window.location 的 href 属性。我们可以直接赋值 location.hash 来改变 href，但是页面不刷新。

~~~sh
"http://www.xxx.com" 打开一个页面
"http://www.xxx.com/#/s/wd=py" 页面不刷新
~~~

下面就来看看前端如何定义路由，当 URL 不同时，展示不同的内容。

>  首先需要安装 vue-router，直接 npm install 即可。

~~~html
<!-- components/Login.vue -->
<template>
  <h2>欢迎来到登录页面</h2>
</template>

<!-- components/Index.vue -->
<template>
  <h2>欢迎来到首页</h2>
</template>
<!-- App.vue -->
<template>
  <div>
    <h2>-------------</h2>
    <!-- 相当于占位符，根据 URL 显示指定的组件内容 -->
    <router-view></router-view>
  </div>
</template>

<script>
</script>

<style scoped>
</style>
~~~

然后是 main.js，我们要创建路由，然后注册到 app 里面。

~~~JavaScript
/* eslint-disable */
import { createApp } from 'vue'
import App from './App.vue'

// 从 vue-router 里面导入相应的函数
import {createRouter, createWebHashHistory, createWebHistory} from "vue-router"
// 此处不使用 import xxx from "vue" 的方式，而是直接用 import
// 并且以箭头函数的形式，可以实现路由的懒加载（总之按照这种模式编码即可）
const Login = () => import(/* webpackChunkName: 'login' */"./components/Login.vue")
const Index = () => import(/* webpackChunkName: 'index' */"./components/Index.vue")
// 创建一个路由：映射关系
let routers = createRouter({
  // 指定采用的模式，是对比 URL 还是对比哈希值
  // createWebHashHistory() -> hash
  // 对比 URL：/login，对比哈希值：/#/login
  history: createWebHistory(),
  // 映射关系
  routes: [
    // name：给路由起一个名字（必须唯一，也可以不起名字），path：路由地址，component：显示的组件
    {name: "login", path: "/login", component: Login},  // 访问 /login 显示 Login 组件
    {name: "index", path: "/index", component: Index},  // 访问 /index 显示 Index 组件
    // 当然还有其它属性，比如 redirect：负责重定向到指定的 URL
    // meta：我们的自定义属性可以通过 meta 属性传递

    // 比如访问 /login，那么就用 Login 组件的内容替换掉 App.vue 中的占位符 <router-view>
  ]
})

let app = createApp(App)
// 将路由组 router 应用在 app 里面
app.use(routers)
app.mount('#app')
~~~

在 vue 里面文件名字必须是多个字符，如果想禁用这一点，那么需要在根目录创建一个文件：.eslintrc.js

~~~JavaScript
module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/essential',
    'eslint:recommended'
  ],
  parserOptions: {
    parser: '@babel/eslint-parser'
  },
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
     //在rules中添加自定义规则
	   //关闭组件命名规则
     "vue/multi-word-component-names":"off",
  },
  overrides: [
    {
      files: [
        '**/__tests__/*.{j,t}s?(x)',
        '**/tests/unit/**/*.spec.{j,t}s?(x)'
      ],
      env: {
        jest: true
      }
    }
  ]
}

~~~

然后我们来看一下效果。























































































































