## Vue全家桶学习笔记 Vue-router
---
### 1. 前端路由原理

改变url，不刷新页面

1. 利用hash改变地址
    ```
    location.hash = "home"
    ```
2. 利用H5的history模式
    ```
    history.putState({},'','home')
    history.relaceState({},'','about')
    history.back()
    history.forward()
    history.go(1)
    history.go(-2)
    ```

---
### 2. 安装vue-router

1. 安装

    ```
    npm install vue-router --save
    ```
2. 使用
    + 导入路由对象
        ```
        import VueRouter from 'vue-router'
        ```
    + 在Vue中注入该对象
        ```
        Vue.use(VueRouter)
        ```
    + 创建路由实例，并导出
        ```
        export default const router = new VueRouter({
            routers:[]
        })
        ```
    + 在`main.js`中挂载路由 
        ```
        new Vue({
            el: '#app',
            router,
            render: h => h(App)
        })
        ```
    + 在需要的地方使用：
        1. `<router-link>`: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个`<a>`标签.
        2. `<router-view>`: 该标签会根据当前的路径, 动态渲染出不同的组件.
        网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和`<router-view>`处于同一个等级.
        在路由切换时, 切换的是`<router-view>`挂载的组件, 其他内容不会发生改变.

    

---
### 3. 配置路由

1. 配置信息

    ```
    new VueRouter({
        //指定是否使用h5 history模式
        mode: 'history',
        //活动class具体的名称也可以通过这个属性进行修改 
        linkActiveClass: 'active'
        routers:[
            {
                path: '/',
                //重定向
                redirect:'/home'
            },
            {
                path: '/',
                name: 'Home',
                component: Home,
                children: [
                    {
                        /*同单个路由配置（path是相对于父路由而言的相对路劲）*/
                    }
                ]
            },
            {
                //动态路由
                path: '/user/:id',
                name: 'Home',
                component: Home
            },
            {
                path: '/about',
                name: 'About',
                //懒加载
                component: () => import('../views/About.vue')
            }
        ]
    })
    ```
2. 标签属性

    + `<router-link>`
        1. tag: tag可以指定`<router-link>`之后渲染成什么组件, 比如上面的代码会被渲染成一个`<li>`元素, 而不是`<a>`
        2. replace: replace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中
        3. active-class: 当`<router-link>`对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.
        4. to: 可以绑定一个对象
            ```
            :to="{
                path:'/home',
                query:{name:'abc',age:18}
            }"
            ```

---
### 4. router对象 

最初创建的那个router对象，在Vue中通过`$router`进行引用。

1. push方法

    ```
    this.$router.push("/home")

    this.$router.push({
        path:'/home',
        query:{name:'abc',age:18}
    })
    ```

---
### 5. route对象

router对象中routers的每个规则，就是一个route，当前的路由用`$route`对象表示。

1. params  
    配置路由格式: `/router/:id`

    ```
    this.$route.params.id
    ```

2. query
    访问路由为：`/router?id=123, /router?id=abc`

    ```
    this.$route.query.id
    ```
3. path  
    当前的路径
4. name  
    当前设置的名字

---
### 6. 导航守卫

+ vue-router提供的导航守卫主要用来监听监听路由的进入和离开的.
+ vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发.
+ 导航首位分为3中（参见官网）：
    1. 全局守卫.
    2. 路由独享的守卫.
    3. 组件内的守卫.

---
### 7. keep-alive

+ keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。
它们有两个非常重要的属性:  
    1. include - 字符串或正则表达，只有匹配的组件会被缓存
    2. exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存
+ router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存

    ```
    <keep-alive>
        <router-view>
            //将被缓存
        </router-view>
    </keep-alive>
    ```






---

#### [返回目录](./)
