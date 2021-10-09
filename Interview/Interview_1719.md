# 面試金典 1719 消失的兩個數字

給定一個數組，包含從 1 到 N 所有的整數，但其中缺了兩個數字。你能在 O(N) 時間內只用 O(1) 的空間找到它們嗎？

以任意順序返回這兩個數字均可。

## Missing Two

You are given an array with all the numbers from 1 to N appearing exactly once, except for two number that is missing.
How can you find the missing number in O(N) time and 0(1) space?

You can return the missing numbers in any order.

[LeetCode](https://leetcode-cn.com/problems/missing-two-lcci)

### Example 1
```
Input: [1]
Output: [2,3]
```

### C++ 


```
class Solution
{
public:
    vector<int> missingTwo(vector<int> &nums)
    {
        int len = nums.size();
        if (len == 0)
            return {1, 2};

        len += 2; /* include the missing two elements*/
        long sum = 0;

        for (const auto &num : nums)
            sum += num;

        sum = (1 + len) * len / 2 - sum;

        long limit = sum / 2;
        long halfSum = 0;
        for (const auto &num : nums)
        {
            if (num <= limit)
                halfSum += num;
        }
        int firstVal =  (1 + limit) * limit / 2 - halfSum;

        return {(int)firstVal, (int)sum - firstVal};
    }
};
```
