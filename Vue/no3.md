## Vue全家桶学习笔记 Vue组件
---
### 1. 基本使用

1. 模板的写法
    + script写法  
        ```
        <script type="text/x-template" id="xxx">
        
        </script>
        ```
    + template写法  
        ```
        <template id="xxx">
        
        </template>
        ```

2. 注册组件  
    + 全局注册      
        ```
        Vue.component('name',{
            template:'xxx',
            ......
        })
        ```
    + 局部注册  
        ```
        new Vue({
            ......
            components:{
                'name':{
                   template:'xxx',
                   ...... 
                }
            }
            ......
        })
        ```

3. 组件的data  
    + 组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)
    + 只是这个data属性必须是一个函数
    + 而且这个函数返回一个对象，对象内部保存着数据
    ```
    components:{
        'name':{
            template:'xxx',
            data(){
                return {
                    ......
                }
            } 
        }
    }
    ```

---
### 2. 父子组件通信  

![props和emit](./image/propsemit.png)

1. 父组件向子组件传递参数（props）
    + 方式一：字符串数组，数组中的字符串就是传递时的名称。
        ```
        components:{
            'name':{
                template:'xxx',
                props:['aaa','bbb']
            }
        }
        
        <name :aaa="" :bbb=""></name>
        ```
    + 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。
        ```
        components:{
            'name':{
                template:'xxx',
                props:{
                    aaa:类型,
                    bbb:[类型1,类型2,...],
                    ccc:{
                        type:类型,
                        required:true|false,
                        defalut:默认值|（对象和数组类型的props默认值必须是一个函数）
                    },
                    ddd:{
                        //自定义验证
                        validator:function(value){
                            return true|false;
                        }
                    }
                }
            }
        }
        ```
2. 子组件向父组件传递事件（$emit）  
    + 在子组件函数中，调用`this.&emit('事件名',参数...)`，发送一个自定义事件。
    + 在父组件中，通过v-on来监听子组件事件。

---
### 3. 父子组件访问 

1. 父组件访问子组件（$children,$refs）

    + $children：数组类型，它包含所有子组件对象。
    + $resfs：
        + $refs和ref指令通常是一起使用的。
        + 首先，我们通过ref给某一个子组件绑定一个特定的ID。
        + 其次，通过this.$refs.ID就可以访问到该组件了。
        ```
        <name ref="xx"></name>
        
        new Vue({
            ......
            methods:{
                test(){
                    this.$refs.xx;
                }
            }
            ......
        })
        ```
2. 子组件访问父组件（$parent）  
    尽管在Vue开发中，我们允许通过$parent来访问父组件，但是在真实开发中尽量不要这样做。

---
### 4. 插槽（slot）  
预留一个位置给使用组件时，自定义html代码。
1. 基本用法   
    + `<slot>`中的内容表示，如果没有在该组件中插入任何其他内容，就默认显示该内容
    ```
    <template id="xx">
        <slot>...默认内容...</slot>
    </template>
    
    <name>
        <h1>我是插槽内容</h1>
    </name>
    ```
2. 带名字的插槽  
    + 给slot元素一个name属性，再使用的时候，在需要替换的html标签上加上`slot`属性，指明替换的slot。
    ```
    <template id="xx">
        <slot name="a">...默认内容...</slot>
        <slot name="b">...默认内容...</slot>
    </template>
    
    <name>
        <h1 slot="a">我是插槽内容</h1>
    </name>
    ```

3. 作用域插槽   
    + 传入插槽的html要遍历，访问组件中的数据
    + 在插槽上绑定一个`自定义属性`，暴露给外部
        ```
        <template id="xx">
            <slot :data="mydata" :data2="mydata2">...默认内容...</slot>
        </template>
        ```
    + 在插入html时，使用`<template slot-scope="对象名称">`来把插槽暴露的属性绑定到`对象名称`对象中。
        ```
        <name>
            <template slot-scope="slotObj">
                <span v-for="item in slotObj.data1">{{item}}</span>
            </template>
        </name>
        ```

---

#### [返回目录](./)
