## sub-array

#### Definition

---

***sub-array***，目的在於學習一個常見的演算法：**動態規劃 (Dynamic Programming)**。

* **原題**

```c
Question:
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
```

```c
Example:
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

```c
Follow up:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```

* **分析** : 找到連續的子陣列，並且陣列和要為最大。
  *注意暴力法去解的話，時間複雜度`O(N^2)`*   
* **解法** : 直接累加 array，並加上兩個`if`做為判斷機制
  * a. 陣列累加後數值變大，更新最大和的數值
  * b. 若陣列和`<0` ，把目前陣列和歸零，即該數值的部分捨棄不計

#### Example

---

```C
#include <stdio.h>
#include <limits.h> // for INT_MIN

// 函數來計算最大子陣列和
int maxSubArray(int nums[], int size) {
    int maxSum = INT_MIN; // 初始化最大和為最小整數
    int currentSum = 0;

    for (int i = 0; i < size; i++) {
        currentSum += nums[i]; // 累加當前數字
        if (currentSum > maxSum) {
            maxSum = currentSum; // 更新最大和
        }
        if (currentSum < 0) {
            currentSum = 0; // 若當前和為負數，則重新開始
        }
    }

    return maxSum;
}

int main() {
    int nums[] = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    int size = sizeof(nums) / sizeof(nums[0]);

    int result = maxSubArray(nums, size);
    printf("The maximum subarray sum is: %d\n", result);

    return 0;
}

```

#### Complexity

---

| **time**  | `O(N)` |
| --------- | ------ |
| **space** | `O(1)` |



#### **Question**

---

1. **為甚麼判斷中出現負數要捨棄，最大值不會為負嗎?**

   **在本題目中，陣列至少有一個正數，所以在`subarray`中最大必定為正，若是出現負數，該數值就不需要被記錄。另外數列中若只有負數，如`[-1, -2, -4, -1]`，就是挑選最大負數即可，也就是`Maximum`的題型。**