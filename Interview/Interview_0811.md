# 面試金典 081 硬幣

給定數量不限的硬幣，幣值為25分、10分、5分和1分，編寫代碼計算n分有幾種表示法。(結果可能會很大，你需要將結果模上1000000007)
 
##  Coin
Given an infinite number of quarters (25 cents), dimes (10 cents), nickels (5 cents), and pennies (1 cent), write code to calculate the number of ways of representing n cents. (The result may be large, so you should return it modulo 1000000007)

[LeetCode](https://leetcode-cn.com/problems/coin-lcci)


### Example 1

```
Input: n = 5
 Output: 2
 Explanation: There are two ways:
5=5
5=1+1+1+1+1
```

### Example 2

```
Input: n = 10
 Output: 4
 Explanation: There are four ways:
10=10
10=5+5
10=5+1+1+1+1+1
10=1+1+1+1+1+1+1+1+1+1

```

### C++ 

* 時間複雜度 O(n * m2) 

* 空間複雜度 O(n)

```
class Solution
{
public:
	int waysToChange(int n)
	{
		int coins[4] = {1, 5, 10, 25};
		/* dynammic programming*/
		vector<int> dp(n + 1, 0);
		dp[0] = 1;

		for (int coin = 0; coin < 4; coin++)
		{
			for (int i = coins[coin]; i <= n; i++)
				dp[i] = (dp[i] + dp[i - coins[coin]])%1000000007;
		}

		return dp[n];
	}
};
```
