## SWAP

#### SWAP (bit operation)

***XOR Swap Algorithm***，透過 **位元運算** 來交換兩個變數的值，而不使用第三個變數。優勢在於 **減少額外的記憶體使用** 。

* ***思路*** : 電腦運算時使用的是二進制，**XOR** `^` 在計算上同樣數值運算得到 0，`a^a=0`

* ***XOR Swap*** 只是用於整數類型 `int, long, char`，因為他們是位元數據

#### Code example

---

```C
void XorSwap(int *x, int *y) 
{
  if (x == y) return;
  *x ^= *y;
  *y ^= *x;
  *x ^= *y;
}
```

```C
#include <stdio.h>

void swap(int *a, int *b) {
    *a = *a ^ *b;
    *b = *a ^ *b; // b = a^b^b = a
    *a = *a ^ *b; // a = a^b^a = b
}

int main() {
    int x = 5, y = 10;
    printf("Before swap: x = %d, y = %d\n", x, y);
    swap(&x, &y);
    printf("After swap: x = %d, y = %d\n", x, y);
    return 0;
}
```

