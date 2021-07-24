# 劍指 Offer 39 數組中出現次數超過一半的數字

數組中有一個數字出現的次數超過數組長度的一半，請找出這個數字。

你可以假設數組是非空的，並且給定的數組總是存在多數元素。


### Example 1

```
輸入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
輸出: 2
```

* 1 <= 數組長度 <= 50000

[LeetCode](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

## Solution  

### C++

* 時間複雜度：O(n))

* 空間複雜度：O(1)

```
#include <vector>

using namespace std;

class Solution
{
public:
    int majorityElement(vector<int> &nums)
    {
        int key = nums[0];
        int count = 0;

        for (const int &num : nums)
        {
            if (key == num)
                count++;
            else
                count--;

            if (count == 0)
            {
                key = num;
                count = 1;
            }
        }

        return key;
    }
};

int main()
{
    /* input*/
    vector<int> input = {1, 2, 3, 2, 2, 2, 5, 4, 2};

    /* Test*/
    Solution test;
    int res = test.majorityElement(input);

    return 0;
}
```