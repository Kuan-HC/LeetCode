# 劍指 Offer 56-2 數組中數字出現的次數 II

在一個數組 nums 中除一個數字只出現一次之外，其他數字都出現了三次。請找出那個只出現一次的數字。

[LeetCode](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

### Example 1

```
輸入：nums = [3,4,3,3]
輸出：4
```

### Example 2

```
輸入：nums = [9,1,7,9,7,9,7]
輸出：1
``` 

* 1 <= nums.length <= 10000
* 1 <= nums[i] < 2^31

## Solution  

### C++

#### Bit operation

* 時間複雜度：O(N) ： N 為vector 長度, 需遍曆 32 次, 由第0bit 到 第31bit

* 空間複雜度：O(1) 
 

```
#include <vector>

using namespace std;

class Solution
{
public:
    int singleNumber(vector<int> &nums)
    {
        int ret = 0;
        /* loop throuth every bit */
        for (int i = 0; i < 32; ++i)
        {
            /* loop through every number, count the sum of bit i*/
            int sum = 0;
            for (const auto &num : nums)
                sum += ((num >> i) & 1);
            
            sum %= 3;

            ret |= (sum << i);
        }
        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {3, 4, 3, 3};

    /* Test*/
    Solution test;
    int res = test.singleNumber(input);

    return 0;
}
```

### C++

#### hash table

* 時間複雜度：O(N) ： N 為vector 長度, 需遍曆 2 次

* 空間複雜度：O(1) 

```
#include <vector>
#include <unordered_map>

using namespace std;

class Solution
{
public:
    int singleNumber(vector<int> &nums)
    {
        unordered_map <int, int>map;

        for(const auto&num: nums)
            map[num]++;

        for(const auto&num: nums)
        {
            if(map[num]==1)
                return num;
        }

        return 0;
    }
};

int main()
{
    /* input*/
    vector<int> input = {3, 4, 3, 3};

    /* Test*/
    Solution test;
    int res = test.singleNumber(input);

    return 0;
}
```