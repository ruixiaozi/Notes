## 算法例题学习笔记 基础语法逻辑题
---

1. 三个整数排序
    
    输入三个整数，按从小到大输出。  

    主要体会条件的连续使用，每个条件语句执行对后续判断存在影响。

    ```
    #include<stdio.h>
    int main(){
        int a, b, c, t;
        scanf("%d%d%d", &a, &b, &c);

        if (a > b){
            t = a;
            a = b;
            b = t;
        }//执行完以后保证a<=b

        if (a > c){
            t = a;
            a = c;
            c = t;
        }//执行完以后保证a<=c

        if (b > c){
            t = b;
            b = c;
            c = t;
        }//执行完以后保证b<=c

        printf("%d %d %d",a,b,c);
        return 0;
    }
    ```
2. 求1加到n的和

    输入正整数n，求1+2+3+……+n的和。  

    主要理解解决同一个问题可以用到数学方法，可以在常数时间内完成。

    ```
    #include<stdio.h>
    int main(){
        int n;
        scanf("%d",&n);
        printf("%d",(n + 1)*n / 2);
        return 0;
    }
    ```

---

#### [返回目录](./)
