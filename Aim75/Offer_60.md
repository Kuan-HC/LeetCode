# 劍指 Offer 60 n個骰子的點數

把n個骰子扔在地上，所有骰子朝上一面的點數之和為s。輸入n，打印出s的所有可能的值出現的概率。

[LeetCode](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)
 
 
### Example 1
```
輸入: 1
輸出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
示例 2:
```


### Example 2
```
輸出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
``` 

* 1 <= n <= 11

### C++

* 時間複雜度：O(n x n) 

* 空間複雜度：O(n) 



```
#include <vector>
#include <cmath>

using namespace std;

class Solution
{
public:
    vector<double> dicesProbability(int n)
    {
        /* different points combination*/

        vector<double> dp(6, 1.0);

        int nextLen = 0;
        int oddLen = 1;

        for (int i = 2; i <= n; ++i)
        {
            nextLen = 5 * i + 1;
            int mid = nextLen / 2;
            oddLen = oddLen == 0 ? 1 : 0;
            vector<double> tmptDp(nextLen, 1.0);

            for (int j = 1; j <= mid - oddLen; ++j)
            {
                if (j <= 5)
                    tmptDp[j] = tmptDp[j - 1] + dp[j];
                else
                {
                    tmptDp[j] = tmptDp[j - 1] + dp[j] - dp[j - 6];
                }

                tmptDp[nextLen - 1 - j] = tmptDp[j];
            }

            dp = tmptDp;
            
        }

        for (auto &i : dp)
            i /= pow(6.0, n);

        return dp;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    vector<double> res = test.dicesProbability(3);

    return 0;
}
```