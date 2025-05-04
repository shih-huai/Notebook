## String Reverse

String reverse，陣列反轉。

```c
#include <stdio.h>
#include <string.h>

void reverseString(char *str) {
    int left = 0;
    int right = strlen(str) - 1;
    while (left < right) {
        char temp = str[left];
        str[left] = str[right];
        str[right] = temp;
        left++;
        right--;
    }
}

int main() {
    char str[] = "hello";
    printf("String  : %s\n", str);
    reverseString(str);
    printf("Reversed: %s\n", str);
    return 0;
}
```