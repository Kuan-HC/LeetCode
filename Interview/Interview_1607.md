# 面試金典 1607 最大數值

編寫一個方法，找出兩個數字a和b中最大的那一個。不得使用if-else或其他比較運算符。
 
##  Maximum 

Write a method that finds the maximum of two numbers. You should not use if-else or any other comparison operator.

[LeetCode](https://leetcode-cn.com/problems/maximum-lcci/)


### C++ 

* 時間複雜度 O(1) 

* 空間複雜度 O(1)

```
class Solution {
public:
    int maximum(int a, int b) {
        long temp = abs((long)a - b);
        return ((long)a + b + temp) / 2;
    }
};
```
