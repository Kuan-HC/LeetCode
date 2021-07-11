# 劍指 Offer 13 機器人的運動範圍

地上有一個m行n列的方格，從坐標 [0,0] 到坐標 [m-1,n-1] 。一個機器人從坐標 [0, 0] 的格子開始移動，它每次可以向左、右、上、下移動一格（不能移動到方格外），
也不能進入行坐標和列坐標的數位之和大於k的格子。例如，當k為18時，機器人能夠進入方格 [35, 37] ，因為3+5+3+7=18。但它不能進入方格 [35, 38]，因為3+5+3+8=19。
請問該機器人能夠到達多少個格子？
 
[LeetCode](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)


### Example 1
```
輸入：m = 2, n = 3, k = 1
輸出：3
```

### Example 2
```
輸入：m = 3, n = 1, k = 0
輸出：1
```

* 1 <= n,m <= 100
* 0 <= k <= 20

## Solution  


### C++

* 時間覆雜度: O(nm) 

* 空間覆雜度: O(nm) 

```
#include <vector>

using namespace std;

class Solution
{
private:
    int digitSum(int input)
    {
        if (input <= 9)
            return input;

        int sum = 0;
        while (input != 0)
        {
            sum += input % 10;
            input /= 10;
        }
        return sum;
    }

public:
    int movingCount(int m, int n, int k)
    {
        vector<vector<bool>> dp(m, vector<bool>(n, false));

        /* Set dp initial state*/
        dp[0][0] = true;
        int count = 1;
        for (int col = 1; col < n; col++)
        {
            if (digitSum(col) <= k && dp[0][col-1] == true)
            {
                dp[0][col] = true;
                count++;
            }
        }

        for (int row = 1; row < m; row++)
        {
            if (digitSum(row) <= k && dp[row-1][0] == true)
            {
                dp[row][0] = true;
                count++;
            }
        }

        for (int row = 1; row < m; ++row)
        {
            for (int col = 1; col < n; ++col)
            {
                int sum = digitSum(row) + digitSum(col);
                if (sum <= k && (dp[row - 1][col] == true || dp[row][col - 1] == true))
                {
                    dp[row][col] = true;
                    count++;
                }
            }
        }

        return count;
    }
};

int main()
{

    Solution test;
    int res = test.movingCount(14, 14, 5);

    return 0;
}
```
