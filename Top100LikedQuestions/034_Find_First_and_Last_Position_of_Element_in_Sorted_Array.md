# 034. Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

Follow up: Could you write an algorithm with O(log n) runtime complexity?

[LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)  

### Example 1:
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

### Example 2:
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

### Example 3:
```
Input: nums = [], target = 0
Output: [-1,-1]
```

# 在排序數組中查找元素的第一個和最後一個位置
給定一個按照升序排列的整數數組 nums，和一個目標值 target。找出給定目標值在數組中的開始位置和結束位置。

如果數組中不存在目標值 target，返回 [-1, -1]。

進階：

你可以設計並實現時間複雜度為 O(log n) 的算法解決此問題嗎？

## Solution
Binary search

### C++

* 時間複雜度 O(log n)

* 空間複雜度 O(1)

```
class Solution
{
public:
    vector<int> searchRange(vector<int> &nums, int target)
    {
        int len = nums.size();
        if (len == 0)
            return vector<int>(-1, -1);

        /*binary search*/
        int left = 0;
        int right = len - 1;
        int mid = 0;
        while (left < right)
        {
            mid = left + (right - left) / 2;

            if (nums[mid] >= target)
                right = mid;
            else
                left = mid + 1;
        }

        if (nums[left] != target)
            return vector<int>(-1, -1);

        right = left;
        while (right < len && nums[right] == nums[left])
            right++;

        return vector<int>(left, right - 1);
    }
};

int main()
{
    /* Input*/
    vector<int> input = {5, 7, 7, 8, 8, 10};
    /* unit test*/
    Solution test;
    vector<int> res = test.searchRange(input, 7);

    return 0;
}
```

### C
* This code is dirty, shall be improved
```
int binary(const int *nums, const int *numsSize, const int *target, int lower)
{
    int start = 0;
    int end = *numsSize - 1;
    int mid = 0;

    while (start <= end)
    {
        mid = start + (end - start) / 2;

        if (nums[mid] > *target || (lower == 1 && nums[mid] >= *target))
            end = mid - 1;
        else
            start = mid + 1;
    }
    return mid;
}

int *searchRange(int *nums, int numsSize, int target, int *returnSize)
{
    *returnSize = 2;
    int *ret = (int *)malloc(sizeof(int) * 2);
    memset(ret, -1, 2 * sizeof(int));

    if (numsSize == 0)
        return ret;
    else if (numsSize == 1)
    {
        if (nums[0] == target)
            memset(ret, 0, 2 * sizeof(int));
        return ret;
    }

    int temp = 0;
    temp = binary(nums, &numsSize, &target, 1);

    if (nums[temp] == target)
        ret[0] = temp;
    else if (temp + 1 < numsSize)
    {
        if (nums[temp + 1] == target)
            ret[0] = temp + 1;
        else
            return ret;
    }
    else
        return ret;

    temp = binary(nums, &numsSize, &target, 0);
    if (nums[temp] == target)
        ret[1] = temp;
    else if (temp - 1 >= 0)
    {
        if (nums[temp - 1] == target)
            ret[1] = temp - 1;
    }

    return ret;
}
```
