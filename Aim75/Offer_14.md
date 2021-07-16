# 劍指 Offer 14-2 剪繩子 I

給你一根長度為 n 的繩子，請把繩子剪成整數長度的 m 段（m、n都是整數，n>1並且m>1），每段繩子的長度記為 k[0],k[1]...k[m - 1] 。請問 k[0]*k[1]*...*k[m - 1] 可能的最大乘積是多少？例如，當繩子的長度是8時，我們把它剪成長度分別為2、3、3的三段，此時得到的最大乘積是18。

答案需要取模 1e9+7（1000000007），如計算初始結果為：1000000008，請返回 1。

 
[LeetCode](https://leetcode-cn.com/problems/ian-sheng-zi-ii-lcof/)


### Example 1
```
輸入: 2
輸出: 1
解釋: 2 = 1 + 1, 1 × 1 = 1
```

### Example 2
```
輸入: 10
輸出: 36
解釋: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

* 2 <= n <= 58

## Solution  


### C++

* 時間複雜度: O(n^2) 

* 空間複雜度: O(n) 

```
class Solution
{
public:
    int cuttingRope(int n)
    {
        /**
         *  dynammic programming
         *  1. Set DP space
         *  2. Set initial state
         * */

        vector<int> dp(n + 1, 0);
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 1;

        for (int i = 3; i <= n; ++i)
        {
            /* Do not cut the robe*/
            int tmpMax = 0;
            /* Cutting the robe*/
            for (int len = 1; len <= i / 2; ++len)
            {
                
                int lenMax = len > dp[len] ? len : dp[len];
                int iminuslenMax = i - len > dp[i - len] ? i - len : dp[i - len];

                tmpMax = tmpMax > lenMax * iminuslenMax ? tmpMax : lenMax * iminuslenMax;
            }
            dp[i] = tmpMax;
        }

        return dp[n];
    }
};
```
