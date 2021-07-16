# 劍指 Offer 10- I. 斐波那契數列
寫一個函數，輸入 n ，求斐波那契（Fibonacci）數列的第 n 項（即 F(N)）。斐波那契數列的定義如下：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契數列由 0 和 1 開始，之後的斐波那契數就是由之前的兩數相加而得出。

答案需要取模 1e9+7（1000000007），如計算初始結果為：1000000008，請返回 1。

[LeetCode](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

### 提示
* 0 <= n <= 100

## Solution  

### C++
* Dynammic Programming

* 時間複雜度：o(n)
* 空間複雜度：o(n)

```
#include <vector>

using namespace std;

class Solution
{
public:
    int fib(int n)
    {
        if (n <= 1)
            return n;
        /** Dynamic Programming
         *  Set DP space length n+1
         *  DP[0] = 0 and DP[1] = 1
         */
        vector<int> dp(n + 1, 0);
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; ++i)
            dp[i] = (dp[i - 1] + dp[i - 2])%1000000007;        

        return dp[n];
    }
};

int main()
{
    /* Input */

    /* Test*/
    Solution test;
    int res = test.fib(5);

    return 0;
}
```

* Iteration

* 時間複雜度：o(n)
* 空間複雜度：o(1)
```
#include <vector>

using namespace std;

class Solution
{
public:
    int fib(int n)
    {
        if (n <= 1)
            return n;      

        int minusOne = 1;
        int minusTwo = 0;
        int ret = 0;

        for (int i = 2; i <= n; ++i)
        {
            ret = (minusOne + minusTwo)% 1000000007;
            minusTwo = minusOne;
            minusOne = ret;
            
        }       

        return ret;
    }
};

int main()
{
    /* Input */

    /* Test*/
    Solution test;
    int res = test.fib(5);

    return 0;
}
```

* 記憶化Recursion

```
class Solution {
private:
    unordered_map<int,int> map;

public:
    int fib(int n)
    {
        if (n <= 1)
            return n;

        if(map.count(n)!= 0)
            return map[n];

        int ret = (fib(n-1) + fib(n-2))%1000000007;       
        map[n] = ret;

        return ret;
    }
};
```