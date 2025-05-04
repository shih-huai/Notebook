## Binary Search

在***已排序的陣列中 (遞增 or 遞減)***，定義中點並選擇左右開始搜尋，時間複雜度為`O(log n)`。

#### Example

```c
#include <stdio.h>

int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target) // search right
            left = mid + 1;
        else // search left
            right = mid - 1;
    }

    return -1; // not found
}

int main() {
    int arr[] = {1, 3, 5, 7, 9, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 7;

    int result = binarySearch(arr, n, target);
    if (result != -1)
        printf("Found at index: %d\n", result);
    else
        printf("Not found.\n");

    return 0;
}
```

