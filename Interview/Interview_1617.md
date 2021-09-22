# 面試金典 1617 連續數列

給定一個整數數組，找出總和最大的連續數列，並返回總和。

## Contiguous Sequence

You are given an array of integers (both positive and negative). Find the contiguous sequence with the largest sum. Return the sum.
 
[LeetCode](https://leetcode-cn.com/problems/contiguous-sequence-lcci/)

### Example 1
```
Input:  [-2,1,-3,4,-1,2,1,-5,4]
Output:  6
Explanation:  [4,-1,2,1] has the largest sum 6.
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1)

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int len = nums.size();   

        int maxSum = INT_MIN;
        int sum = 0;
        for(int i = 0; i < len; ++i)
        {
            sum += nums[i];
            maxSum = max(maxSum, sum);
            sum = sum < 0? 0:sum;
        }

        return maxSum;
    }
};
```
