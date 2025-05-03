## Double Pointer

* `*`運算子的不同優先權

```c
int* arr[10];   // 長度為10的指標陣列
int* (arr[10]); // 長度為10的指標陣列
int (*arr)[10]; // 指標指向長度為10的陣列
```

* example of double pointer

  ```c
  #include <stdio.h>
  
  int main() {
    
    	// A variable
      int var = 10;
    
      // Pointer to int
      int *ptr1 = &var;
    
      // Pointer to pointer (double pointer)
      int **ptr2 = &ptr1;  
  
      printf("var: %d\n", var);          
      printf("*ptr1: %d\n", *ptr1);
      printf("**ptr2: %d", **ptr2);
  
      return 0;
  }
  /* output
  var: 10
  *ptr1: 10
  **ptr2: 10
  */
  ```

#### Create a dynamic 2D array

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int m = 2, n = 3;

    // Create a double pointer
    int** arr;
    
    // Allocate memory for rows
    arr = (int**)malloc(m * sizeof(int*)); 

    // Allocate memory for each row
    for (int i = 0; i < m; i++)
        arr[i] = (int*)malloc(n * sizeof(int));

    // Initialize with some values
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            arr[i][j] = i * n + j + 1; 
        }
    }

    // Print the array
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }

    // Free allocated memory
    for (int i = 0; i < m; i++) {
        free(arr[i]); 
    }
    free(arr); 

    return 0;
}
```







#### Reference

* https://www.geeksforgeeks.org/c-pointer-to-pointer-double-pointer/