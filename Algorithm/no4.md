## 算法学习笔记 排序算法
---

+ 各排序算法的对比
![排序算法比较](./img/pxsf.jpg)

---
### 1. 选择排序  

&emsp;&emsp;就是从需要排序的数据中选择最小的记录下来，然后放在第一个，选择第二小的放在第二个，依次下去。 
+ 时间复杂度：N<sup>2</sup>
+ 交换次数：N
+ 特点：稳定，不受数据顺序好坏影响，交换次数少

![选择排序演示](./img/xzpx.gif)

```
//选择排序算法,从小到大
template<class T>
inline void selectSort(T arr[],int begin,int end){
	int minInx;
	for (int i = begin; i <= end; ++i){
		minInx = i;
		for (int j = i + 1; j <= end; ++j){
			if (arr[j] < arr[minInx])
				minInx = j;
		}
		if (minInx != i)
			swap(arr[minInx], arr[i]);
	}
}
```

---
### 2. 插入排序  

&emsp;&emsp;遍历数组，对于每一个元素，循环与前面的元素比较，直到遇到比该元素小的为止，把元素插入到该位置后面，数组实现中可以一边比较一边交换的移动。  

+ 时间复杂度：N<sup>2</sup>
+ 比较次数：最好（N）最坏（N<sup>2</sup>）平均（N<sup>2</sup>）
+ 交换次数：最好（0） 最坏（N<sup>2</sup>） 平均（N<sup>2</sup>）
+ 特点：顺序倒置少，速度快

![插入排序演示](./img/crpx.gif)

```
//插入排序算法，从小到大
template<class T>
inline void insertSort(T arr[], int begin, int end){
	for (int i = begin; i <= end; ++i){
		for (int j = i; j > begin && arr[j]<arr[j-1]; --j){
				swap(arr[j], arr[j - 1]);		
		}
	}
}
```

---
### 3. 冒泡排序  

&emsp;&emsp;小数字慢慢往上浮，让大的数字沉淀在下方。每次冒泡结束后，当前子序列的最后一个数最大。下一轮冒泡进行到倒数第二个元素。依次进行。

+ 时间复杂度：N<sup>2</sup>
+ 特点：比较次数等于选择，交换次数等于插入。比前面两个算法效率差一点点。

![冒泡排序演示](./img/mppx.jpg)

```
//冒泡排序算法，从小到大
template<class T>
inline void bubbleSort(T arr[], int begin, int end){
	for (int i = end; i > begin; --i){
		for (int j = begin; j < i; ++j){
			if (arr[j + 1] < arr[j])
				swap(arr[j + 1], arr[j]);
		}
	}
}
```

&emsp;&emsp;可以优化冒泡排序，当某一次遍历的每一对都没有交换，那么表示已经拍好顺序了，则无需再进行后续比较。

```
//冒泡排序算法 优化版，从小到大
template<class T>
inline void bubbleSortAdvance(T arr[], int begin, int end){
	for (int i = end; i > begin; --i){
		bool isChange = false;
		for (int j = begin; j < i; ++j){
			if (arr[j + 1] < arr[j]){
				swap(arr[j + 1], arr[j]);
				isChange = true;
			}
		}
		if (!isChange)
			break;
	}
}
```

---
### 4. 梳排序  

&emsp;&emsp;梳排序是对冒泡排序的改良，因为冒泡排序比较和交换的是相邻数，也就是说间距为1的数字，梳排序的理念是这个间距可以大于1，这样就可以改善小数字在数组末尾情况的效率。

+ 时间复杂度：NlogN

![梳排序演示](./img/spx.gif)

```
//梳排序算法，从小到大
template <typename T>
void combSort(T arr[],int begin, int end) {
	int step = (int)((end - begin +1) * 0.8);   // 0.8 = 1 / 1.3
	while (step >= 1) {
		for (int i = begin; i <= end; ++i) {
			int des = i + step;
			if (des > end) {
				break;
			}
			else if (arr[i] > arr[des]) {
				swap(arr[i], arr[des]);
			}
		}
		step *= 0.8;
	}
}
```

---
### 5. 希尔排序  

&emsp;&emsp;希尔排序是插入排序的一种改进，通过分组的方式，对每一组进行插入排序，逐渐缩小增量，达到高效排序方式。在编写代码的时候可以对插入排序的算法稍加更改，就可以实现。

+ 时间复杂度：NlogN

![希尔排序示意图](./img/shellpxsm.jpg)

![希尔排序演示](./img/xrpx.gif)

```
//希尔排序,从小到大
template<class T>
inline void shellSort(T arr[], int begin, int end){
	int gap = (end - begin + 1)/2;
	while (gap > 0){
		int start = begin + gap;
		//类似插入排序，只是内部循环每次的距离的gap
		for (int i = begin; i <= end; ++i){
			for (int j = i; j >= start && arr[j]<arr[j-gap]; j -= gap){
				swap(arr[j], arr[j - gap]);
			}
		}
		gap /= 2;
	}
}
```

---
### 6. 快速排序  

&emsp;&emsp;从数组中选择一个元素，我们把这个元素称之为中轴元素吧，然后把数组中所有小于中轴元素的元素放在其左边，所有大于或等于中轴元素的元素放在其右边，显然，此时中轴元素所处的位置的是有序的。也就是说，我们无需再移动中轴元素的位置。然后再分别对中轴元素左右两个子数列递归进行上述操作。

+ 时间复杂度：NlogN
+ 特点：平均时间复杂度是最稳定于：NlogN的算法

![快速排序演示](./img/kspx.gif)

```
//快速排序
template<class T>
void quickSort(T arr[], int begin, int end){
	if (begin < end){
		int mid = quickPartition(arr, begin, end);
		quickSort(arr, begin, mid - 1);
		quickSort(arr, mid + 1, end);
	}
}

//快排用到的工具函数
template<class T>
inline int quickPartition(T arr[], int begin, int end){
	T midE = arr[begin];
	int i = begin+1, j = end;
	
	while (true){
		while (i <= j && arr[i] <= midE) ++i;

		while (i <= j && arr[j] >= midE) --j;

		if (i >= j)
			break;

		swap(arr[i], arr[j]);
	}
	swap(arr[begin], arr[j]);
	return j;
}
```

---
### 7. 堆排序  

&emsp;&emsp;