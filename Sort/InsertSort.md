## Insert Sort

---

**插入排序**（英語：Insertion Sort）是一種簡單直觀的**排序演算法**。它的工作原理是通過構建有序序列，對於未排序資料，在已排序序列中從後向前掃描，找到相應位置並插入。**插入排序**在實現上，通常採用in-place排序（即只需用到的額外空間的排序)，因而在從後向前掃描過程中，需要反覆把已排序元素逐步向後挪位，為最新元素提供插入空間。



| **average Time Complexity** | **`O(n^2)`** |
| --------------------------- | ---------- |
| **worst Time Complexity**   | **`O(n^2)`** |
| **best Time Complexity**    | **`O(n)`**   |
| **Space Complexity**        |  **`O(n)`**  |



###### **Example**

**假如是從小到大排序，目標值插入對列時候，從最左邊(最小)的開始比較，**
**如果遇到目標值小於對列中的數值，就不需要往後比較了。 複雜度來說，**
**最糟糕的情況，也就是每次都是比較到最後，需要 O (n^2)**

```c
// C++ program for implementation of Insertion Sort
#include <iostream>
using namespace std;

/* Function to sort array using insertion sort */
void insertionSort(int arr[], int n)
{
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;

        /* Move elements of arr[0..i-1], that are
           greater than key, to one position ahead
           of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver method
int main()
{
    int arr[] = { 12, 11, 13, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);
    printArray(arr, n);

    return 0;
}
```

#### **Reference**

* **https://www.geeksforgeeks.org/insertion-sort-algorithm/**
* **https://ithelp.ithome.com.tw/m/articles/10294880**
