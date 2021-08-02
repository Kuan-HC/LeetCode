# 劍指 Offer 47 禮物的最大價值

在一個 m*n 的棋盤的每一格都放有一個禮物，每個禮物都有一定的價值（價值大於 0）。你可以從棋盤的左上角開始拿格子里的禮物，
並每次向右或者向下移動一格、直到到達棋盤的右下角。給定一個棋盤及其上面的禮物的價值，請計算你最多能拿到多少價值的禮物？

[LeetCode](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/) 

### Example 1
```
輸入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
輸出: 12
解釋: 路徑 1→3→5→2→1 可以拿到最多價值的禮物
``` 

* 0 < grid.length <= 200
* 0 < grid[0].length <= 200

## Solution  


### C++

* 時間複雜度：O(m x n )  m為grid的高度 n 為grid的長度

* 空間複雜度：O(m x n)  需另外有 m x n 的 vector儲存動態規劃的過程

```
#include <vector>

using namespace std;

class Solution
{

public:
    int maxValue(vector<vector<int>> &grid)
    {
        int rowNum = grid.size();
        int colNum = grid[0].size();

        /* dynammic programming space*/
        vector<vector<int>> dp(rowNum, vector<int>(colNum, 0));

        /* initiate dynammic programming space*/
        dp[0][0] = grid[0][0];
        int col = 1;
        for (; col < colNum; ++col)
            dp[0][col] = grid[0][col] + dp[0][col - 1];

        int row = 1;
        for (; row < rowNum; ++row)
            dp[row][0] = grid[row][0] + dp[row - 1][0];

        /* dynammic programming*/
        for (row = 1; row < rowNum; ++row)
        {
            for (col = 1; col < colNum; ++col)
            {
                dp[row][col] = dp[row - 1][col] > dp[row][col - 1] ? dp[row - 1][col] : dp[row][col - 1];
                dp[row][col] += grid[row][col];
            }
        }

        return dp[rowNum - 1][colNum - 1];
    }
};

int main()
{
    /* input*/
    vector<vector<int>> input = {{1, 3, 1}, {1, 5, 1}, {4, 2, 1}};
    /* Test*/
    Solution test;
    int res = test.maxValue(input);

    return 0;
}
```