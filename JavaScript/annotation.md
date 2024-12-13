## JavaScript学习笔记 注释规范

---

### 1. 什么是 JSDoc 

JSDoc 是一个根据 JavaScript 文件中注释信息，生成 JavaScript 应用程序或模块的API文档的工具。你可以使用 JSDoc 标记如：**命名空间**，**类**，**方法**，**方法参数**等。从而使开发者能够轻易地阅读代码，掌握代码定义的类和其属性和方法，从而降低维护成本，和提高开发效率。

### 2. JSDoc 注释规则

JSDoc注释一般应该放置在方法或函数声明之前，它必须以`/ **`开始，以便由JSDoc解析器识别。其他任何以 **/\*** ， **/\**\*** 或者超过3个星号的注释，都将被JSDoc解析器忽略。

范例：

```
/**
* Book类，代表一个书本.
* @constructor
* @param {string} title - 书本的标题.
* @param {string} author - 书本的作者.
*/
functionBook(title, author){
    this.title=title;
    this.author=author;
}
Book.prototype={
/**
* 获取书本的标题
* @returns {string|*} 返回当前的书本名称
*/

getTitle:function(){
    returnthis.title;   
},
/**
* 设置书本的页数
* @param pageNum {number} 页数
*/
setPageNum:function(pageNum){
   this.pageNum=pageNum;   
}
};

```

### 3. 常用注释标注

@file ：写在文件开头，用于描述当前文件
 @desc: 用于描述当前文件或者代码
 @author：当前文件的作者
 @copyright： 当前文件的版权信息
 @license 文件许可证
 @version 版本号
 @since 描述某个功能自哪个版本开始支持
 @see '另见'
 @todo 接下来准备做的事情
 @function/@func/@method 描述一个函数
 @param 描述参数信息
 @return 描述返回值
 @callback 描述回调函数

### 3. 所有标注

@abstract 标签 (同义词: @virtual 标签)
描述这个成员必须在继承的子类中实现（或重写）。
@access 标签
指定该成员的访问级别（私有 private，公共 public，或保护 protected）。
@alias 标签
标记成员有一个别名。
@async 标签
Indicate that a function is asynchronous.
@augments 标签 (同义词: @extends 标签)
指名这个子类继承至哪个父类，后面需要加父类名。
@author 标签
指定项目的作者。
@borrows 标签
指明这个对象使用另一个对象的某些东西。
@callback 标签
描述一个回调函数。
@class 标签 (同义词: @constructor 标签)
此函数旨在需要使用"new"关键字调用，即构造函数。
@classdesc 标签
用于为类提供一个描述，这样和构造函数的描述区分开来.
@constant 标签 (同义词: @const 标签)
指明这个对象是一个常量。
@constructs 标签
描述这个函数成员将成为类的构造函数。
@copyright 标签
描述一个文件的版权信息。
@default 标签 (同义词: @defaultvalue 标签)
描述默认值.
@deprecated 标签
标签指明一个标识在你代码中已经被弃用。
@description 标签 (同义词: @desc 标签)
描述一个标识符。
@enum 标签
描述一个相关属性的集合。
@event 标签
描述一个事件。
@example 标签
提供一个如何使用描述项的例子。
@exports 标签
标识一个由JavaScript模块导出的成员。
@external 标签 (同义词: @host 标签)
用来标识一个在当前包外部定义的类，命名空间，或模块。
@file 标签 (同义词: @fileoverview 标签, @overview 标签)
描述一个文件。
@fires 标签 (同义词: @emits 标签)
描述事件这个方法可能会触发。
@function 标签 (同义词: @func 标签, @method 标签)
描述一个函数或方法。
@generator 标签
Indicate that a function is a generator function.
@global 标签
指定一个在文档的标识是为全局性的标识。
@hideconstructor 标签
Indicate that the constructor should not be displayed.
@ignore 标签
忽略文档中的一个标识。
@implements 标签
指示一个标识实现一个接口
@inheritdoc 标签
指明这个标识应继承其父类的文档。
@inner 标签
描述一个内部对象。
@instance 标签
标明该标识符作为它父标识符的实例成员。
@interface 标签
使一个标识符作为其他标识符的一个实现接口。
@kind 标签
指明标识的类型
@lends 标签
将一个字面量对象的所有属性标记为某个标识符（类或模块）的成员。
@license 标签
标识你的代码采用何种软件许可协议。
@listens 标签
指示一个标识监听指定的事件。
@member 标签 (同义词: @var 标签)
记录一个成员。
@memberof 标签
标明这个标识属于哪个父级标识。
@mixes 标签
此对象混入了另一个对象中的所有成员。
@mixin 标签
记录一个mixin（混入）对象。
@module 标签
记录一个 JavaScript 模块。
@name 标签
记录一个对象的名称。
@namespace 标签
记录一个命名空间对象。
@override 标签
指明一个标识符覆盖其父类同名的标识符。
@package 标签
This symbol is meant to be package-private.
@param 标签 (同义词: @arg 标签, @argument 标签)
记录传递给一个函数的参数。
@private 标签
标记标识符为私有。
@property 标签 (同义词: @prop 标签)
记录一个对象的属性。
@protected 标签
标记标识符为受保护的。
@public 标签
标记为公开的。
@readonly 标签
标记一个标识符为只读。
@requires 标签
指示这个文件需要一个 JavaScript 模块。
@returns 标签 (同义词: @return 标签)
描述一个函数的返回值。
@see 标签
指明可以参考另一个标识符的说明文档，或者一个外部资源。
@since 标签
标签标明一个类，方法，或其它标识符是在哪个特定版本开始添加进来的。
@static 标签
记录一个静态成员。
@summary 标签
完整描述的一个简写版本。
@this 标签
指明this关键字的指向
@throws 标签 (同义词: @exception 标签)
说明可能会被抛出什么样的错误.
@todo 标签
记录要完成的任务。
@tutorial 标签
插入一个到包含教程文件的链接。
@type 标签
记录一个对象的类型。
@typedef 标签
描述自定义类型.
@variation 标签
区分具有相同名称的不同的对象。
@version 标签
指明被用于表示该项的版本。
@yields 标签 (同义词: @yield 标签)
Document the value yielded by a generator function.













---

#### [返回目录](./)