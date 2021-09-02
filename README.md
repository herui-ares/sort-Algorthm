# sort-Algorthm
# 排序算法


This just for test. 

test 2.

### TopK问题

- 堆排序思想解决
- 快排思想解决

### 冒泡排序

相邻元素两两比较，反序则交换；

每一轮完毕，将最大元素排在数组顶端；

时间复杂度：o(n^2)





![bubblesort](https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/bubblesort.gif)




```c++
vector<int> sortSolution::bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = n - 1; i >= 0; --i) {
        int cnt = 0;
        for(int j = 0; j < i; ++j) {
            if(arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j  + 1]);
                cnt++;
            }
        }
        if(cnt == 0) break;
    }

    return arr;
}
```

![](D:\钟政恰饭资料\bubblesort.gif)



### 选择排序

每一趟选出一个最小值，放到前面
时间复杂度：o(n^2)
https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/slectsort.gif
```c++
vector<int> sortSolution::selectSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = 0; i < n - 1; ++i) {
        int min = i;
        for(int j = i; j < n; ++j) {
            if(arr[j] < arr[min]) {
                min = j;
            }
        }
        if(min != i) {
            swap(arr[i], arr[min]);
        }
    }
    return arr;
}
```

![](D:\钟政恰饭资料\slectsort.gif)



### 插入排序

不断地从后面选一个数，然后插入到前面已经有序的序列里；

时间复杂度：o(n^2)
https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/insertionsort.gif
```c++
vector<int> sortSolution::insertSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = 1; i < n; ++i) {
        while(i > 0) {
            if(arr[i] < arr[i - 1]) {
                swap(arr[i], arr[i - 1]);
                i--;
            }
            else break;
        }
    }
    return arr;
}
```

![](D:\钟政恰饭资料\insertionsort.gif)



### 希尔排序

是一种分组插入排序算法
时间复杂度：o(nlogn) ~ o(n^2)

```c++
class Solution {
public:
vector<int> sortSolution::shelleSort(vector<int>& arr) {
    int n = arr.size();
    for(int gap = n / 2; gap > 0; gap /= 2) {
        for(int i = gap; i < n; ++i) {
            int tmp = arr[i];
            int j = i - gap;
            while(j >= 0 && tmp < arr[j]) {
                arr[j + gap] = arr[j];
                j -= gap;
            }
            arr[j + gap] = tmp;
        }
    }
    return arr;
}
};
```

![](D:\钟政恰饭资料\shellsort.gif)



### 快速排序

指定第一个数为mid_value,排序使得mid_value左边的数比mid_value小，右边的数比mid_value大，然后分别对左边和右边进行递归排序。
https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/quicksort.gif
```c++
class Solution {
public:
void sortSolution::quickSort(vector<int>& arr, int start, int end) {
    if(start >= end) {
        return;
    }
    int midVal = arr[start];
    int low = start;
    int high = end;
    
    while(low < high) {
        while(low < high && arr[high] >= midbVal) { 
            high--;
        }
        arr[low] = arr[high];
        while(low < high && arr[low] <= midVal) {
            low++;
        }
        arr[high] = arr[low];
    }
    arr[low] = midVal;
    quickSort(arr, start, low - 1);
    quickSort(arr, low + 1, end);
}
};
```

![](D:\钟政恰饭资料\quicksort.gif)



### 归并排序

拆分到单个元素，然后两个两个往上进行递归合并。设置left 和right两个游标,进行合并。

时间复杂度：o(nlogn)
https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/mergesort.gif
```c++
class Solution {
public:
void sortSolution::merge(vector<int> &arr, int left, int mid, int right) {
    std::vector<int> tmp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    
    while(i <= mid && j <= right) {
        tmp[k++] = arr[i] > arr[j] ? arr[i++] : arr[j++];
    }
    while(i <= mid) {
        tmp[k++] = arr[i++];
    }
    while (j <= right) {
        tmp[k++] = arr[j++];
    }
    for(int p = 0; p < tmp.size(); ++p) {
        arr[left + p] = tmp[p];
    }
}
void sortSolution::mergeSort(vector<int>& arr, int left, int right) {
    if(left >= right) {
        return;
    }
    int mid = (left + right) >> 1;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}
};
```

![](D:\钟政恰饭资料\mergesort.gif)



### 堆排序

构造堆：从小堆到大堆，先看最后一个非叶子节点，从下往上
时间复杂度 ： o(nlogn)
https://github.com/herui-ares/sort-Algorthm/blob/main/pictures/heapsort.gif


```c++
void sortSolution::maxHeap(vector<int>& arr, int i, int heapSize) {
    int l = i * 2 + 1;
    int r = l + 1;
    int largest = i;
    if(l < heapSize && arr[l] > arr[largest]) {
        largest = l;
    }
    if(r < heapSize && arr[r] > arr[largest]) {
        largest = r;
    }
    if(largest != i) {
        swap(arr[i], arr[largest]);
        maxHeap(arr, largest, heapSize);
    }
}

void sortSolution::buildMaxHeap(vector<int>& arr) {
    for(int i = arr.size() / 2 - 1; i >= 0; --i) {
        maxHeap(arr, i, arr.size());
    }
}
void sortSolution::heapSort(vector<int>& arr) {
    buildMaxHeap(arr);
    for(int i = arr.size() - 1; i > 0; --i) {
        swap(arr[0], arr[i]);
        maxHeap(arr, 0, i);
    }
}

```

![](D:\钟政恰饭资料\heapsort.gif)
