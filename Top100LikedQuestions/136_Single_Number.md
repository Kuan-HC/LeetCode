# 136. Single Number
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

Follow up: Could you implement a solution with a linear runtime complexity and without using extra memory?

[LeetCode](https://leetcode.com/problems/single-number/)  

### Example 1:
```
Input: nums = [2,2,1]
Output: 1
```
### Example 2:
```
Input: nums = [4,1,2,1,2]
Output: 4
```
# 只出現一次的數字
給定一個非空整數數組，除了某個元素只出現一次以外，其余每個元素均出現兩次。找出那個只出現了一次的元素。  

你的算法應該具有線性時間覆雜度。 你可以不使用額外空間來實現嗎？

# Solution
constraints: linear runtime complexity and without using extra memory
hint: every element appears twice except for one

We could apply xor to our problem. 
Important features of xor: (a != 0)
a ^ 0 = a
a ^ a = 0
a ^ b ^ a = b ^ a ^ a = b ^ (a ^ a) = b ^ 0 = b

## C

```
int singleNumber(int* nums, int numsSize){
    int res = 0;
    for(int i = 0; i <numsSize; ++i)
        res ^= nums[i];

    return res;
}
```


