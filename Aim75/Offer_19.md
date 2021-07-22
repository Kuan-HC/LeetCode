# 010. 正則表達式匹配

給你一個字符串 s 和一個字符規律 p，請你來實現一個支持 '.' 和 '*' 的正則表達式匹配。

* '.' 匹配任意單個字符
* '*' 匹配零個或多個前面的那一個元素

所謂匹配，是要涵蓋 整個 字符串 s的，而不是部分字符串。

[LeetCode](https://leetcode-cn.com/problems/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)


### Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

### Example 2:
```
Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

### Example 3:
```
Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```


## Solution  
* Dynammic Programming

<img src="img/019_1.jpg" width = "400"/>

<img src="img/019_2.jpg" width = "400"/>

<img src="img/019_3.jpg" width = "400"/>

### C++

* 時間複雜度：O(mn)，其中 m 和 n 分別是字符串 s 和 p 的長度。我們需要計算出所有的狀態，並且每個狀態在進行轉移時的時間複雜度為 O(1)。

* 空間複雜度：O(mn)，即為存儲所有狀態使用的空間。

```
#include <string>
#include <vector>

using namespace std;

class Solution
{
public:
    bool isMatch(string s, string p)
    {
        /** dynamic programming 
         *  Step 1: set dp space */
        int colLen = p.size() + 1;
        int rowLen = s.size() + 1;
        vector<vector<bool>> dp(rowLen, vector<bool>(colLen, false));

        /* dp space initialization*/
        int col = 0;
        int row = 0;
        dp[0][0] = true;

        for (col = 1; col < colLen; ++col)
        { 
            if (p[col - 1] == '*')
                dp[0][col] = dp[0][col - 2];
        }

        /* dynammic programming*/
        for (row = 1; row < rowLen; ++row)
        {
            for (col = 1; col < colLen; ++col)
            {
                if (p[col - 1] == '*')
                {
                    if (dp[row][col - 2] == true)
                        dp[row][col] = true;
                    else if (s[row - 1] == p[col - 2] || p[col - 2] == '.')
                        dp[row][col] = dp[row - 1][col];
                }
                else if (s[row - 1] == p[col - 1] || p[col - 1] == '.')
                    dp[row][col] = dp[row - 1][col - 1];
            }
        }

        return dp[rowLen - 1][colLen - 1];
    }
};

int main()
{
    /* input*/
    string s = "aaa";
    string p = "ab*a*c*a";

    /* Test*/
    Solution test;
    bool res = test.isMatch(s, p);
    return 0;
}
```