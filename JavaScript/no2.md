## JavaScript学习笔记 变量与数据类型
## 1. 变量

ECMAScript的变量是松散类型的，可以保存任何类型的数据。每一个变量仅仅只是一个用于保存值的占位符。

定义变量的三种方式：

### 1. var关键字

使用 var 操作符(注意 var 是一个关键字)，后跟变量名：

```
var message;
```

1. **var** 声明作用域

    var 操作符定义的变量会成为**包含它的函数**的局部变量，**不过，在函数内定义变量时省 略 var 操作符，可以创建一个全局变量**

   ```
   function test() {
   	message = "hi"; // 全局变量,不推荐这么做
   }
   test();
   console.log(message); // "hi"
   ```

2.  **var** 声明提升

   使用var关键字声明的变量会自动提升到函数作用域顶部:

   ```
   function foo() {
     console.log(age);
     var age = 26;
   }
   foo();  // undefined
   //虽然变量提升了，但是赋值任然是在后面赋值的，所以输出undefined
   //反复多次使用 var 声明同一个变量也没有问题
   
   ```

3. 全局声明

   var 声 明的变量会成为 window 对象的属性

### 2. let关键字

 let 声明的范围是**块作用域**， 而 var 声明的范围是函数作用域；

1. 暂时性死区

   let 与 var 的另一个重要的区别，就是 let 声明的变量不会在作用域中被提升；**在 let 声明之前的执行瞬间被称为“暂时性死区”(temporal dead zone)**，在此 阶段引用任何后面才声明的变量都会抛出 `ReferenceError`。

2. 全局声明

    let 在全局作用域中声明的变量  **不会**  成为 window 对象的属性

3. **for** 循环中的 **let** 声明

   使用 let 之后，迭代变量的作用域仅限于 for 循环块内部。

   **使用 let 声明迭代变量时，JavaScript 引擎在后台会为每个迭代循环声明一个新的迭代变量，每个 setTimeout 引用的都是不同的变量实例**

   ```
    for (let i = 0; i < 5; ++i) {
           setTimeout(() => console.log(i), 0)
   }
   // 会输出0、1、2、3、4
   ```

   这种每次迭代声明一个独立变量实例的行为适用于所有风格的 for 循环，包括 for-in 和 for-of 循环;

### 3. const关键字

const 的行为与 let 基本相同，唯一一个重要的区别是用它声明变量时必须同时初始化变量，且 尝试修改 const 声明的变量会导致运行时错误。

```
const age = 26;
age = 36; // TypeError: 给常量赋值
```

不能用 const 来声明迭代变量:

```
for (const i = 0; i < 10; ++i) {} // TypeError:给常量赋值
```

用 const 声明一个不会被修改的 for 循环变量，每次迭代只是创建一个新变量。这对 for-of 和 for-in 循环特别有意义:

```
for (const key in {a: 1, b: 2}) {
	console.log(key);
}
// a, b
for (const value of [1,2,3,4,5]) {
	console.log(value);
}
// 1, 2, 3, 4, 5
```



## 2. 数据类型

&emsp;&emsp;ECMAScript有6种基本数据类型：`Undefined` , `Null` , `Boolean` , `Number` , `String` , ` Symbol`。还有1种复杂数据类型（引用类型）：`Object`。所有值都是这6种数据类型其中之一。

&emsp;&emsp;可以使用 `typeof` 操作符来检测变量的数据类型。对一个值使用 `typeof` 操作符可以返回以下字符串之一（操作符后可用括号，但不是必须，返回的字符串和上述数据类型不一定一样）：
+ "undefined"：未定义
+ "boolean"：布尔值
+ "string"：字符串
+ "number"：数值
+ "object": 对象或者**null**
+ "function"：函数
+ "symbol"：表示值为符号。

&emsp;&emsp;以下对各个类型进行说明：

### 1. **Undefined 类型 ** 

Undefined类型只有一个值就是：`undefined`，**未初始化的变量默认值为它**。主要用于比较一个变量是不是该值。**最好使用 `typeof` 操作符（未定义的变量使用会报错，但是对未定义的变量执行 typeof操作返回undefined）**。undefined 是一个假值。

### 2. **Null 类型**  

Null类型也只有一个值就是：`null`，但是在**使用 `typeof` 操作符的时候会返回 "object" 字符串**。需要注意，所以在一个变量将来要用做保存对象的时候，可以先给这个变量初始化为 `null` 值，这样检测的时候就知道是对象变量了。**`undefined` 值派生自 `null`，但是用途不同**。null 是一个假值。

### 3. Boolean 类型  

Boolean类型只有两个值：`true` 和 `false`。需要注意的是：这两个值与数字 `1` 和 `0` 不相等，但是可以使用**转型函数 `Boolean()`**将其他类型转换到对应的布尔值，在某些需要编程 `Boolean` 类型的情况中会被自动转换。下面是转换规则：

| 数据类型 | true | false |
| :------ | :---- | :---- |
| String | 非空字符串 | "" |
| Number | 非零数值 | 0和NaN |
| Object | 任何对象 | null |
| Undefined | (没有真值) | undefined |

### 4. Number 类型  

Number类型使用IEEE754格式来表示整数和浮点数。  

1. 对于整数数值字面量，整数**八进制**第一位必须是零 `0` ，整数**十六进制**前两位必须是零x `0x` 。如果八进制后面的数值超出了进制范围，就被当做10进制数。
2. 对于浮点数字面量，如果是一个整数大小，那么就解析为整数，而不是以浮点数的形式，最高精度为17位小数。可以使用科学计数法，用一个大写或者小写的E在中间表示乘10的n次方。
3. 特殊值列表：
    | 特殊值 | 含义 |
    | :---- | :---- |
    | Number.MIN_VALUE | 最小数值（一般为 5e-324） |
    | Number.MAX_VALUE | 最大数值（一般为 1.7976931348623157e+308） |
    | Infinity | 无穷大（超出上述范围。**它不能参与运算**） |
    | Number.NEGATIVE_INFINITY | 正无穷大 |
    | Number.POSITIVE_INFINITY | 负无穷大 |
    | NaN | 非数值（无法返回或转换成数值，如数值除以0，且它参与运算返回NaN） |
    可以使用 `isFinite()` 方法判断一个数值是否在规定范围内（是否有限大），在就返回 `true` ，否则返回 `false` 。  
    `NaN` 不与任何值相等，只能通过 `isNaN()` 方法来判断。
4. **转型函数**
   
    + **Number()  **
        用于任何类型。规则如下：
        + Boolean类型，true和false对应1和0
        + null值，转换为0
        + undefined值，转换为NaN
        + String类型，又需要以下规则：
            + 只包含数字和小数点，转换为十进制数值
            + 只包含有效十六进制格式，转换成对应的数值
            + 空串""，转换为0
            + 其他格式 ( 只要有非上述3钟的字符 )，转换为NaN
        + Object类型，调用对象的 `valueOf()` 方法，然后对返回值按上述方法进行转换，如果结果是 `NaN` ,则再调用对象的 `toString()` 方法，再对返回值按上述方法进行转换。
    + **parseInt() ** 
        只用于字符串。忽略字符串的前导空格，直到第一个非空格字符。如果第一个字符不是数字或负号，则返回 `NaN` ，如果是着继续解析，直到不是为止。  
        对于非十进制格式，可以使用 `parseInt(String str,Number decimal)` 方法，第一个参数还是字符串，第二个参数是表示进制的数值。
    + **parseFloat()**  
        只用于字符串。规则与 `parseInt()` 基本相同，对于不包含小数的会返回整数，但是该方法**只支持十进制**，所以对于十进制转换可以统一使用该方法。
    + **注意：还可以使用一元运算符 `+` 来用做与 `Number()` 相同的功能**

### 5. String 类型  

String类型用于表示Unicode字符组成的字符序列，既可以使用单引号 `'` ，也可以使用双引号 `"` 包裹字符序列。  
对于转型函数有两种：

1. **数值、布尔值、对象和字符串**的 `toString()` 方法  
    会返回一个字符串副本，如果是**数值，可以指定一个数值参数，该参数指明进制的数值**。
    
2. String()  
    它的转换规则如下：
    
    + 如果有 `toString()` 方法，调用它
    + 如果是 `null` 值，则返回 `"null"`
    + 如果是 `undefined` 值，则返回 `"undefined"`
    
3. **注意：可以使用链接字符串运算符 `+` 将其与空串 `""` 链接，效果与 `String()` 相同**

4. **模板字面量（ES6）**：

    ECMAScript 6 新增了使用模板字面量定义字符串的能力(使用反引号)。与使用单引号或双引号不同，模板字面量 保留换行字符，可以跨行定义字符串:

    ```
     let myMultiLineTemplateLiteral = `first line
        second line`;
    ```

    **1.字符串插值：**

    模板字面量在定义时**立即求值并转换为字符串**实例，任何插入的变量也会从它们最接近的作 用域中取值。

    **字符串插值通过在${}中使用一个 JavaScript 表达式实现**

    ```
    // 现在，可以用模板字面量这样实现: 12 
    let interpolatedTemplateLiteral = `${ value } to the ${ exponent } power is ${ value * value }`;
    ```

    **2.标签函数：**

    模板字面量也支持定义标签函数(tag function)，而通过标签函数可以自定义插值行为。标签函数 会接收被插值记号分隔后的模板和对每个表达式求值的结果。

    标签函数本身是一个常规函数，通过前缀到模板字面量来应用自定义行为，如下例所示。标签函数 接收到的参数依次是**原始字符串数组**和对**每个表达式求值的结果**。这个函数的返回值是对模板字面量求 值得到的字符串。

    ```
    let a = 6;
    let b = 9;
    function simpleTag(strings, aValExpression, bValExpression, sumExpression) { 
    	console.log(strings);
    	console.log(aValExpression);
    	console.log(bValExpression);
      console.log(sumExpression);
      return 'foobar';
    }
    let untaggedResult = `${ a } + ${ b } = ${ a + b }`;
    let taggedResult = simpleTag`${ a } + ${ b } = ${ a + b }`;
    // ["", " + ", " = ", ""]
    // 6
    // 9
    // 15
    console.log(untaggedResult);
    console.log(taggedResult);
    // "6 + 9 = 15"
    // "foobar"
    ```

    通常应该使用剩余操作符(rest operator)将它们收集到一个 数组。

    ```
    let a = 6;
    let b = 9;
    function simpleTag(strings, ...expressions) {
      console.log(strings);
      for(const expression of expressions) {
        console.log(expression);
      }
      return 'foobar';
    }
    let taggedResult = simpleTag`${ a } + ${ b } = ${ a + b }`;
    // ["", " + ", " = ", ""]
    // 6
    // 9
    // 15
    console.log(taggedResult);  // "foobar"
    ```

    **3. 原始字符串**：

    直接获取原始的模板字面量内容(如换行符或 Unicode 字符)，而不是被转 换后的字符表示：

    ```
    console.log(`\u00A9`); // ©
    console.log(String.raw`\u00A9`); // \u00A9
    ```

    也可以通过标签函数的第一个参数，即字符串数组的.raw 属性取得每个字符串的原始内容:

    ```
    function printRaw(strings) {
          console.log('Actual characters:');
          for (const string of strings) {
            console.log(string);
          }
          console.log('Escaped characters;');
          for (const rawString of strings.raw) {
            console.log(rawString);
          }
    }
    printRaw`\u00A9${ 'and' }\n`; 
    // Actual characters:
    // ©
    //(换行符)
    // Escaped characters:
    // \u00A9
    // \n
    ```

### 6. **Symbol**类型(ES6)

Symbol(符号)是 ECMAScript 6 新增的数据类型。符号是原始值，且符号实例是唯一、不可变的。

**符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险**

用法：

1. 基本用法：

   使用 Symbol()函数初始化symbol类型：

   ```
   let sym = Symbol();
   console.log(typeof sym); // symbol
   ```

   也可以传入一个字符串参数作为对符号的描述(description),但是，这个字符串参数与符号定义或标识完全无关:

   ```
   let fooSymbol = Symbol('foo');
   let otherFooSymbol = Symbol('foo');
   console.log(genericSymbol == otherGenericSymbol);  // false
   ```

   **最重要的是，Symbol()函数不能与 new 关键字一起作为构造函数使用。这样做是为了避免创建符 号包装对象**:

   ```
   let mySymbol = new Symbol(); // TypeError: Symbol is not a constructor
   ```

2. 使用全局符号注册表

   运行时的不同部分需要**共享和重用符号实例**，那么可以用**一个字符串作为键**，在全局符号注册 表中**创建并重用符号**

   ```
   let fooGlobalSymbol = Symbol.for('foo');
   console.log(typeof fooGlobalSymbol); // symbol
   ```

   Symbol.for()对每个字符串键都执行幂等操作。第一次使用某个字符串调用时，它会检查全局运 行时注册表，发现不存在对应的符号，于是就会生成一个新符号实例并添加到注册表中。后续使用相同 字符串的调用同样会检查注册表，发现存在与该字符串对应的符号，然后就会返回该符号实例。

   **还可以使用 Symbol.keyFor()来查询全局注册表，这个方法接收符号，返回该全局符号对应的字 符串键。如果查询的不是全局符号，则返回 undefined。**

   ```
   // 创建全局符号
   let s = Symbol.for('foo'); console.log(Symbol.keyFor(s)); // foo
   ```

3. 使用符号作为属性

   凡是可以使用字符串或数值作为属性的地方，都可以使用符号。包括了对象**字面量属性**和 `Object.defineProperty()` / `Object.defineProperties()` 定义的属性：

   ```
   let s1 = Symbol('foo'),
       s2 = Symbol('bar'),
       s3 = Symbol('baz'),
       s4 = Symbol('qux');
       
   let o = {
         [s1]: 'foo val'
   };
   // 这样也可以:o[s1] = 'foo val';
   Object.defineProperty(o, s2, {value: 'bar val'});
   Object.defineProperties(o, {
         [s3]: {value: 'baz val'},
         [s4]: {value: 'qux val'}
   });
   ```

   类似于` Object.getOwnPropertyNames()`返回对象实例的常规属性数组，`Object.getOwnPropertySymbols()`返回对象实例的符号属性数组。这两个方法的返回值彼此互斥。`Object.getOwnPropertyDescriptors()`会返回同时包含常规和符号属性描述符的对象。`Reflect.ownKeys()`会返回两种类型 的键。

4. 常用内置符号：见《JavaScript高级程序设计 第四版》 p47

   **注意 在提到ECMAScript规范时，经常会引用符号在规范中的名称，前缀为@@。比如， @@iterator 指的就是 Symbol.iterator。**

### 7. Object 类型  

对象就是一组数据和功能的集合，可以创建 `Object` 类型的实例并添加属性和方法，就可以创建自定义对象。

```
let o = new Object();
```

Object的 **每个实例** 都具有下列属性和方法：

+ constructor  
    指向构造函数。
+ hasOwnProperty(String propertyName)  
    检查给定的属性名是否存在当前对象实例中。
+ isPrototypeOf(Object object)  
    检查对象是否是传入实例的原型。
+ propertyIsEnumerable(String propertyName)  
    检查给定的属性名是否能够使用 `for-in` 语句来枚举。
+ toLocaleString()  
    返回对象的当地字符串表示。
+ toString()  
    返回对象的字符串表示。
+ valueOf()  
    返回对象的字符串、数值或布尔值表示。



---

#### [返回目录](./)