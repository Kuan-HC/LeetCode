# 劍指 Offer 57 和為s的兩個數字

輸入一個遞增排序的數組和一個數字s，在數組中查找兩個數，使得它們的和正好是s。如果有多對數字的和等於s，則輸出任意一對即可。

[LeetCode](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)


### Example 1

```
輸入：nums = [10,26,30,31,47,60], target = 40
輸出：[10,30] 或者 [30,10]
```

### Example 2

```
輸入：nums = [2,7,11,15], target = 9
輸出：[2,7] 或者 [7,2]

```

* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^6

## Solution  

### C++

* 時間複雜度：O(n) n 為vector 長度

* 空間複雜度：O(1)

```
class Solution
{
public:
    vector<int> twoSum(vector<int> &nums, int target)
    {
        int len = nums.size();

        int left = 0;
        int right = len - 1;
        vector<int> ret;

        while (nums[right] > target)
            --right;

        int sum = 0;
        while (left < right)
        {
            sum = nums[left]+nums[right];
            if(sum > target)
                --right;
            else if(sum < target)
                ++left;
            else
            {
                ret = {nums[left], nums[right]};
                break;
            }            
        }
        
        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {10, 26, 30, 31, 47, 60};

    /* Test*/
    Solution test;
    vector<int> res = test.twoSum(input, 40);

    return 0;
}
```

* 時間複雜度：O(n) n 為vector 長度

* 空間複雜度：O(n) 最差情況下，需要建立n個map

```
#include <vector>
#include <unordered_map>

using namespace std;

class Solution
{
public:
    vector<int> twoSum(vector<int> &nums, int target)
    {
        unordered_map<int, vector<int>> map;

        int residual = 0;
        for (const auto &num : nums)
        {
            if(num > target)
                break;

            if(map.count(num) != 0)
                return map[num];

            /* build the map*/
            residual = target - num;
            map[residual] = {num, residual};   
        }

        vector<int> noMatch(0);
        return noMatch;
    }
};

int main()
{
    /* input*/
    vector<int> input = {10, 26, 31, 31, 47, 60};

    /* Test*/
    Solution test;
    vector<int> res = test.twoSum(input, 40);

    return 0;
}
```