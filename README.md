> [nuxt.js官方网站](https://zh.nuxtjs.org/)
#### 一、安装
1. 全局安装```vue-cli```
2. 模板有很多种，当前使用的是express模板  
```
vue init nuxt-community/express-template <project-name>
```
3. 安装依赖包  
``` 
cd <project-name>
cnpm install
```
4. 运行  
```
npm run dev
```
---
#### 二、项目目录结构

```
|——.nuxt
|—— assets （资源目录，用于组织未编译的静态资源，如less，sass或JavaScript）
|—— build
|—— components （组件目录）
|—— layouts （布局页面）
    —— default.vue
    —— error.vue
|—— pages （页面目录）
    —— index.vue
    —— _id.vue
|—— plugins （插件目录）
|—— server
|—— static （静态文件目录，不会被webpack编译，直接映射到根目录）
—— backpack.config.js
—— nuxt.config.js （nuxt配置）
—— package.json
```
---

#### 三、pages页面
##### 1.路由
在pages文件中创建.vue文件，编译后会在```.nuxt/router.js```文件中生成路由：
```
...
routes: [
	{
		path: "/login",
		component: _6924fae4,
		name: "login"
	},
	{
		path: "/",
		component: _01c5df77,
		name: "index"
	},
	{
		path: "/:id",
		component: _c53958c2,
		name: "id"
	}
]
...
```
在vue文件中跳转链接：
```
<nuxt-link to="/login">to login</nuxt-link>
```
---
### 四、head头部管理（vue-meta)
所有页面的公共头部管理在```nuxt.config.js```中配置：
```
...
head: {
    title: 'starter',
    meta: [
        { charset: 'utf-8' },
        { name: 'viewport', content: 'width=device-width, initial-scale=1' },
        { hid: 'description', name: 'description', content: 'Nuxt.js project' }
    ],
    link: [
        { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
}
...
```
在具体页面中使用不同的title，则在```pages/*.vue```文件下添加配置：
```
export default {
    head() {
        return {
            title: 'login page'
        }
    }
}
```
---
### 五、layouts模板
![image](https://segmentfault.com/img/bV1The?w=260&h=356)  
图片来自[技术文章：Nuxt.js实战](https://segmentfault.com/a/1190000012802572)  
pages/*.vue文件的内容会插在```</nuxt>```中
```
// layouts/default.vue
<template>
  <div>
    <nuxt/>
    <my-footer/>
  </div>
</template>
```
> 使用defalut.vue模板，页面都会有footer，如果某些页面不需要或需要添加其他内容，则可以新建一个模板，在pages/*.vue中引用：

```
// layouts/nav.vue

<template>
    <div>
        <div>这里是导航</div>
        <nuxt/>
    </div>
</template>

```
```
// pages/login.vue
...
export defalut {
    layout: 'nav',
    ...
}
...
```