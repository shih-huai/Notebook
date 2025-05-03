## 一、指標

指標 ( pointer )，一個指向某個存儲位址的變數，

```c
int *ptr = &var;
```

where,

* &: 取變數位址
*  *: 為指標變數
*  **function pointer**

函數也可以使用指標，叫 **function pointer**。也就是把 ***function*** 的地址傳遞給**變數**，該**變數**就可以相當於該 ***function*** 被呼叫。

```c
void (*fptr)(type_a, type_b) = &func;
int (*fp)(int); // fp這個函數輸入是int，輸出是int
```

```C
#include <stdio.h>

int add_one(int x) {
    return x + 1;
}

int main() {
    int (*fp)(int);  // 定義一個函式指標
    fp = add_one;    // 把函式 add_one 的地址賦值給 fp

    int result = fp(5);  // 透過 fp 呼叫 add_one(5)
    printf("Result: %d\n", result);  // 輸出 Result: 6

    return 0;
}
```

use in,

* 函式sort時傳入判斷準則
* multi-thread傳函數進入建立thread的API中
* call-back function
* 也可以想像deep learning在定義 **model** 時候，在呼叫時才給予需要的 **model address** 。後續運作不用更動，只有替換模型時使用，增加程式碼可讀性。

### 1.指標判讀範例

```C
int a; // 一個整型數
int *a; // 一個指向整數的指標
int **a; // 一個指向指標的指標，它指向的指標是指向一個整型數
int a[10]; // 一個有10個整數型的陣列
int *a[10]; // 一個有10個指標的陣列，該指標是指向一個整數型的
int (*a)[10]; // 一個指向有10個整數型陣列的指標
int (*a)(int); // 一個指向函數的指標，該函數有一個整數型參數並返回一個整數
int (*a[10])(int); // 一個有10個指標的陣列，該指標指向一個函數，該函數有一個整數型參數並返回一個整數
```

### 2.指標與其他關鍵字混用

```C
const int * foo; // 一個 pointer，指向 const int 變數。
int const * foo; // 一個 pointer，指向 const int 變數。
int * const foo; // 一個 const pointer，指向 int 變數。
int const * const foo; // 一個 const pointer，指向 const int 變數。
```

## 二、Call by value, call by reference

* **call by value** : 

  只傳遞(複製)參數，不傳遞位址。所以呼叫者改變參數，傳遞者不會改變。
  ( when we **pass the value** of the parameter during the calling of the function, it copies them to the function's actual local argument. )

* **call by reference** :
  傳遞記憶體位址。呼叫者改變，傳遞者會跟著改變。
  ( when we **pass the parameter's location reference/address**, it copies and assigns them to the function's local argument. )

*C 語言之父明確表示 C 語言只有 call by value。坊間有 call by address 的說法其實是方便教學，指的是對指標變數進行操作的 call by value，具體的執行效果和 call by reference 一樣。*

## 三、變數範圍 (keyword : static)

1. local variable : 僅在函式內使用，存放在記憶體中的 **stack** 或 **heap**。
2. static variable : 靜態變數，生命週期由第一次宣告開始，直到程式結束而消失。範圍維持不變，即在宣告函式之外無法存取變數。
3. global variable : 所有區段皆可使用此變數。

### Static vs. Global

Static variable 只有在宣告檔案可以使用；Global variable 加上 extern 關鍵字修飾，即可在 header 使用該變數。

### 記憶體配置

* Stack : 存放函數的參數、區域變數，由空間配置系統自行產生與收回。(遵守LIFO)
* Heap : 由程式設計師自行分配式放，如 malloc/new 和 free/delete。
* Global : 包含 **BSS** (未初始化的靜態變數)、**data section** (全域變數、靜態變數) 和 text/code (長數字元)。 

![img](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiydSdQlo72eNMcQCFap9CnmDrMqXpMEeaII8PvYr01Gfuq5ftSy0lAggGfQvwvvNbZGybB8YHRWDUa7knVA2XVNYDM5iqtvIUcU6JjEA9yXmin0AkIJcoYz4dY-7hTSFIv8-qv8U_k9yc/s400/program_in_memory2.png)

### example

* allocation

```C
int a=0;   //global 初始化區
char *p1;  //global 未初始化區
main(){
    int b;             // stack
    char s[]="abc";    // stack
    char *p2;          // stack
    char *p3="123456"; // 123456\0 在常量區，p3在stack。
    static int c=0;   // global (static) 初始化區
    p1 = (char*)malloc(10);
    p2 = (char*)malloc(20);  //分配得來得10和20位元組的區域在heap
    strcpy(p1,"123456");  
    //123456\0 在常量區，編譯器可能會將它與 p3 中的 123456\0 優化成一個地方。
}
```

* Static

```C
static int num_a;
// 專屬於整個檔案的全域變數，其他檔案不能存取

void func (int num_b) { // stack 區 
 int num_c; // stack 區

 static int num_d; 
 //scope不變，只能在函數 func 內呼叫，但 lifetime 是整支程式執行的時間。
}
```

## 四、關鍵字 const

```const``` 表示只可讀取不可寫入(更改)的變數，常用來宣告常數，用在 :

* 程式可讀性
* 保護不希望被更動的參數

### const vs. define

1. compiler : ```define``` 在預處理階段展開；`const`在編譯階段使用。
2. 類型和安全檢查 : `const` 會在編譯階段執行檢查類型；`define` 則不會。
3. storage : `define` 直接展開不會分配記憶體；`const` 則互在記憶體中配置。