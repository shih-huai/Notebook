## Palindromic number

###### 回文數(**palindromic number**) 回文數(或迴文數)是指一個像14641這樣「對稱」的數，即：將這個數的數字按相反的順序重新排列後，所得到的數和原來的數一樣。

* **thought** : 數字左右翻轉後，數值一樣就是回文數

##### Example

```C
#include <stdio.h>
 
int main()
{
    int n, reversedInteger = 0, remainder, originalInteger;
 
    printf("输入一个整数: ");
    scanf("%d", &n);
 
    originalInteger = n;
 
    // 翻转
    while( n!=0 )
    {
        remainder = n%10;
        reversedInteger = reversedInteger*10 + remainder;
        n /= 10;
    }
 
    // 判断
    if (originalInteger == reversedInteger)
        printf("%d 是回文数。", originalInteger);
    else
        printf("%d 不是回文数。", originalInteger);
    
    return 0;
}
```

