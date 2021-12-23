## TypeScript学习笔记 数组

### 1.「类型 + 方括号」表示法

```ts
let fibonacci: number[] = [1, 1, 2, 3, 5];
```

数组的项中**不允许**出现其他的类型

### 2. 数组泛型

也可以使用数组泛型（Array Generic） `Array<elemType>` 来表示数组：

```ts
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

### 3. 接口表示

```ts
interface NumberArray {
    [index: number]: number;
}
let fibonacci: NumberArray = [1, 1, 2, 3, 5];
```







---

#### [返回目录](./)

