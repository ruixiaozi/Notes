## 算法学习笔记 分治与递归

---

递归算法：直接或者间接不断反复调用自身来达到解决问题的方法。这就要求原始问题可以分解成相同问题的子问题。

示例：阶乘、斐波纳契数列、汉诺塔问题

斐波纳契数列：又称黄金分割数列，指的是这样一个数列：1、1、2、3、5、8、13、21、……在数学上，斐波纳契数列以如下被以递归的方法定义：F1=1,F2=1,Fn=F（n-1）+F（n-2）（n>2,n∈N*））。

分治算法：待解决复杂的问题能够简化为几个若干个小规模相同的问题，然后逐步划分，达到易于解决的程度。

1、将原问题分解为n个规模较小的子问题，各子问题间独立存在，并且与原问题形式相同

2、递归的解决各个子问题

3、将各个子问题的解合并得到原问题的解

示例：棋盘覆盖、找出伪币、求最值

棋盘覆盖：在一个(2k)*(2k)个方格组成的棋盘上，有一个特殊方格与其他方格不同，称为特殊方格，称这样的棋盘为一个特殊棋盘。要求对棋盘的其余部分用L型方块填满



---

### 1. 阶乘

```
//循环
let m = parseInt(readline());
while(m-- && (n = parseInt(readline()))){
    let result = 1;
    for(let i=1;i<=n;i++){
        result *= i;
    }
    console.log(result);
}
//递归
let m = parseInt(readline());
function jc(n){
   if(n==1)
       return 1;
    return n*jc(n-1);
}
while(m-- && (n = parseInt(readline()))){
    console.log(jc(n));
}
```

### 2. 斐波拉契数列

```
//递归：O（2^n）
let m = parseInt(readline());
function fn(n){
   if(n==1 || n==2)
       return 1;
    return fn(n-1)+fn(n-2);
}
while(m-- && (n = parseInt(readline()))){
    console.log(fn(n));
}
//循环O（n）(动态规划)
let m = parseInt(readline());
while(m-- && (n = parseInt(readline()))){
	let arr = [1,1];
	for(let i=2;i<n;i++){
		arr.push(arr[i-1] + arr[i-2]);
	}
    console.log(arr[n-1]);
}

```

3. 汉罗塔问题





---

#### [返回目录](./)