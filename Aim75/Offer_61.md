# 劍指 Offer 61 撲克牌中的順子

從撲克牌中隨機抽5張牌，判斷是不是一個順子，即這5張牌是不是連續的。2～10為數字本身，A為1，J為11，Q為12，K為13，而大、小王為 0 ，可以看成任意數字。A 不能視為 14。

[LeetCode](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

### Example 1
```

輸入: [1,2,3,4,5]
輸出: True
```

### Example 2
```

輸入: [0,0,1,2,5]
輸出: True
```

限制：

* 數組長度為 5 

* 數組的數取值為 [0, 13] .


## Solution  

### C++

* 時間複雜度：O(n) : O(N)=O(5)=O(1) ： 其中 N 為 nums 長度，本題中 N≡5 ；遍歷數組使用 O(N) 時間。

* 空間複雜度：O(1) : O(N)=O(5)=O(1) ： 用於判重的輔助 Set 使用 O(N) 額外空間

```
#include <vector>
#include <unordered_set>

using namespace std;

/* Definition for a binary tree node. */
class Solution
{
public:
    bool isStraight(vector<int> &nums)
    {
        unordered_set<int> cardSet;
        int maxNum = 0;
        int minNum = 13;
        bool ret = false;
        for (const auto &num : nums)
        {
            if (num == 0)
                continue;

            maxNum = max(num, maxNum);
            minNum = min(num, minNum);

            if (cardSet.find(num) != cardSet.end())
                return false;
            else
                cardSet.insert(num);
        }

        if ((maxNum - minNum) <= 4)
            ret = true;

        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {0, 0, 1, 2, 5};

    /* Test*/
    Solution test;
    bool res = test.isStraight(input);

    return 0;
}
```