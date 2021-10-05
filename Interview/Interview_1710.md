# 面試金典 1710 主要原素

數組中占比超過一半的元素稱之為主要元素。給你一個 整數 數組，找出其中的主要元素。若沒有，返回 -1 。

請設計時間覆雜度為 O(N) 、空間覆雜度為 O(1) 的解決方案。


## Find Major Element

A majority element is an element that makes up more than half of the items in an array. Given a integers array, find the majority element.
If there is no majority element, return -1. Do this in O(N) time and O(1) space.

[LeetCode](https://leetcode-cn.com/problems/find-majority-element-lcci/)

### Example 1
```
Input: [1,2,5,9,5,9,5,5,5]
Output: 5
```

### C++ 

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int len = nums.size();
        int count = 0;
        int key = 0;

        for(int i = 0; i < len; ++i)
        {
            if(count == 0)
                key = nums[i];

            if(nums[i] == key)
                count++;
            else
                count--;               
        }

        count = 0;
        for(int i = 0; i < len; ++i)
        {
            if(nums[i] == key)
                count++;
        }

        if(count > len>>1)
            return key;
        return -1;
    }
};
```
