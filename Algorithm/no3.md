## 算法学习笔记 复用功能函数实现
---

1. 交换值功能函数
    ```
    template<class T>
    inline void Rswap(T &a, T &b){
        T tem = a;
        a = b;
        b = tem;
    }
    ```
2. 整数的辗转相除求最大公约数
    ```
    template<class T>
    T gcb(T a, T b){
        if (a < b)
            swap(a, b);

        if (b == 0)
            return a;


        T c = a%b;

        if (c == 0)
            return b;

        return gcb(c, b);
    }
    ```
3. 浮点数判零值
    ```
    const double d_zero = 0.1;

    bool equalZero(double a){
        if (fabs(a) < d_zero)
            return true;
        return false;
    }
    ```