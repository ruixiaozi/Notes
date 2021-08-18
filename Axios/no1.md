## Axios学习笔记 基本使用

---

### 1. 介绍

+ 在浏览器中发送 XMLHttpRequests 请求
+ 在 node.js 中发送 http请求
+ 支持 Promise API
+ 拦截请求和响应
+ 转换请求和响应数据

---

### 2. 基本使用

```
import axios from 'axios'

//普通请求
axios({
    url:'http://www.ruixiaozi.com'
}).then(res => {
    /*处理结果*/  
}).catch(err => {
    /*处理错误*/
})

//并发请求
axios.all([
    axios(config),
    axios(config)
]).then(axios.spread((res1,res2) => {
    /*处理结果*/  
})).catch(err => {
    /*处理错误*/
})

//config为配置对象
axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
```

---

### 3. 常见的配置选项

1. 请求地址

   ```
   url: '/user'
   ```

2. 请求类型

   ```
   method: 'get'
   ```

3. 请根路径

   ```
   baseURL: 'http://www.mt.com/api'
   ```

4. 请求前的数据处理  

   ```
   transformRequest:[function(data){}]
   ```

5. 请求后的数据处理

   ```
   transformResponse: [function(data){}]
   ```

6. 自定义的请求头

   ```
   headers:{'x-Requested-With':'XMLHttpRequest'}
   ```

7. URL查询对象(query，只能是GET请求)

   ```
   params:{ id: 12 }
   ```

8. 查询对象序列化函数

   ```
   paramsSerializer: function(params){ }
   ```

9. request body（data，post请求）

   ```
   data: { key: 'aa'}
   ```

10. 超时设置

    ```
    timeout: 1000
    ```

11. 跨域是否带Cookie

    ```
    withCredentials: true
    ```

12. 自定义请求处理

    ```
    adapter: function(resolve, reject, config){}
    ```

13. http身份验证信息

    ```
    auth: { uname: '', pwd: '12'}
    ```

14. 响应的数据格式 json / blob /document /arraybuffer / text / stream

    ```
    responseType: 'json'
    ```

---

### 4. 全局默认配置

```
axios.defaults.配置名称 = 配置值
```

---

### 5. axios实例

1. 用途

   不同模块，某些请求配置可能会不太一样

2. 用法

   ```
   //其中的config作为该实例的默认配置
   const axiosIns = axios.creat(config)
   
   axiosIns({
       url:'http://www.ruixiaozi.com'
   }).then(res => {
       /*处理结果*/  
   }).catch(err => {
       /*处理错误*/
   })
   ```

---

### 6. 拦截器

可以给每个axios实例设置拦截器，拦截**请求**和**响应**，分别包含**成功**和**失败**两种状态的拦截。

+ 拦截器包含return则继续执行，不包含return或者return信息不争气停止执行

拦截器的作用：

+ 显示/关闭 请求中 动画效果
+ 在请求拦截中 检查/修改 请求参数信息
+ 在响应拦截中 过滤/初步处理 返回信息
+ 在拦截失败中 进行页面跳转/提示用户 等


1. 请求拦截

   ```
   axiosIns.interceptors.request.use(config => {
       //成功进行请求拦截
       return config
   },err => {
       //请求失败拦截
       return err
   })
   ```

2. 响应拦截

   ```
   axiosIns.interceptors.response.use(response => {
       //成功进行返回拦截
       return response
   },err => {
       //返回失败拦截
       return err
   })
   ```



---

#### [返回目录](./)