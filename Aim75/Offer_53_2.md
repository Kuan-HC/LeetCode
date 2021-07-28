# 劍指 Offer 53-2 左旋轉字符串

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

[LeetCode](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

### Example 1
```

输入: [0,1,3]
输出: 2
```

### Example 2
```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```


* 1 <= 数组长度 <= 10000


## Solution  

### C++

* 時間複雜度：O(log n) 二分法为对数级别复杂度。

* 空間複雜度：O(1) 

```
#include <vector>

using namespace std;

class Solution
{
public:
    int missingNumber(vector<int> &nums)
    {
        int len = nums.size();
        if(len == 1)
           return nums[0] == 0? 1:0;

        int left = 0;
        int right = len - 1;
        int mid = 0;

        while (left < right)
        {
            mid = left + (right - left) / 2;
            if (nums[mid] == mid)
                left = mid + 1;
            else
                right = mid;
        }

        /* condition below if for left reachch the end*/
        if(nums[left] == left)
            ++left;

        return left;
    }
};

int main()
{
    /* input*/
    vector<int> input = {0,1,2,3,4,5,6,7,9};

    /* Test*/
    Solution test;
    int res = test.missingNumber(input);

    return 0;
}
```