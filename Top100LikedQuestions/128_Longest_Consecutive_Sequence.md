# 128. Longest Consecutive Sequence

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

[LeetCode](https://leetcode.com/problems/longest-consecutive-sequence)  

### Example 1:

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

### Example 2:

```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

### Constraints
* 0 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

# 128. 最長連續序列

給定一個未排序的整數數組 nums ，找出數字連續的最長序列（不要求序列元素在原數組中連續）的長度。

 

進階：你可以設計並實現時間覆雜度為 O(n) 的解決方案嗎？


## Solution

### C++


```
#include <vector>
#include <unordered_set>

using namespace std;

/* Definition for a binary tree node.*/

class Solution
{

public:
    int longestConsecutive(vector<int> &nums)
    {
        int len = nums.size();
        if (len <= 1)
            return len;

        unordered_set<int> num_set;
        for (const auto &i : nums)
            num_set.insert(i);

        int maxLen = 1;
        int tmpLen = 1;
        int next = 0;

        for (const auto &num : num_set)
        {
            next = num + 1;
            tmpLen = 1;
            if (num_set.count(num - 1) == 0)
            {
                while (num_set.count(next++) != 0)
                {
                    tmpLen++;
                }
                maxLen = maxLen > tmpLen ? maxLen : tmpLen;
            }
            
        }

        return maxLen;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {9,1,4,7,3,-1,0,5,8,-1,6};

    /* unit test*/
    Solution test;
    int res = test.longestConsecutive(input);

    return 0;
}
```