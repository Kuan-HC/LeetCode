# 494. Target Sum
You are given an integer array nums and an integer target.

You want to build an expression out of nums by adding one of the symbols '+' and '-' before each integer in nums and then concatenate all the integers.

For example, if nums = [2, 1], you can add a '+' before 2 and a '-' before 1 and concatenate them to build the expression "+2-1".
Return the number of different expressions that you can build, which evaluates to target.

[LeetCode](https://leetcode.com/problems/target-sum)

### Example 1:

```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

### Example 2:

```
Input: nums = [1], target = 1
Output: 1
```
### Constraints:

* 1 <= nums.length <= 20
* 0 <= nums[i] <= 1000
* 0 <= sum(nums[i]) <= 1000
* -1000 <= target <= 1000


#  目標合
給定一個非負整數數組，a1, a2, ..., an, 和一個目標數，S。現在你有兩個符號 + 和 -。對於數組中的任意一個整數，你都可以從 + 或 -中選擇一個符號添加在前面。

返回可以使最終數組和為目標數 S 的所有添加符號的方法數。

## Solution  
Dynammic Programming
Refer to [416 分割等合子集 Partition Equal Subset Sum](https://github.com/Kuan-HC/LeetCode/blob/main/Top100LikedQuestions/416_Partition_Equal_Subset_Sum.md)


### C++

```
#include <vector>
#include <queue>
#include <numeric>
#include <cstring>

using namespace std;

class Solution
{
public:
    int findTargetSumWays(vector<int> &nums, int target)
    {
        int ret = 0;
        int sum = accumulate(nums.begin(), nums.end(), 0);
        int numsLen = nums.size();

        /* sum smaller than target, there is no way to achieve it*/
        if (sum < target)
            return ret;

        /* Allocate Dynamic Programming space*/
        int dpWidth = 2 * sum + 1;
        int dp[numsLen + 1][dpWidth];
        memset(dp, 0, sizeof(dp));

        /* Set Dynamic Programming Boundary condition, set space that sum equals to 0 to 1 */
        dp[0][sum] = 1;

        int i, j, leftAncestor, rightAncestor;

        /* loop through dynamic space*/
        for (i = 1; i <= numsLen; ++i)
        {
            for (j = 0; j < dpWidth; ++j)
            {
                /* for each dp element, its value is the sum of left and right ancestor
                   Need to consider the range, in case index out of range*/

                /* for dp[i][j], it left ancestor is dp[i-1][j-nums[i]]
                   if j-nums[i] < 0, means it is out of range*/
                leftAncestor = j - nums[i - 1] < 0 ? 0 : dp[i - 1][j - nums[i - 1]];

                /* for dp[i][j], it left ancestor is dp[i-1][j+nums[i]]
                   if j+nums[i] > sum, means it is out of range*/
                rightAncestor = j + nums[i - 1] >= dpWidth ? 0 : dp[i - 1][j + nums[i - 1]];

                dp[i][j] = leftAncestor + rightAncestor;
            }
        }

        return dp[numsLen][dpWidth / 2 + target];
    }
};

int main()
{
    vector<int> input = {1, 2, 3, 2};
    Solution test;
    int res = test.findTargetSumWays(input, 4);

    return 0;
}
```