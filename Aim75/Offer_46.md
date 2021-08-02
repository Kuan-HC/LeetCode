# 劍指 Offer 46 把數字翻譯成字符串

給定一個數字，我們按照如下規則把它翻譯為字符串：0 翻譯成 “a” ，1 翻譯成 “b”，……，11 翻譯成 “l”，……，25 翻譯成 “z”。
一個數字可能有多個翻譯。請編程實現一個函數，用來計算一個數字有多少種不同的翻譯方法。

[LeetCode](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

### Example 1
```
輸入: 12258
輸出: 5
解釋: 12258有5種不同的翻譯，分別是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
``` 

* 0 <= num < 2^31

## Solution  


### C++

* 時間複雜度：O(n)  n 為數字的長度

* 空間複雜度：O(n)  需另外有 vector<int> 長度 n 儲存 input的每一位

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
public:
    int translateNum(int num)
    {
        if (num < 10)
            return 1;

        /* split num*/
        vector<int> nums;
        while (num != 0)
        {
            nums.push_back(num % 10);
            num = num / 10;
        }
        reverse(nums.begin(), nums.end());

        /* allocate dp space*/
        int dpLen = nums.size();
        vector<int> dp(dpLen, 0);

        /*initiate dp space*/
        dp[0] = 1;
        dp[1] = (nums[0] * 10 + nums[1]) > 25 ? 1 : 2;

        /* initiate dp*/
        for (int i = 2; i < dpLen; ++i)
        {
            int tmp = nums[i - 1] * 10 + nums[i];
            dp[i] = (tmp > 25 || tmp < 10)  ? dp[i - 1] : dp[i - 1] + dp[i - 2];
        }

        return dp[dpLen - 1];
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int res = test.translateNum(12258);

    return 0;
```