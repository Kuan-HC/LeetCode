# 面試金典 1716 按摩師

一個有名的按摩師會收到源源不斷的預約請求，每個預約都可以選擇接或不接。在每次預約服務之間要有休息時間，因此她不能接受相鄰的預約。
給定一個預約請求序列，替按摩師找到最優的預約集合（總預約時間最長），返回總的分鐘數。

## The Masseuse

A popular masseuse receives a sequence of back-to-back appointment requests and is debating which ones to accept. She needs a break between appointments and therefore she cannot accept any adjacent requests. Given a sequence of back-to-back appoint­ ment requests, find the optimal (highest total booked minutes) set the masseuse can honor. Return the number of minutes.
 
[LeetCode](https://leetcode-cn.com/problems/the-masseuse-lcci/)

### Example 1
```
Input:  [1,2,3,1]
Output:  4
Explanation:  Accept request 1 and 3, total minutes = 1 + 3 = 4

```


### C++ 

* 時間複雜度: O(N)

* 空間複雜度: O(N), 還可更進一步優化成O(1)

```
class Solution {
public:
    int massage(vector<int>& nums) {
        int len = nums.size();
        if(len == 0)
            return 0;

        /* dynammic programming兩個狀態，接 & 不接*/
        vector<vector<int>> dp(2, vector<int>(len,0));
        dp[0][0] = nums[0];

        for(int i = 1; i < len; ++i)
        {
            dp[0][i] = dp[1][i-1] + nums[i]; // 接
            dp[1][i] = max(dp[0][i-1], dp[1][i-1]); //不接
        }
        
        return max(dp[0][len - 1], dp[1][len - 1]);
    }
};
```
