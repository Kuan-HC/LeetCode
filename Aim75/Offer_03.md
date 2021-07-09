# 劍指 Offer 03 數組中重覆的數字

找出數組中重覆的數字。


在一個長度為 n 的數組 nums 里的所有數字都在 0～n-1 的範圍內。數組中某些數字是重覆的，但不知道有幾個數字重覆了，
也不知道每個數字重覆了幾次。請找出數組中任意一個重覆的數字。

[LeetCode](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

### Example

```
輸入：
[2, 3, 1, 0, 2, 5, 3]
輸出：2 或 3 
```

### 提示
* 2 <= n <= 100000

## Solution  

### C++
* Map

* 時間覆雜度：o(n)
* 空間覆雜度：o(n)

```
#include <vector>

using namespace std;

class Solution
{
public:
    int findRepeatNumber(vector<int> &nums)
    {
        int len = nums.size();
        vector<bool> digitPos(len, false);

        for (const auto &i : nums)
        {
            if (digitPos[i] != false)
                return i;
            
            digitPos[i] = true;
        }

        return -1;
    }
};

int main()
{
    /* Input */
    vector<int> input = {2, 3, 1, 0, 2, 5, 3};

    /* Test*/
    Solution test;
    int res = test.findRepeatNumber(input);

    return 0;
}
```
