# 309. Best Time to Buy and Sell Stock with Cooldown
You are given an array prices where prices[i] is the price of a given stock on the ith day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

* After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).
Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

[LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown)

### Example 1:
```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

### Example 2:
```
Input: prices = [1]
Output: 0
```

#  最佳買賣股票時機含冷凍期
給定一個整數數組，其中第 i 個元素代表了第 i 天的股票價格 。​

設計一個算法計算出最大利潤。在滿足以下約束條件下，你可以盡可能地完成更多的交易（多次買賣一支股票）:

你不能同時參與多筆交易（你必須在再次購買前出售掉之前的股票）。
賣出股票後，你無法在第二天買入股票 (即冷凍期為 1 天)。


## Solution  
### Dynamic Programming

### C++
```
class Solution
{
public:
    int maxProfit(vector<int> &prices)
    {
        /* three states dynammic programming
           1. have stock: could be bought today, or we already have
           2. have no stock - not sold today
           3. have no stock = sol today
        */
        int len = prices.size();
        if (len == 0)
            return 0;
        /* initiate dp space*/
        vector<vector<int>> dp(3, vector<int>(len, 0));
        dp[0][0] = -prices[0];
        /* dynammic programming*/

        for (int i = 1; i < len; ++i)
        {
            dp[0][i] = max(dp[0][i - 1], dp[2][i - 1] - prices[i]);
            dp[1][i] = dp[0][i - 1] + prices[i];
            dp[2][i] = max(dp[1][i - 1], dp[2][i - 1]);
        }

        return max(max(dp[0][len-1], dp[1][len-1]), dp[2][len-1]);
    }
};

```

### C

```
int max(int a, int b)
{
  return (a > b ? a : b);
}

int maxProfit(int *prices, int pricesSize)
{

  /**
   * TODO: Create space to store solution for sub-problems: dp[3][pricesSize]
   * Three categories:
   * 1. Have stocks - 1.1 Bought it today 1.2  Already have it
   * 2. Have no stocks since yesterday
   * 3. Have no stocks - sells it today 
   * */

  int dp[pricesSize][3];
  int balance = 0;

  /* initial state*/
  dp[0][0] = balance - prices[0];
  dp[0][1] = 0;
  dp[0][2] = 0;

  for (int i = 1; i < pricesSize; ++i)
  {
    dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
    dp[i][1] = max(dp[i - 1][1], dp[i - 1][2]);
    dp[i][2] = dp[i - 1][0] + prices[i];
  }
  
  return max(max(dp[pricesSize - 1][0], dp[pricesSize - 1][1]), dp[pricesSize - 1][2]);
}

int main()
{
  int nums[] = {1, 2, 3, 0, 2};

  int res = maxProfit(nums, sizeof(nums) / sizeof(nums[0]));

  return 0;
}
```


