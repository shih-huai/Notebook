## Decoractor

裝飾器 decorator 是 Python 的一種程式設計模式，裝飾器本質上是一個 Python 函式或類 ( class )，它可以讓其他函式或類，*在不需要做任何代碼修改的前提下增加額外功能，裝飾器的返回值也是一個函式或類對象*， 有了裝飾器，就可以抽離與函式功能本身無關的程式碼，放到裝飾器中並繼續重複使用。

在 Python 中，**使用「@」當做裝飾器使用的語法糖符號** ( 語法糖指的是將複雜的程式碼包裝起來的糖衣，也就是簡化寫法 )。

**在神經網路中，比如```@persistence.persistent_class```，是為了讓```.pkl```了解並序列化，與這邊的裝飾器用法有異。**

#### Example 

```@staticmethod```

1. none use

```python
class Calculator:
    def add(x, y):
        return x + y

# 或者正確設計法是這樣：把 add 寫成 instance method
class Calculator:
    def add(self, x, y):
        return x + y

calc = Calculator()
result = calc.add(3, 5)
print(result)  # 輸出：8
```

2. use it

```python
class Calculator:
    @staticmethod
    def add(x, y):
        return x + y
     
# 可以直接用類別呼叫，不用建立物件
result = Calculator.add(3, 5)
print(result)  # 輸出：8
```

#### Conclusion

| 比較項目                 | 有使用 `@staticmethod`     | 沒使用 `@staticmethod`       |
| ------------------------ | -------------------------- | ---------------------------- |
| 是否需要 `self`          | ❌ 不需要                   | ✅ 需要，或手動傳入           |
| 是否能用類別直接呼叫方法 | ✅ 可以                     | ❌ 不行（會報錯）             |
| 適用情境                 | 工具函式、與實例無關的邏輯 | 需要用到物件屬性或狀態的函式 |

***Advise :***

✅ 用 `@staticmethod`：當這個方法**不依賴任何類別屬性或實例屬性**，像是數學計算、轉換函式等工具。

❌ 不加（用 instance method）：當這個方法**需要用到 `self`（如內部變數、網路層等）**。

