# 面試金典 0804 遞歸乘法

遞歸乘法。 寫一個遞歸函數，不使用 * 運算符， 實現兩個正整數的相乘。可以使用加號、減號、位移，但要吝嗇一些。

##  Power Set
WWrite a recursive function to multiply two positive integers without using the * operator. You can use addition, subtraction, and bit shifting, but you should minimize the number of those operations.


[LeetCode](https://leetcode-cn.com/problems/recursive-mulitply-lcci)


### Example 1
```
輸入：A = 1, B = 10
輸出：10
```

### Example 2
```
輸入：A = 3, B = 4
輸出：12
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
class Solution {
private:
    int recursion(int x, int y)
    {
        if(y == 0)
            return 0;
        return x + recursion(x, y-1);
    }
public:
    int multiply(int A, int B)
    {
        return recursion(max(A,B), min(A,B));
    }
};
```
