# 劍指 Offer 03 數組中重覆的數字

請實現一個函數，把字符串`s`中的每個空格替換成`%20`

[LeetCode](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

### Example

```
輸入：s = "We are happy."
輸出："We%20are%20happy."
```

### 提示
* 2 <= n <= 100000

## Solution  

### C++
* Map

* 時間複雜度：o(n)
* 空間複雜度：o(n)

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
