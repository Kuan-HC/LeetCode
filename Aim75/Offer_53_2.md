# 劍指 Offer 53-2 0～n-1中缺失的數字
一個長度為n-1的遞增排序數組中的所有數字都是唯一的，並且每個數字都在範圍0～n-1之內。在範圍0～n-1內的n個數字中有且只有一個數字不在該數組中，請找出這個數字。

[LeetCode](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

### Example 1
```

輸入: [0,1,3]
輸出: 2
```

### Example 2
```
輸入: [0,1,2,3,4,5,6,7,9]
輸出: 8
```


* 1 <= 數組長度 <= 10000


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