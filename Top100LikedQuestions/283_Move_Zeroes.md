#  Move Zeroes
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

[LeetCode](https://leetcode.com/problems/move-zeroes/)

### Example :
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```
### Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

#  移动零
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

### 說明：
必須在原數組上操作，不能拷貝額外的數組。
盡量減少操作次數

# Solution  
## two pointers

## C

```
void moveZeroes(int *nums, int numsSize)
{
    int second = 0;
    for (int i = 1; i < numsSize; i++)
    {
        if (nums[second] == 0 && nums[i] != 0)
        {
            int tmp = nums[i];
            nums[i] = nums[second];
            nums[second] = tmp;
        }
        if (nums[second] != 0)
            second++;
    }
}
```

