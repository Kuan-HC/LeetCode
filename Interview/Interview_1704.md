# 面試金典 1704 消失的數字

數組nums包含從0到n的所有整數，但其中缺了一個。請編寫代碼找出那個缺失的整數。你有辦法在O(n)時間內完成嗎？

## Missing Number

An array contains all the integers from 0 to n, except for one number which is missing.  Write code to find the missing integer.
Can you do it in O(n) time?

[LeetCode](https://leetcode-cn.com/problems/missing-number-lcci)

### Example 1
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8

```

### C++ 

* 時間複雜度: O(n)

* 空間複雜度: O(n)

```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int len = nums.size();
        vector<bool>position(len + 1, false);

        for(const int& num: nums)
            position[num] = true;

        for(int i = 0; i <= len; ++i )
        {
            if(position[i] == false)
                return i;
        }

        return 0;
    }
};

```
