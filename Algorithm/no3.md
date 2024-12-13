## 算法学习笔记 复用功能函数实现
---

1. 交换值功能函数
    ```
    function swap(arr, index1, index2){
    	const temp = arr[index1];
    	arr[index1] = arr[index2];
    	arr[index2] = temp;
    }
    ```
    
2. 整数的辗转相除求最大公约数
    ```
    function gcb(a, b){
    	if(a < b){
    		const temp = a;
    		a = b;
    		b = temp;
    	}
    	
    	if(b === 0){
    		return a;
    	}
    	
    	const c = a % b;
    	if(c === 0){
    		return b;
    	}
    	
    	return gcb(c, b);
    }
    
3. 浮点数判零值
    ```
    const d_zero = 0.1;
    
    function equalZero(a){
        if (Math.abs(a) < d_zero)
            return true;
        return false;
    }
    ```

---

#### [返回目录](./)