# 劍指 Offer 14-2 剪繩子 II

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

* 2 <= n <= 1000

## Solution  


### C++

* 時間覆雜度: O(n) 

* 空間覆雜度: O(1) 

```
/*
  Definition for a binary tree node.*/
class Solution
{
public:
    int cuttingRope(int n)
    {
        if (n < 4)
            return n - 1;

        unsigned int res = 1;
        while (n > 4)
        {
            n -= 3;
            res *= 3;
            res %= 1000000007;
        }
        res = res * n % 1000000007;
        return res;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int res = test.cuttingRope(62);

    return 0;
}
```
