## 算法学习笔记 输入输出的优化
---
### 1. 输入优化
1. 读取整形  
    ```
    //读取长整型
    inline long readLong(){
        char ch;
        int sign = 0;
        long result = 0;

        while (ch = getchar(), ch != '-' && (ch<'0' || ch>'9'));
        sign = ((ch == '-') && (ch = getchar()));

        while (ch >= '0' && ch <= '9')
            result = result * 10 + (ch - 48), ch = getchar();

        ungetc(ch, stdin);

        return sign ? -result : result;
    }

    //读取long long类型
    inline long long readLongLong(){
        char ch;
        int sign = 0;
        long long result = 0;

        while (ch = getchar(), ch != '-' && (ch<'0' || ch>'9'));
        sign = ((ch == '-') && (ch = getchar()));

        while (ch >= '0' && ch <= '9')
            result = result * 10 + (ch - 48), ch = getchar();

        ungetc(ch, stdin);

        return sign ? -result : result;
    }

    //读取整型
    inline int readInt(){
        char ch;
        int sign = 0, result = 0;

        while (ch = getchar(), ch != '-' && (ch<'0' || ch>'9'));
        sign = ((ch == '-') && (ch = getchar()));

        while (ch >= '0' && ch <= '9')
            result = result * 10 + (ch - 48), ch = getchar();

        ungetc(ch, stdin);

        return sign ? -result : result;

    }
    ```
2. 读取浮点型  
    ```
    inline double readDouble(){
        double dou;
        scanf("%lf", &dou);
        return dou;
    }
    ```
3. 读取字符串  
    ```
    //读取一个以空白字符分隔的字符串
    inline string readString(){
        string s;
        char ch;

        while (ch = getchar(), ch < '!' || ch > '~');

        s.append(1, ch);
        while (ch = getchar(), ch >= '!' && ch <= '~'){
            s.append(1, ch);
        }

        ungetc(ch, stdin);

        return s;
    }
    //读取一个空白字符分隔（不包括换行符）的字符串，换行符算作一个单独的字符串
    inline string readStringExceptEnter(){
        string s;
        char ch;

        while (ch = getchar(), ch < '!' || ch > '~'){
            if (ch == '\n')
                return "\n";
        }

        s.append(1, ch);
        while (ch = getchar(), ch >= '!' && ch <= '~'){
            s.append(1, ch);
        }

        ungetc(ch, stdin);

        return s;
    }
    //读取一行，丢掉最后的换行符
    inline string readLine(){
        string s;
        char ch;

        while (ch = getchar(), ch != '\n'){
            s.append(1, ch);
        }

        return s;
    }
    //回退字符串到缓冲区
    inline void unString(string s){
        for (register int i = s.size() - 1; i >= 0; --i)
            ungetc(s[i], stdin);
    }
    ```

---
### 2. 输出优化  

1. 字符串的输出  
    ```
    inline void pstr(string s){
        printf("%s", s.c_str());
    }

    inline void pstrln(string s){
        printf("%s\n", s.c_str());
    }
    ```

---

#### [返回目录](./)