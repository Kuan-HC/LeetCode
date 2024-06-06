# 053. Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

##  最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

[LeetCode](https://leetcode.cn/problems/maximum-subarray/)  

### Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

### Example 2:
```
Input: nums = [1]
Output: 1
```


## Solution


### C++

* Dynamic Programming

* 時間複雜度 O(n)

* 空間複雜度 O(1)

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        /*
            動態規劃，dp[i]代表著，以i為結尾的
            最大subarray, 其是由前一個狀態
            dp[i - 1]而來-> dp[i] = max(dp[i - 1] + nums[i], nums[i])
            由於只與前一個狀態有關，我們不需要真的記下整個dp，只需要前一個狀態
        */
        int prev = 0;
        int ret = INT_MIN;

        for(int i = 0; i < nums.size(); ++i){
            prev = max(prev + nums[i], nums[i]);
            ret = max(ret, prev);
        }

        return ret;
    }
};
```



