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
### 3. 配置路由与标签

1. 配置信息

    Vue-Router使用  [path-to-regexp](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0) 作为匹配引擎，可以查看更多的`path`写法，查看它的[文档](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0#parameters)学习高阶的路径匹配，还有[这个例子 ](https://github.com/vuejs/vue-router/blob/dev/examples/route-matching/app.js)展示 `vue-router` 怎么使用这类匹配。
    
    ```
    new VueRouter({
        //指定是否使用h5 history模式
        //要在服务端增加一个覆盖所有情况的候选资源：
        //如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面
        //这个页面就是你 app 依赖的页面。
        //参考 后端history配置
        mode: 'history',	//"hash" | "history" | "abstract"
        base: "/",	//应用的基路径
        scrollBehavior (to, from, savedPosition) {
            // return 期望滚动到哪个的位置
        },
        //活动class具体的名称也可以通过这个属性进行修改 
        linkActiveClass: 'active',
        linkExactActiveClass: 'active',
        //提供自定义查询字符串的解析/反解析函数。覆盖默认行为
        parseQuery(query){return query},
        stringifyQuery(query){return query},
        //当浏览器不支持 history.pushState 控制路由是否应该回退到 hash 模式。默认值为 true
        fallback:true,
        routers:[
            {
                path: '/',
                //重定向  重定向不会触发路由守卫
                redirect:'/home'
                //或者是对象
                //redirect:{name: 'Home'}
                //或者是方法（route对象是参数）
                //redirect: to => {
                // 方法接收 目标路由 作为参数
                // return 重定向的 字符串路径/路径对象
                //}
            },
            //普通路由
            {
                path: '/home',
                name: 'Home',
                component: Home,
                // 元信息，用于存储一个特征
             	meta: { requiresAuth: true }
            },
            //别名路由 【重要】
            {
                path: '/home',
                name: 'Home',
                alias: '/home2'  //访问home2也会访问到home，地址不变，相当于转发
                //主要用于在内层嵌套路由中，需要一个外层地址访问
                component: Home,
            },
            
            //多视图路由 【重要】
            {
                path: '/home',
                name: 'Home',
                component: {
                	default: Home, //对应 <router-view></router-view>
                	a: Bar,  //对应 <router-view name="a"></router-view>
                	b: Baz	//对应 <router-view name="b"></router-view>
                },
            },
            //路由参数 【重要】
            {
                path: '/home',
                name: 'Home',
                //true的时候，route.params下的属性，将作为props传入组件
                props: true
                //props 是一个对象，它会被按原样设置为组件属性。当 props 是静态的时候有用
                //props:{ newsletterPopup: false }
                //创建一个函数返回 props。这样你便可以将参数转换成另一种类型
                //props: route => ({ query: route.query.q })
                component: Home,
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
            //动态路由 【重要】
            {
                // 动态路径参数 以冒号开头
                // 参数值会被设置到 this.$route.params，可以在每个组件内使用
                // 动态路由复用组件，会导致组件生命周期不完整
                path: '/user/:id',
                name: 'Home',
                component: Home
            },
            //懒加载 【重要】
            {
                path: '/about',
                name: 'About',
                //懒加载
                component: () => import('../views/About.vue'),
                //把某个路由下的所有组件都打包在同个异步块 (chunk) 中
                //只需要使用 命名 chunk (opens new window)，
                //一个特殊的注释语法来提供 chunk name (需要 Webpack > 2.4)。
                component: () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
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
    

---

###  4. 标签属性

+ `<router-link>`

    1. **tag:** tag可以指定`<router-link>`之后渲染成什么组件, 比如上面的代码会被渲染成一个`<li>`元素, 而不是`<a>`

    2. **replace:** boolean类型，replace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中

    3. **append**：boolean类型，设置 append 属性后，则在当前 (相对) 路径前添加基路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

    4. **active-class:** 当`<router-link>`对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.

    5. **exact**：boolean类型，是否开启严格的激活模式。严格的激活模式，只有在to和当前路由完全匹配才激活。否则只要当前路由包含to就激活。

    6. **exact-active-class**：字符串类型，严格匹配的class样式。

    7. **event**：字符串类型，表示什么事件触发导航。默认是"click"

    8. **to:** 可以绑定一个对象或者path字符串

        ```
        :to="{
            path:'/home',
            query:{name:'abc',age:18}
        }"
        ```

    9. **v-slot**：使用 v-slot API 时，需要向 router-link 传入一个单独的子元素。否则 router-link 将会把子元素包裹在一个 span 元素内。

       ```html
       <router-link
         to="/about"
         custom
         v-slot="{ href, route, navigate, isActive, isExactActive }"
       >
         <NavLink :active="isActive" :href="href" @click="navigate"
           >{{ route.fullPath }}</NavLink
         >
       </router-link>
       ```

       - `href`：解析后的 URL。将会作为一个 `a` 元素的 `href` attribute。
       - `route`：解析后的规范化的地址。
       - `navigate`：触发导航的函数。**会在必要时自动阻止事件**，和 `router-link` 同理。
       - `isActive`：如果需要应用[激活的 class](https://router.vuejs.org/zh/api/#active-class) 则为 `true`。允许应用一个任意的 class。
       - `isExactActive`：如果需要应用[精确激活的 class](https://router.vuejs.org/zh/api/#exact-active-class) 则为 `true`。允许应用一个任意的 class

+ `<router-view>`

    1. **name**：多视图路由

    

---
### 4. router对象 

最初创建的那个router对象，在Vue中通过`$router`进行引用。

属性：

```
1. app 配置了 router 的 Vue 根实例
2. mode 路由使用的模式
3. currentRoute 当前路由对应的路由信息对象
4. START_LOCATION 以路由对象的格式展示初始路由地址，即路由开始的地方。可用在导航守卫中以区分初始导航
```



**Vue Router 的导航方法 (`push`、 `replace`、 `go`) 在各类路由模式 (`history`、 `hash` 和 `abstract`) 下表现一致。**

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

2. replace方法

    ```
    //router.replace(location, onComplete?, onAbort?)
    //<router-link :to="..." replace> 与 该方法相同
    // 使用方法与push相似，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。
    ```

3. go方法

    ```
    //这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 window.history.go(n)
    // 在浏览器记录中前进一步，等同于 history.forward()
    router.go(1)
    
    // 后退一步记录，等同于 history.back()
    router.go(-1)
    
    // 前进 3 步记录
    router.go(3)
    
    // 如果 history 记录不够用，那就默默地失败呗
    router.go(-100)
    router.go(100)
    ```

4. back方法

    ```
    //回退一步
    router.back();
    ```

5. forward方法

    ```
    //前进一步
    router.forward();
    ```

6. getMatchedComponents方法

    ```
    返回目标位置或是当前路由匹配的组件数组 (是数组的定义/构造类，不是实例)。通常在服务端渲染的数据预加载时使用
    const matchedComponents: Array<Component> = router.getMatchedComponents(location?)
    ```

7. resolve方法

    ```
    const resolved: {
      location: Location;
      route: Route;
      href: string;
    } = router.resolve(location, current?, append?)
    /*
    解析目标位置 (格式和 <router-link> 的 to prop 一样)。
    
    current 是当前默认的路由 (通常你不需要改变它)
    append 允许你在 current 路由上附加路径 (如同 router-link)
    */
    ```

8. addRoute方法

    ```
    //添加一条新路由规则。如果该路由规则有 name，并且已经存在一个与之相同的名字，则会覆盖它
    addRoute(route: RouteConfig): () => void
    //添加一条新的路由规则记录作为现有路由的子路由。如果该路由规则有 name，并且已经存在一个与之相同的名字，则会覆盖它。
    addRoute(parentName: string, route: RouteConfig): () => void
    ```

9. getRoutes方法

    ```
    //获取所有活跃的路由记录列表
    getRoutes(): RouteRecord[]
    ```

10. onReady方法

    ```
    /*该方法把一个回调排队，在路由完成初始导航时调用，这意味着它可以解析所有的异步进入钩子和路由初始化相关联的异步组件。
    
    这可以有效确保服务端渲染时服务端和客户端输出的一致。
    
    第二个参数 errorCallback 只在 2.4+ 支持。它会在初始化路由解析运行出错 (比如解析一个异步组件失败) 时被调用。
    */
    router.onReady(callback, [errorCallback])
    ```

11. onError方法

     ```
     /*
     注册一个回调，该回调会在路由导航过程中出错时被调用。注意被调用的错误必须是下列情形中的一种：
     
     错误在一个路由守卫函数中被同步抛出；
     
     错误在一个路由守卫函数中通过调用 next(err) 的方式异步捕获并处理；
     
     渲染一个路由的过程中，需要尝试解析一个异步组件时发生错误。
     */
     router.onError(callback)
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
    
5. hash

    当前路由的hash值（带#），如果没有，则为空字符串

6. fullPath

    包含query、hash的完整路径

7. matched（Array）

    一个数组，包含当前路由的所有嵌套路径的路由记录（就是router配置中该路由的信息对象）

8. redirectedFrom

    如果存在路由重定向，即重定向来源的路由名字。

---
### 6. 导航守卫

有多种机会植入路由导航过程中：**全局**的, **单个路由独享**的, 或者**组件级**的。

【重要】**参数或查询的改变并不会触发进入/离开的导航守卫**。你可以通过[观察 `$route` 对象](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html#响应路由参数的变化)来应对这些变化，或使用 `beforeRouteUpdate` 的组件内守卫

1. 全局前置守卫

   使用 `router.beforeEach` 注册一个全局前置守卫：

   ```
   const router = new VueRouter({ ... })
   
   router.beforeEach((to, from, next) => {
     // ...
   })
   ```

   当一个导航触发时，全局前置守卫按照创建顺序调用.

   守卫是异步解析执行，**此时导航在所有守卫 resolve 完之前一直处于** **等待中**。

   每个守卫方法接收三个参数：

   - **`to: Route`**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)
   - **`from: Route`**: 当前导航正要离开的路由
   - **`next: Function`**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
     - **`next()`**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
     - **`next(false)`**: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
     - **`next('/')` 或者 `next({ path: '/' })`**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
     - **`next(error)`**: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。

2. 全局解析守卫

   用 `router.beforeResolve` 注册一个全局守卫。这和 `router.beforeEach` 类似，区别是在导航被确认之前，**同时在所有组件内守卫和异步路由组件被解析之后**，解析守卫就被调用。

3. 全局后置钩子

   注册全局后置钩子，然而和守卫不同的是，这些钩子不会接受 `next` 函数也不会改变导航本身：

   ```
   router.afterEach((to, from) => {
     // ...
   })
   ```

4. 路由独享的守卫

   在路由配置上直接定义 `beforeEnter` 守卫:

   ```
   const router = new VueRouter({
     routes: [
       {
         path: '/foo',
         component: Foo,
         beforeEnter: (to, from, next) => {
           // ...
         }
       }
     ]
   })
   ```

5. 组件内的守卫

   可以在路由组件内直接定义以下路由导航守卫：

   - `beforeRouteEnter`
   - `beforeRouteUpdate` (2.2 新增)
   - `beforeRouteLeave`

   ```
   const Foo = {
     template: `...`,
     beforeRouteEnter(to, from, next) {
       // 在渲染该组件的对应路由被 confirm 前调用
       // 不！能！获取组件实例 `this`
       // 因为当守卫执行前，组件实例还没被创建
       // 通过传一个回调给 next来访问组件实例
       // 只有beforeRouteEnter可以传回调
        next(vm => {
           // 通过 `vm` 访问组件实例
        })
     },
     beforeRouteUpdate(to, from, next) {
       // 在当前路由改变，但是该组件被复用时调用
       // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
       // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
       // 可以访问组件实例 `this`
     },
     beforeRouteLeave(to, from, next) {
       // 导航离开该组件的对应路由时调用
       // 可以访问组件实例 `this`
       // 可以通过 next(false) 来取消
     }
   }
   ```

---
### 7. 路由解析流程

1. 导航被触发。
2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫 (2.2+)。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫 (2.5+)。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 DOM 更新。
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。(此处可以获取数据，但是在next之前会停留在之前的页面)

---

### 8. keep-alive

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

###  9. 过度效果

`<router-view>` 是基本的动态组件，所以我们可以用 `<transition>` 组件给它添加一些过渡效果：

```
<transition>
  <router-view></router-view>
</transition>
```

可以基于当前路由与目标路由的变化关系，动态设置过渡效果:

```html
<!-- 使用动态的 transition name -->
<transition :name="transitionName">
  <router-view></router-view>
</transition>

// 接着在父组件内
// watch $route 决定使用哪种过渡
watch: {
  '$route' (to, from) {
    const toDepth = to.path.split('/').length
    const fromDepth = from.path.split('/').length
    this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
  }
}
```

---

### 10. 滚动行为

 **这个功能只在支持 `history.pushState` 的浏览器中可用**

使用前端路由，当切换到新路由时，想要页面滚到顶部，或者是保持原先的滚动位置，就像重新加载页面那样。

当创建一个 Router 实例，你可以提供一个 `scrollBehavior` 方法：

```js
const router = new VueRouter({
  routes: [...],
  scrollBehavior (to, from, savedPosition) {
    // return 期望滚动到哪个的位置
  }
})
```

`scrollBehavior` 方法接收 `to` 和 `from` 路由对象。第三个参数 `savedPosition` 当且仅当 `popstate` 导航 (通过浏览器的 前进/后退 按钮触发) 时才可用。

这个方法返回滚动位置的对象信息，长这样：

- `{ x: number, y: number }`
- `{ selector: string, offset? : { x: number, y: number }}` (offset 只在 2.6.0+ 支持)

如果返回一个 falsy (译者注：falsy 不是 `false`，[参考这里 (opens new window)](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy))的值，或者是一个空对象，那么不会发生滚动。

1. 异步滚动

   可以返回一个 Promise 来得出预期的位置描述：

   ```js
   scrollBehavior (to, from, savedPosition) {
     return new Promise((resolve, reject) => {
       setTimeout(() => {
         resolve({ x: 0, y: 0 })
       }, 500)
     })
   }
   ```

2. 平滑滚动

   只需将 `behavior` 选项添加到 `scrollBehavior` 内部返回的对象中，就可以为[支持它的浏览器 (opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/ScrollToOptions/behavior)启用原生平滑滚动：

   ```js
   scrollBehavior (to, from, savedPosition) {
     if (to.hash) {
       return {
         selector: to.hash,
         behavior: 'smooth',
       }
     }
   }
   ```

---

### 11. 导航故障

当使用 `router-link` 组件时，Vue Router 会自动调用 `router.push` 来触发一次导航。 虽然大多数链接的预期行为是将用户导航到一个新页面，但也有少数情况下用户将留在同一页面上：

- 用户已经位于他们正在尝试导航到的页面
- 一个[导航守卫](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)通过调用 `next(false)` 中断了这次导航
- 一个[导航守卫](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)抛出了一个错误，或者调用了 `next(new Error())`

当使用 `router-link` 组件时，**这些失败都不会打印出错误**。然而，如果你使用 `router.push` 或者 `router.replace` 的话，可能会在控制台看到一条 *"Uncaught (in promise) Error"* 这样的错误，后面跟着一条更具体的消息。让我们来了解一下如何区分*导航故障*。

**在 v3.2.0 中，可以通过使用 `router.push` 的两个可选的回调函数：`onComplete` 和 `onAbort` 来暴露*导航故障*。从版本 3.1.0 开始，`router.push` 和 `router.replace` 在没有提供 `onComplete`/`onAbort` 回调的情况下会返回一个 *Promise*。这个 *Promise* 的 resolve 和 reject 将分别用来代替 `onComplete` 和 `onAbort` 的调用**

1. 检测导航故障

   *导航故障*是一个 `Error` 实例，附带了一些额外的属性。要检查一个错误是否来自于路由器，可以使用 `isNavigationFailure` 函数：

   ```js
   import VueRouter from 'vue-router'
   const { isNavigationFailure, NavigationFailureType } = VueRouter
   
   // 正在尝试访问 admin 页面
   router.push('/admin').catch(failure => {
     if (isNavigationFailure(failure, NavigationFailureType.redirected)) {
       // 向用户显示一个小通知
       showToast('Login in order to access the admin panel')
     }
   })
   ```

   提示

   如果你忽略第二个参数：`isNavigationFailure(failure)`，那么就只会检查这个错误是不是一个*导航故障*。

2. NavigationFailureType

   `NavigationFailureType` 可以帮助开发者来区分不同类型的*导航故障*。有四种不同的类型：

   - `redirected`：在导航守卫中调用了 `next(newLocation)` 重定向到了其他地方。
   - `aborted`：在导航守卫中调用了 `next(false)` 中断了本次导航。
   - `cancelled`：在当前导航还没有完成之前又有了一个新的导航。比如，在等待导航守卫的过程中又调用了 `router.push`。
   - `duplicated`：导航被阻止，因为我们已经在目标位置了

3. 导航故障的属性

   所有的导航故障都会有 `to` 和 `from` 属性，分别用来表达这次失败的导航的目标位置和当前位置。

   ```js
   // 正在尝试访问 admin 页面
   router.push('/admin').catch(failure => {
     if (isNavigationFailure(failure, NavigationFailureType.redirected)) {
       failure.to.path // '/admin'
       failure.from.path // '/'
     }
   })
   ```

   在所有情况下，`to` 和 `from` 都是规范化的路由位置

---

### 12. 后端history模式配置

#### Apache

```text
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

除了 `mod_rewrite`，你也可以使用 [`FallbackResource`](https://httpd.apache.org/docs/2.2/mod/mod_dir.html#fallbackresource)。

#### nginx

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

#### 原生 Node.js

```js
const http = require('http')
const fs = require('fs')
const httpPort = 80

http.createServer((req, res) => {
  fs.readFile('index.html', 'utf-8', (err, content) => {
    if (err) {
      console.log('We cannot open "index.html" file.')
    }

    res.writeHead(200, {
      'Content-Type': 'text/html; charset=utf-8'
    })

    res.end(content)
  })
}).listen(httpPort, () => {
  console.log('Server listening on: http://localhost:%s', httpPort)
})
```

#### 基于 Node.js 的 Express

对于 Node.js/Express，请考虑使用 [connect-history-api-fallback 中间件](https://github.com/bripkens/connect-history-api-fallback)




---

#### [返回目录](./)
