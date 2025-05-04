## Invert Binary Tree

將建立好的 Binary tree ，對於每一個節點進行左右反轉。



#### Example

```c++
#include <iostream>
using namespace std;

// define TreeNode struct
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

// invert binary tree
TreeNode* invertTree(TreeNode* root) {
    if (root == nullptr) return nullptr;

    TreeNode* left = invertTree(root->left);
    TreeNode* right = invertTree(root->right);

    root->left = right;
    root->right = left;

    return root;
}

// invert binary tree
// version 2
void Invert(TreeNode* root){
    if (root != nullptr){
        TreeNode* left = root->left;
        TreeNode* right = root->right;
        root->left = right;
        root->right = left;
        Invert(root->left);
        Invert(root->right);
    }
}

void printInOrder(TreeNode* root) {
    if (root == nullptr) return;
    printInOrder(root->left);
    cout << root->val << " ";
    printInOrder(root->right);
}

int main() {
    /*
        建立範例樹：
              1
             / \
            2   3
           / \
          4   5
    */

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2, new TreeNode(4), new TreeNode(5));
    root->right = new TreeNode(3);

    cout << "原始樹的中序走訪: ";
    printInOrder(root);
    cout << endl;

    invertTree(root);

    cout << "翻轉後的中序走訪: ";
    printInOrder(root);
    cout << endl;
    
	Invert(root);

    cout << "再次翻轉中序走訪: ";
    printInOrder(root);
    cout << endl;
    return 0;
}
```



#### Tips

* `struct` 的建構子 :

  此方式稱為**初始化列表**，在主程式定義完 `struct`，就能使用啟用不同的方式賦予數值。

  ```c++
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};
  ```

* `struct` 使用 `new` 建立 :

  `new` 會在**heap建立物件**，並且回傳**地址**，但存放在此的變數並不會自動釋放記憶體，不需要的時候需使用 `delete` 將變數釋放。所以在建立 binary tree 的時候傳入的 type 為 `TreeNode *` ，如下

  ```c++
  // 從 root 開始建立
  TreeNode* root = new TreeNode(1);
  root->left = new TreeNode(2, new TreeNode(4), new TreeNode(5));
  root->right = new TreeNode(3);
  ```

  若是不使用 `new`，則需要**先建立變數再傳遞位址**，如下

  ```c++
  // 須從 leaf 開始建立
  TreeNode n4(4);
  TreeNode n5(5);
  TreeNode n2(2, &n4, &n5);
  TreeNode n3(3);
  TreeNode root(1, &n2, &n3);
  // 若傳入上述 function 則傳入位址，ex:
  invertTree( &root );
  ```

  

