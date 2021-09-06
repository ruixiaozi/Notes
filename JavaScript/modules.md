## JavaScript学习笔记 JS模块化

### 1. UMD

UMD 叫做通用模块定义规范（Universal Module Definition）。也是随着大前端的趋势所诞生，它可以通过运行时或者编译时让同一个代码模块在使用 CommonJs、CMD 甚至是 AMD 的项目中运行。未来同一个 JavaScript 包运行在浏览器端、服务区端甚至是 APP 端都只需要遵守同一个写法就行了。

它没有自己专有的规范，是集结了 CommonJs、CMD、AMD 的规范于一身，我们看看它的具体实例：

```
((root, factory) => {
    if (typeof define === 'function' && define.amd) {
        //AMD
        define(['jquery'], factory);
    } else if (typeof exports === 'object') {
        //CommonJS
        var $ = requie('jquery');
        module.exports = factory($);
    } else {
        root.testModule = factory(root.jQuery);
    }
})(this, ($) => {
    //todo
});
```

不难发现，它在定义模块的时候回检测当前使用环境和模块的定义方式，将各种模块化定义方式转化为同样一种写法。

### 2. CommonJS

CommonJs 是一种 JavaScript 语言的模块化规范，它通常会在服务端的 Nodejs 上使用。项目是由多个模块组成的，模块和模块之间的调用，需要各个模块有相同规范的 API，这样一来在使用的过程中不会有那么多的学习成本，并且对于单个模块来说是类聚的。

在 CommonJs 的模块化规范中，每一个文件就是一个模块，拥有自己独立的作用域、变量、以及方法等，对其他的模块都不可见。CommonJS规范规定，每个模块内部，module 变量代表当前模块。这个变量是一个对象，它的 exports 属性（module.exports）是对外的接口。加载某个模块，其实是加载该模块的 module.exports 属性。require 方法用于加载模块。

```
//moudle-a.js
moudle.exports = {
    a: 1
};

//moudle-b.js
var ma = require('./moudle-a');
var b = ma.a + 2;
module.exports ={
    b: b
};
```

**为了方便，Node为每个模块提供一个exports变量，指向module.exports**【exports就是一个别名】。这等同在每个模块头部，有一行这样的命令。

```
var exports = module.exports;
```

于是我们可以直接在 exports 对象上添加方法，表示对外输出的接口，如同在module.exports上添加一样。

*注意*，因为 **Node 模块是通过 module.exports 导出**的，如果直接将exports变量指向一个值，就切断了exports与module.exports的联系，导致意外发生：

```
// a.js
exports = function a() {};

// b.js
const a = require('./a.js') // a 是一个空对象
```

### 3. CMD

CMD 叫做通用模块定义规范（Common Module Definiton），它是类似于 CommonJs模块化规范，但是运行于浏览器之上的，它是随着前端业务和架构的复杂度越来越高运用而生的，来自淘宝玉伯的 SeaJS 就是它的实现。

CMD 规范尽量保持简单，并与 CommonJS 的 Modules 规范保持了很大的兼容性。通过 CMD 规范书写的模块，可以很容易在 Node.js 中运行。在 CMD 规范中，一个模块就是一个文件。格式如下：

```
// moudle-a.js
define(function(require, exports, module) {

    module.exports = { 
        a: 1 
    };

});

// moudle-b.js
define(function(require, exports, module) {

    var ma = require('./moudle-a');
    var b = ma.a + 2;
    module.exports = { 
        b: b 
    };

});
```

CMD 规范拥有简单、异步加载脚本、友好的调试并且兼容 Nodejs，它的确在开发过程中给我们提供了较好的模块管理方式。

### 4. AMD

AMD 叫做异步模块定义规范（Asynchronous Module Definition），它是 CommonJs模块化规范的超集，但是运行于浏览器之上的。AMD 的特点就和它的名字一样，模块的加载过程是异步的，它大大的利用了浏览器的并发请求能力，让模块的依赖过程的阻塞变得更少了。requireJs 就是 AMD 模块化规范的实现。

AMD 作为一个规范，只需定义其语法 API，而不关心其实现。AMD 规范简单到只有一个 API，即 define 函数：

```
// moudle-a.js
define('moudleA', function() { 
    return {
        a: 1
    }
});

// moudle-b.js
define(['moudleA'], function(ma) {
    var b = ma.a + 2;

    return {
        b: b
    }
});
```

它看起来似乎和 CMD 差不多，不过在实现上还是有一定的差异，它们各有优缺点.

### 5. ES Module

**ES Module**把一个文件当作一个模块，每个模块有自己的独立作用域，那如何把每个模块联系起来呢？核心点就是模块的导入（import）与导出（export）。ES Module借助babel进行转换兼容。

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

