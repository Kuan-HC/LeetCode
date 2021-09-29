# 面試金典 1605 階乘尾數

設計一個算法，算出 n 階乘有多少個尾隨零。


## Factorial Zeros

Write an algorithm which computes the number of trailing zeros in n factorial.

[LeetCode](https://leetcode-cn.com/problems/factorial-zeros-lcci/)

### Example 1

```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

### C++ 

* 時間複雜度 O(log n)

* 空間複雜度 O(1)

```
class Solution {
public:
    int trailingZeroes(int n) {
        /* 計算總共有多少個 5，需注意 25 有兩個，125 有三個*/
        int count = 0;
        while(n != 0)
        {
            n /= 5;
            count += n;
        }

        return count;       
    }
};
```
