## Vue全家桶学习笔记 Vuex
---
### 1. 介绍  

Vuex 是一个专为 Vue.js 应用程序开发的***状态管理模式***。它采用***集中式存储***管理应用的所有组件的状态，并以相应的规则保证以一种可预测的方式发生变化。

Vuex状态管理图例：
![Vuex](./image/vuex.png)

每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的**状态 (state)**。Vuex 和单纯的全局对象有以下两点不同：

1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用

---
### 2. 基本使用 

1. 创建并导出store  

    ```
    import Vue from 'vue'
    import Vuex from 'vuex'

    // 1.安装插件
    Vue.use(Vuex)

    // 2.创建状态对象
    const state = {
        counter: 1000,
        students: [
            {id: 110, name: 'why', age: 18},
            {id: 111, name: 'kobe', age: 24},
            {id: 112, name: 'james', age: 30},
            {id: 113, name: 'curry', age: 10}
        ],
        info: {
            name: 'kobe',
            age: 40,
            height: 1.98
        }
    }

    //创建vuex存储对象
    const store = new Vuex.Store({
        state,
        mutations:{
        },
        actions:{
        },
        getters:{
        },
        modules: {
        }
    })

    // 3.导出store
    export default store
    ```

2. 在Vue中挂载：

    ```
    new Vue({
      store,
      render: h => h(App)
    }).$mount('#app')
    ```
    
3. 使用状态

    ```
    通过this.$store.state.属性的方式来访问状态
    ```

---
### 3. State

就是保存全局状态信息的地方。可以通过`this.$store.state.属性`的方式进行访问。

+ Vuex的store中的state是响应式的

#### 3.1 mapState 辅助函数

当一个组件需要获取多个状态的时候，将这些状态都声明为计算属性会有些重复和冗余。为了解决这个问题，我们可以使用 `mapState` 辅助函数帮助我们生成计算属性，让你少按几次键：

```
import { mapState } from 'vuex'

export default {
  // ...
  computed: {
    localComputed() {
      /* ... */
    },
    // 使用对象展开运算符将此对象混入到外部对象中
    ...mapState({
      // ...
      count: state => state.count,
      //或者用字符串
      // 传字符串参数 'count' 等同于 `state => state.count`
      countAlias: 'count',
      //或者写函数
      // 为了能够使用 `this` 获取局部状态，必须使用常规函数
      countPlusLocalState(state) {
        return state.count + this.localCount
      }
    }),
    //也可以使用数组
    ...mapState([
      // 映射 this.count 为 store.state.count
      'count'
    ])
  }
}

```



---
### 4. Getters  

有时候我们需要从 store 中的 state 中派生出一些状态，如果有多个组件需要用到此属性，我们要么复制这个函数，或者抽取到一个共享函数然后在多处导入它——无论哪种方式都不是很理想。不同地方都需要需要从store中获取一些state变异后的状态，可以使用Getters，与计算属性类似。

1. 定义getters 

    Getter接受 state 作为其第一个参数，也接受 getter 作为第二个参数

    ```
    getters:{
        powerCounter(state) {
            return state.counter * state.counter
        },
        //第二参数为getters
        powerCounterAdd1(state, getters) {
            return getters.powerCounter+1
        }
    },
    ```

2. 使用getters

    ```
    this.$store.getters.powerCounter
    
    {{$store.getters.powerCounterAdd1}}
    ```

#### 4.1 mapGetters  辅助函数

与mapState一样的使用方式

```
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```



---
### 5. Mutation 

Vuex的store状态的更新唯一方式：***提交Mutation***。

+ 不要在Mutation方法内执行异步操作，应当在Action中执行异步，再调用commit执行Mutation方法。

1. 定义Mutation方法

    state作为第一个参数，第二个是参数为载荷

    ```
    mutations:{
        decrement(state) {
            state.counter--
        },
        //负载用来携带参数
        incrementCount(state, payload) {
            state.counter += payload.count
        }
    },
    ```

2. 使用Mutation

    ```
    //1. 携带的第二参数就是payload
    this.$store.commit('incrementCount',2);
    
    //2. 整个对象（带type）作为payload传入
    this.$store.commit({
        type: 'incrementCount',
        count: 100
    })
    ```

#### 5.1 mapMutations 辅助函数

与mapState和mapGetters类似，不过是在methods里面：

```
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' 
      // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```



---
### 6. Action

Action类似于Mutation, 但是是用来代替Mutation进行***异步操作***的。

1. 定义Action方法

    第一个参数为context（和store对象具有相同方法和属性，不同于store，在多模块情况下，context代表当前模块）

    第二个参数这是载荷

    ```
    actions:{
        //context是和store对象具有相同方法和属性的对象。但是在多模块情况下，context代表当前模块
        incrementAsync(context, payload) {
            new Promise((resolve, reject) => {
                /*异步操作*/
                if(/*结果正确*/)
                    resolve(/*结果*/)
                else
                    reject("错误信息")
            })
            .then(res=>{
            	//提交
            	context.commit("increase",res);
            })
        },
        //action也可以返回一个Promise
        increment2Async(context, payload) {
            return new Promise((resolve, reject) => {
                /*异步操作*/
                if(/*结果正确*/)
                    resolve(/*结果*/)
                else
                    reject("错误信息")
            });
        }
    }
    ```

2. 使用Action

    ```
    // 携带的第二参数就是payload
    this.$store.dispatch('incrementAsync', {
        amount: 10
    })
    
    // 整个对象作为payload
    this.$store.dispatch({
        type: 'incrementAsync',
        amount: 10
    })
    ```

#### 6.1 mapActions 辅助函数

与mapMutations相似

---
### 7. Module

当应用变得非常复杂时,store对象就有可能变得相当臃肿.为了解决这个问题, Vuex允许我们**将store分割成模块(Module)**, 而每个模块拥有自己的state、mutation、action、getters等。

1. 定义模块

    ```
    modules: {
        //定义模块a
        a: {
            //如果需要开启命名空间，所有访问字符串变成"a/对应的方法名称"
            namespaced: true,
            state:()=>({
            	count:1
            })
            mutations:{
            },
            actions:{
            },
            getters:{
            },
            modules: {
            }
        }
    }
    ```

2. 使用模块 

    + state 

        ```
        this.$store.state.a.属性
        ```
    + mutation\getter\action  

        默认情况下，模块内部的 action、mutation 和 getter 是注册在**全局命名空间**的——这样使得**多个模块**能够对**同一** mutation 或 action 作出响应。

        你可以通过添加 `namespaced: true` 的方式使其成为带命名空间的模块

        ```
        //没有添加namespaced
        this.$store.commit(...)
        this.$store.dispatch(...)
        this.$store.getters.某一个getter
        
        //添加了namespaced
        this.$store.commit('a/...',...)
        this.$store.dispatch('a/...',..)
        this.$store.getters['a/...',..]
        
        ```

---

#### [返回目录](./)
