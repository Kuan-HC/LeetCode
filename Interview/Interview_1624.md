# 面試金典 1624 對數和

設計一個算法，找出數組中兩數之和為指定值的所有整數對。一個數只能屬於一個數對。

## Pairs with Sum

Design an algorithm to find all pairs of integers within an array which sum to a specified value.

[LeetCode](https://leetcode-cn.com/problems/pairs-with-sum-lcci)

### Example 1
```
Input: nums = [5,6,5], target = 11
Output: [[5,6]]
```

### C++ 

```
class Solution
{
public:
    vector<vector<int>> pairSums(vector<int> &nums, int target)
    {
        int len = nums.size();
        if (len <= 1)
            return {};

        unordered_map<int, int> valCount;
        vector<vector<int>> ret;

        for (int i = 0; i < len; ++i)
        {
            int temp = target - nums[i];
            if (valCount.find(temp) != valCount.end() && valCount[temp] > 0)
            {
                ret.push_back({temp, nums[i]});
                valCount[temp]--;
                continue;
            }
            valCount[nums[i]]++;
        }

        return ret;
    }
};
```
