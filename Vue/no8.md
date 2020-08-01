## Vue全家桶学习笔记 Promise
---
### 1. 介绍

Promise是异步编程的一种解决方案。

+ 解决链式异步操作的嵌套写法
+ 解决并发异步操作
+ 将异步操作和结果处理分开

---
### 2. 基本使用 

```
new Promise((resolve,reject) => {
    /*异步操作*/
    if(/*结果正确*/)
        resolve(/*结果*/)
    else
        reject("错误信息")
}).then(data => {
    /*处理结果*/
}).catch(mes => {
    /*处理错误*/
})
```

---
### 3. 链式异步操作 

```
new Promise((resolve, reject) => {
    /*异步操作*/
    if(/*结果正确*/)
        resolve(/*结果*/)
    else
        reject("错误信息")
  }).then(res => {
    // 1.对结果进行第一次处理(通过new Promise的方式返回Promise)
    return new Promise((resolve, reject) => {
        /*异步操作*/
        if(/*结果正确*/)
            resolve(/*结果*/)
        else
            reject("错误信息")
    })
  }).then(res => {
    // 2.对结果进行第二次处理（通过Promise的全局方法返回Promise）
    return Promise.resolve(res + '222')
  }).then(res => {
    // 3.对结果进行第三次处理（直接返回，相当于2）
    return res + '333'
  }).then(res => {
    // 4.对结果进行第三次处理（throw相当于Promise.reject）
    if(/*出错*/)
        throw '错误信息'
    return res + '444'
  }).catch(err){
      /*处理错误信息*/
  }
```
---
### 4. 并发异步操作  

```
 Promise.all([
    new Promise((resolve, reject) => {
        /*异步操作1*/
        if(/*结果正确*/)
            resolve(/*结果*/)
        else
            reject("错误信息")
    }),
    new Promise((resolve, reject) => {
        /*异步操作2*/
        if(/*结果正确*/)
            resolve(/*结果*/)
        else
            reject("错误信息")
    })
  ]).then(results => {
      //results是一个数组,包含两次的结果
      console.log(results);
  })
```

---

#### [返回目录](./)
