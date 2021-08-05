# 劍指 Offer 63 股票的最大利率

假設把某股票的價格按照時間先後順序存儲在數組中，請問買賣該股票一次可能獲得的最大利潤是多少？

[LeetCode](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

### Example 1
```
輸入: [7,1,5,3,6,4]
輸出: 5
解釋: 在第 2 天（股票價格 = 1）的時候買入，在第 5 天（股票價格 = 6）的時候賣出，最大利潤 = 6-1 = 5 。
     注意利潤不能是 7-1 = 6, 因為賣出價格需要大於買入價格。
```

### Example 2
```
輸入: [7,6,4,3,1]
輸出: 0
解釋: 在這種情況下, 沒有交易完成, 所以最大利潤為 0。
```

* 0 <= 數組長度 <= 10^5

## Solution  

### C++

* 時間複雜度：O(n) : 數列的長度

* 空間複雜度：O(1) 

```
#include <vector>

using namespace std;

class Solution
{
public:
    int maxProfit(vector<int> &prices)
    {
        int buy = prices[0];
        int profit = 0;

        for (const auto &price : prices)
        {
            if (price - buy <= 0)
                buy = price;
            
            profit = price - buy > profit? price - buy: profit;
        }

        return profit;
    }
};

int main()
{
    /* input*/
    vector<int> input = {7, 1, 5, 3, 6, 4};
    /* Test*/
    Solution test;
    int res = test.maxProfit(input);
    ;

    return 0;
}
```