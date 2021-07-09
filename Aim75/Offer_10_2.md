# 劍指 Offer 10- II 青蛙跳台階問題

一只青蛙一次可以跳上1級台階，也可以跳上2級台階。求該青蛙跳上一個 n 級的台階總共有多少種跳法。

答案需要取模 1e9+7（1000000007），如計算初始結果為：1000000008，請返回 1。

[LeetCode](https://leetcode-cn.com/problems/ing-wa-tiao-tai-jie-wen-ti-lcof/)

### Example 1
```
輸入：n = 2
輸出：2
```

### Example 2
```
輸入：n = 7
輸出：21
```

### Example 3
```
輸入：n = 0
輸出：1
```


### 提示
* 0 <= n <= 100


## Solution  

### C++

* 時間覆雜度：o(n)
* 空間覆雜度：o(1)

```
class Solution
{
public:
    int numWays(int n)
    {
        if (n <= 1)
            return 1;

        int minusOne = 1;
        int minusTwo = 1;

        /* Number of way to current position equals to
           ways to 2 step before + ways to 1 step before
        */

        int ways = 0;
        for (int i = 2; i <= n; ++i)
        {
            ways = (minusOne + minusTwo)%1000000007;
            minusTwo = minusOne;
            minusOne = ways;
        }

        return ways;
    }
};

int main()
{
    /* Input */

    /* Test*/
    Solution test;
    int res = test.numWays(3);

    return 0;
}
```
