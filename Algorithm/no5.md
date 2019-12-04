## 算法学习笔记 语言特性与技巧
---

1. 位运算的妙用
    + 算术左移*2，算术右移/2
    + 与运算特性与应用
        特性：`a&1=a`,`a&0=0`,`a&a=a`
        应用：取值与1，清零与0，判断奇偶
    + 或运算特性与应用
        特性：`a|1=1`,`a|0=a`,`a|a=a`
        应用：设置或1，保持或0
    + 异或运算特性与应用
        特性：`a^1=~a`,`a^0=a`,`a^a=0`
        应用：交换值，加密解密，加减法
    + 判断奇偶性  
        `a&1==1?"奇数":"偶数"`
    + 交换两个数值
        ```
        a^=b; //解释：a=a^b;
        b^=a; //解释：b=b^a=b^a^b=a^0=a;
        a^=b; //解释：a=a^b=a^b^b=a^b^a=b;
        //同上
        a^=b^=a^=b;
        ```
    + 实现加减法
        ```
        //（1）0+0=0；
        //（2）1+0=1；
        //（3）0+1=1；
        //（4）1+1=0；需要进位
        //加法A+B=A^B+(A&B)<<1;
        //减法A-B=A+(-B)=A+(~B+1);
        ```
    + 实现加密解密
        ```
        //明文为a，密钥为b
        //加密
        //c=a^b;
        //解密
        //d=c^b=a^b^b=a;
        ```

2. 浮点数转整形的四舍五入法  
    浮点运算可能存在细微的误差，当转换成整形的时候，默认舍弃法，但是误差可能导致数值变小或者变大一点，使用四舍五入法，可以避免这种情况的产生。
    ```
    floor(x+0.5);//存在0.5也可能被舍弃的问题
    ```

3. 关于基本数据类型及其大小  
    整形相关定义在stdint.h头文件中，如果不支持c99可以自己编写：
    ```
    #ifndef _STDINT_H
    #define _STDINT_H

    // Define C99 equivalent types.
    typedef signed char          int8_t;
    typedef signed short         int16_t;
    typedef signed int           int32_t;
    typedef signed long long     int64_t;

    typedef unsigned char        uint8_t;
    typedef unsigned short       uint16_t;
    typedef unsigned int         uint32_t;
    typedef unsigned long long   uint64_t;

    typedef unsigned char        byte;
    typedef unsigned short       word;
    typedef unsigned int         dword;
    typedef unsigned long long   qword;

    typedef enum 
    {
        FALSE = 0,
        TRUE  = 1,
    } bool；

    #define INT8_MIN (-128) 
    #define INT16_MIN (-32768)
    #define INT32_MIN (-2147483647 - 1)
    #define INT64_MIN  (-9223372036854775807LL - 1)

    #define INT8_MAX 127
    #define INT16_MAX 32767
    #define INT32_MAX 2147483647
    #define INT64_MAX 9223372036854775807LL

    #define UINT8_MAX 0xff /* 255U */
    #define UINT16_MAX 0xffff /* 65535U */
    #define UINT32_MAX 0xffffffff  /* 4294967295U */
    #define UINT64_MAX 0xffffffffffffffffULL /* 18446744073709551615ULL */

    #endif  //_STDINT_H
    ```
    浮点型定义在 float.h 中，可以引入后查看。

4. C语言输入输出格式：
    + 输入scanf：
        ```
        其控制串由三类字符构成：
        1.格式化说明符；
        2.空白符；
        3.非空白符；
        一、格式化说明符
        格式字符           说明
        %a                 读入一个浮点值(仅C99有效) 
        %A                 同上
        %c                 读入一个字符
        %d                 读入十进制整数
        %i                 读入十进制，八进制，十六进制整数
        %o                 读入八进制整数
        %x                 读入十六进制整数
        %X                 同上
        %c                 读入一个字符
        %s                 读入一个字符串
        %f                 读入一个浮点数
        %F                 同上
        %e                 同上
        %E                 同上
        %g                 同上
        %G                 同上
        %p                 读入一个指针
        %u                 读入一个无符号十进制整数
        %n                 至此已读入值的等价字符数
        %[]                扫描字符集合
        %%                 读%符号
                        
        附加格式说明字符表
        修饰符                       说明
        L/l （长度修饰符）            输入"长"数据
        h （长度修饰符）              输入"短"数据
        W 整型常数                   指定输入数据所占宽度
        * 星号                       空读一个数据
        二、空白符
        空格，制表符和换行，一般scanf函数(格式字符为%c时除外)会在读操作中略去输入中一个或多个空白符，空白符可以，直到第一个非空白字符出现为止，遇到空白字符时读取停止，并把空白字符留在输入队列中。

        三、非空白字符
        一个非空白字符会使scanf()函数在读入时剔除掉与这个非空白字符相同的字符。

        四、特别说明 %c和%s
        %s 是读字符串，读取时开始时忽略空白符，从第一非空白符开始读，直到遇到空白符停止，将空白符留在输入队列

        %c时读字符，如何字符都可以读取（包括空白符）
        ```
    + 输出printf：
        ```
        1．转换说明符
        %a(%A)     浮点数、十六进制数字和p-(P-)记数法(C99)
        %c         字符
        %d         有符号十进制整数
        %f         浮点数(包括float和doulbe)
        %e(%E)     浮点数指数输出[e-(E-)记数法]
        %g(%G)     浮点数不显无意义的零"0"
        %i         有符号十进制整数(与%d相同)
        %u         无符号十进制整数
        %o         八进制整数    e.g.     0123
        %x(%X)     十六进制整数
        %p         指针
        %s         字符串
        %%         "%"

        
        2．标志
        左对齐："-"     e.g.   "%-20s"
        右对齐："+"     e.g.   "%+20s"
        空格：          若符号为正，则显示空格，负则显示"-"     
        #：             对c,s,d,u类无影响；对o类，在输出时加前缀o；对x类，在输出时加前缀0x；对e,g,f 类当结果有小数时才给出小数点。


        3．格式字符串（格式）
        ［标志］［输出最少宽度］［．精度］［长度］类型
        "％-md" ：左对齐，若m比实际少时，按实际输出。
        "%m.ns"：输出m位，取字符串(左起)n位，左补空格，当n>m or m省略时m=n
        "%m.nf"：输出浮点数，m为宽度，n为小数点右边数位
        长度：为ｈ短整形量,ｌ为长整形量

        printf的格式控制的完整格式：
        % - .n l或h 格式字符
        下面对组成格式说明的各项加以说明：
        ①%：表示格式说明的起始符号，不可缺少。
        ②-：有-表示左对齐输出，如省略表示右对齐输出。
        ③0：有0表示指定空位填0,如省略表示指定空位不填。
        ④m.n：m指域宽，即对应的输出项在输出设备上所占的字符数。N指精度。用于说明输出的实型数的小数位数。为指定n时，隐含的精度为n=6位。
        ⑤l或h:l对整型指long型，对实型指double型。h用于将整型的格式字符修正为short型。

        一个h表示short，即short int

        两个h表示short short，即 char。
        %hhx用于输出char
        %hx用于输出short int.

        ```

5. C语言常量表示：
    ```
    1.整数常量
    整数常量可以是十进制、八进制或十六进制的常量。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，不带前缀则默认表示十进制。

    整形常量默认原则：根据常数所在范围，决定其类型。

    整数常量也可以带一个后缀，后缀是 U 和 L 的组合，U 表示无符号整数（unsigned），L 表示长整数（long）,LL 表示 long long。后缀可以是大写，也可以是小写，U 和 L 的顺序任意。

    2.浮点常量
    浮点常量由整数部分、小数点、小数部分和指数部分组成。您可以使用小数形式或者指数形式来表示浮点常量。

    当使用小数形式表示时，必须包含整数部分、小数部分，或同时包含两者。
    当使用指数形式表示时， 必须包含小数点、指数，或同时包含两者。带符号的指数是用 e 或 E 引入的。

    浮点常量默认是 double 类型。使用 F 和 f 后缀表示 float 类型，使用 L 和 l 后缀表示 long double 类型。
    ```

---

#### [返回目录](./)