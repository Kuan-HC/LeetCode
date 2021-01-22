# 070. Climbing Stairs
You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

[LeetCode](https://leetcode.com/problems/climbing-stairs/)  

### Example 1:
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

### Example 2:
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

# 爬樓梯
假設你正在爬樓梯，需要N階你才能到達樓頂。  
每次你可以爬1或2個台階。你有多少種不同的方法可以爬到樓頂呢?

給定 n是一個正整數

# 動態規劃
[Wiki](https://zh.m.wikipedia.org/zh-tw/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
動態規劃背後的基本思想非常簡單。大致上，若要解一個給定問題，我們需要解其不同部分（即子問題），再根據子問題的解以得出原問題的解。  

通常許多子問題非常相似，為此動態規劃法試圖僅僅解決每個子問題一次，從而減少計算量：一旦某個給定子問題的解已經算出，則將其記憶化儲存，  
以便下次需要同一個子問題解之時直接查表。這種做法在重複子問題的數目關於輸入的規模呈指數增長時特別有用

## Solution
### C

```
int climbStairs(int n){
    if (n <= 3)
        return n;
    
    int res = 0;
    /** begine from n = 4 
     *  ways to get n = 4 is the sum of n = 2 and n = 3
     */
    int f_minus_1 = 3; 
    int f_minus_2 = 2;
    for (int i = 4; i <= n; i++)
    {
        res = f_minus_1 + f_minus_2;
        f_minus_2 = f_minus_1;
        f_minus_1 = res;
    }

    return res;
}
}
```




