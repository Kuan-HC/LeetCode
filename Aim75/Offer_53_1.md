# 劍指 Offer 58-1 在排序數組中查找數字 I

統計一個數字在排序數組中出現的次數。

[LeetCode](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

### Example 1
```
輸入: nums = [5,7,7,8,8,10], target = 8
輸出: 2
```

### Example 2
```
輸入: nums = [5,7,7,8,8,10], target = 6
輸出: 0
``` 

提示：

* 0 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9
* nums 是一個非遞減數組
* -10^9 <= target <= 10^9


## Solution  

### C++

* 時間複雜度：O(log n) 二分查找法 複雜度 log n 本題最差情況整個數最為同一數字，複雜度為 n

* 空間複雜度：O(1) 
```
#include <vector>

using namespace std;

class Solution
{
public:
    int search(vector<int> &nums, int target)
    {
        int len = nums.size();
        int ret = 0;

        if (len == 0)
            return ret;

        int left = 0;
        int right = len - 1;
        int mid = left + (right - left) / 2;
        bool found = false;

        while (left <= right)
        {
            mid = left + (right - left) / 2;

            if (nums[mid] > target)
                right = mid - 1;
            else if (nums[mid] < target)
                left = mid + 1;
            else
            {
                found = true;
                break;
            }
        }

        if (found == false)
            return ret;

        left = right = mid;

        while (left >= 0 && nums[left] == target)
            left--;
        while (right < len && nums[right] == target)
            right++;

        return right - left - 1;
    }
};

int main()
{
    /* input*/
    vector<int> input = {2};

    /* Test*/
    Solution test;
    int res = test.search(input, 2);

    return 0;
}
```
### C++

```
class Solution {
public:
    int search(vector<int>& nums, int target)
    {
        int ret = 0;
        for(const int &num :nums)
        {
            if(num == target)
                ++ret;
        }

        return ret;
    }
};
```