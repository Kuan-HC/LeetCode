# 033. Search in Rotated Sorted Array

You are given an integer array nums sorted in ascending order (with distinct values), and an integer target.

Suppose that nums is rotated at some pivot unknown to you beforehand (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

If target is found in the array return its index, otherwise, return -1.

[LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array)  

### Example 1:
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

### Example 2:
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

### Example 3:
```
Input: nums = [1], target = 0
Output: -1
```

#  搜索旋轉排序數組
升序排列的整數數組 nums 在預先未知的某個點上進行了旋轉（例如， [0,1,2,4,5,6,7] 經旋轉後可能變為 [4,5,6,7,0,1,2] ）。

請你在數組中搜索 target ，如果數組中存在這個目標值，則返回它的索引，否則返回 -1


## Solution
Binary search

### C

```
int search(int *nums, int numsSize, int target)
{
    int start = 0;
    int end = numsSize - 1;
    int mid = start + (end - start) / 2;

    if (numsSize == 0)
        return -1;

    while (start <= end)
    {
        if (nums[mid] == target)
            return mid;

        if (nums[start] <= nums[mid])
        {
            /* left side is sorted */
            if (target >= nums[start] && target < nums[mid])
                end = mid - 1;
            else
                start = mid + 1;
        }
        else
        {
            /* right side is sorted */
            if (target > nums[mid] && target <= nums[end])
                start = mid + 1;
            else
                end = mid - 1;
        }
        mid = start + (end - start) / 2;
    }

    return -1;
}
```
