## Vue全家桶学习笔记 模块化
---
### 1. CommonJS 模块化

1. 导出  

    ```
    module.exports = {
        ...
    }
    ```

2. 导入  

    ```
    let { ... } = require('moduleA');
    ```

---
### 2. ES6 模块化

1. 导出  

    ```
    export { ... };
    export let a = '';
    export function(){

    }
    //export default在同一个模块中，不允许同时存在多个
    export default {

    }
    ```

2. 导入  

    + 需要在HTML代码中引入js文件，并且类型需要设置为module
        ```
        <script src="xx.js" type="module"></script>
        <script src="xx2.js" type="module"></script>
        ```
    + import指令用于导入模块中的内容
        ```
        import { ... } from "./xx.js";
        import * as XX from "./xx.js";
        ```



---

#### [返回目录](./)
