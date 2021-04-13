# 287. Find the Duplicate Number
Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

[LeetCode](https://leetcode.com/problems/find-the-duplicate-number)

### Example 1:
```
Input: nums = [1,3,4,2,2]
Output: 2
```

### Example 2:
```
Input: nums = [3,1,3,4,2]
Output: 3
```

### Example 3:
```
Input: nums = [1,1]
Output: 1
```
### Constraints

* 2 <= n <= 3 ^ 104
* nums.length == n + 1
* 1 <= nums[i] <= n
* All the integers in nums appear only once except for precisely one integer which appears two or more times.


#  尋找重複數
給定一個包含 n + 1 個整數的數組 nums ，其數字都在 1 到 n 之間（包括 1 和 n），可知至少存在一個重覆的整數。

假設 nums 只有 一個重覆的整數 ，找出 這個重覆的數 。



## Solution  
### Fast and slow pointers

### C
<img src="img/28.jpg" width = "1046"/>

```
int findDuplicate(int *nums, int numsSize)
{
  int slow = 0;
  int fast = 0;

  do
  {
    slow = nums[slow];
    fast = nums[nums[fast]];
    printf("pause");

  } while (slow != fast);

  int third = 0;

  while (third != slow)
  {
    slow = nums[slow];
    third = nums[third];
    printf("pause");
  }

  return slow;
}

int main()
{
  int nums[] = {1, 3, 4, 2, 2};

  int res = findDuplicate(nums, sizeof(nums) / sizeof(nums[0]));

  return 0;
}
```


