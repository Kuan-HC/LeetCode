# 劍指 Offer 56 數組中數字出現的次數

一個整型數組 nums 里除兩個數字之外，其他數字都出現了兩次。請寫程序找出這兩個只出現一次的數字。要求時間覆雜度是O(n)，空間覆雜度是O(1)。

[LeetCode](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

### Example 1
```
輸入：nums = [4,1,4,6]
輸出：[1,6] 或 [6,1]
```

### Example 2
```
輸入：nums = [1,2,10,4,1,4,3,3]
輸出：[2,10] 或 [10,2]
```

* 2 <= nums.length <= 10000


## Solution  

### C++

* 時間複雜度：O(N) ： N 為vector 長度, 需遍曆 2 次

* 空間複雜度：O(1) 
 

```
#include <vector>

using namespace std;

class Solution
{
public:
    vector<int> singleNumbers(vector<int> &nums)
    {
        int totalXorResult = 0;
        for (const auto &num : nums)
            totalXorResult ^= num;

        /* find the first bit to be 1*/
        int firstBit = 1;

        while ((totalXorResult & firstBit) != firstBit)
            firstBit <<= 1;

        /* divide the whole vector into two groupbs with firstBit is 1 or 0*/
        int valueA = 0;
        int valueB = 0;

        for (const auto &num : nums)
        {
            if ((num & firstBit) == firstBit)
                valueA ^= num;
            else
                valueB ^= num;
        }

        return vector<int>{valueA, valueB};
    }
};

int main()
{
    /* input*/
    vector<int> input = {4, 1, 4, 6};

    /* Test*/
    Solution test;
    vector<int> res = test.singleNumbers(input);

    return 0;
}
```