# 面試金典 1601 交換數字

編寫一個函數，不用臨時變量，直接交換numbers = [a, b]中a與b的值。
 
##  Swap numbers

Write a function to swap a number in place (that is, without temporary variables).

[LeetCode](https://leetcode-cn.com/problems/swap-numbers-lcci/)


### Example 1

```
Input: numbers = [1,2]
Output: [2,1]
```

### C++ 

* 時間複雜度 O(1)

* 空間複雜度 O(1)

```
class Solution {
public:
    vector<int> swapNumbers(vector<int>& numbers) {
        numbers[0] ^= numbers[1];
        numbers[1] ^= numbers[0];
        numbers[0] ^= numbers[1];

        return numbers;
    }
};
```
