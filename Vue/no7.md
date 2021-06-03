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
    /*
    pushState和replaceState参数：
    状态对象 — state是一个JavaScript对象，通过pushState () 创建新的历史记录条目。无论什么时候用户导航到新的状态，popstate事件就会被触发，且该事件的state属性包含该历史记录条目状态对象的副本。
    标题 — Firefox 目前忽略这个参数，但未来可能会用到。在此处传一个空字符串应该可以安全的防范未来这个方法的更改。或者，你可以为跳转的state传递一个短标题。
    URL — 该参数定义了新的历史URL记录，新URL必须与当前URL同源，否则 pushState() 会抛出一个异常
    */
    history.pushState({},'','home') //添加一个记录
    history.replaceState({},'','about') //替换一个记录
    
    history.back() //这和用户点击浏览器回退按钮的效果相同
    history.forward() //如同用户点击了前进按钮
    
    //用 go() 方法载入到会话历史中的某一特定页面，通过与当前页面相对位置来标志 (当前页面的相对位置标志为0）
    history.go(1)
    history.go(-2)
    
    //可以通过查看长度属性的值来确定的历史堆栈中页面的数量
    history.length
    
    //可以读取当前历史记录项的状态对象state，而不必等待popstate 事件
    history.state
    ```
    
    popstate 事件：
    
    当活动的历史记录项发生变化时， `popstate` 事件都会被传递给window对象。如果当前活动的历史记录项是被 `pushState` 创建的，或者是由 `replaceState` 改变的，那么 `popstate` 事件的状态属性 `state` 会包含一个当前历史记录状态对象的拷贝。

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
        import Vue from 'vue'
        import VueRouter from 'vue-router'
        
        Vue.use(VueRouter)
        ```
    + 创建路由实例，并导出
        ```
        export default new VueRouter({
            routers:[]
        })
        ```
    + 在`main.js`中挂载路由 
        ```
        import router from '@/router'
        
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

    Vue-Router使用  [path-to-regexp](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0) 作为匹配引擎，可以查看更多的`path`写法，查看它的[文档](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0#parameters)学习高阶的路径匹配，还有[这个例子 ](https://github.com/vuejs/vue-router/blob/dev/examples/route-matching/app.js)展示 `vue-router` 怎么使用这类匹配。
    
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
            //嵌套路由
            {
                path: '/home',
                name: 'Home',
                component: Home,
                //子路由（渲染组件对应父路由组件Home中的 <router-view>）
                children: [
                    {
                    	// 配置与单个路由相同
                        // path是相对于父路由而言的相对路劲
                        // 当 /home/profile 匹配成功，
                        // UserProfile 会被渲染在 Home 的 <router-view> 中
                        path: 'profile',
                        name: 'UserProfile',
                        component: UserProfile
                    }
                ]
            },
            {
                // 动态路径参数 以冒号开头
                // 参数值会被设置到 this.$route.params，可以在每个组件内使用
                // 动态路由复用组件，会导致组件生命周期不完整
                path: '/user/:id',
                name: 'Home',
                component: Home
            },
            {
                path: '/about',
                name: 'About',
                //懒加载
                component: () => import('../views/About.vue')
            },
            {
                // 通配符路由，请把通配符路由放在最后一个
                // 可以用作默认路由，（即其他路由都不匹配的时候）
                // 使用一个通配符时，$route.params 内会自动添加一个名为 pathMatch 参数。它包含了 URL 通过通配符被匹配的部分
                //this.$route.params.pathMatch //eg. 'admin'
                path: '*', //或者path: '/user-*'
                name: 'Home',
                component: Home
            },
        ]
    })
    ```
    
    + 匹配优先级
    
      有时候，同一个路径可以匹配多个路由，此时，匹配的优先级就按照路由的定义顺序：**谁先定义的，谁的优先级就最高**。
    
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
    //router.push(location, onComplete?, onAbort?)
    //在 3.1.0+，可以省略第二个和第三个参数，此时如果支持 Promise，router.push 或 router.replace 将返回一个 Promise。
    //点击 <router-link :to="..."> 等同于调用 router.push(...)
    //location可以是一个字符串路径，或者一个描述地址的对象
    
    // 字符串
    this.$router.push('home')
    
    // 对象
    this.$router.push({ path: 'home' })
    
    // 命名的路由
    this.$router.push({ name: 'user', params: { userId: '123' }})
    
    // 带查询参数，变成 /register?plan=private
    this.$router.push({ path: 'register', query: { plan: 'private' }})
    
    //提供了 path，params 会被忽略
    const userId = '123'
    router.push({ name: 'user', params: { userId }}) // -> /user/123
    router.push({ path: `/user/${userId}` }) // -> /user/123
    // 这里的 params 不生效
    router.push({ path: '/user', params: { userId }}) // -> /user
    
    ```
    
    如果目的地和当前路由相同，只有参数发生了改变 (比如从一个用户资料到另一个 `/users/1` -> `/users/2`)，你需要使用 `beforeRouteUpdate` 来响应这个变化 (比如抓取用户信息)

2. 123

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
