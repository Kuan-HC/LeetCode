# 面試金典 0804 冪集

編寫一種方法，返回某集合的所有子集。集合中不包含重覆的元素。

說明：解集不能包含重覆的子集。

##  Power Set LCCI
Write a method to return all subsets of a set. The elements in a set are pairwise distinct.

Note: The result set should not contain duplicated subsets.

[LeetCode](https://leetcode-cn.com/problems/power-set-lcci)


### Example 1
```
Input:  nums = [1,2,3]
 Output: 
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1)

```
#include <vector>

using namespace std;

class Solution
{
private:
    vector<vector<int>> ret;
    int len{0};
    void dfs(const int &start, vector<int>& prev, const vector<int> &nums)
    {
        ret.emplace_back(prev);
        for (int i = start; i < len; ++i)
        {
            prev.push_back(nums[i]);
            dfs(i + 1,prev , nums);
            prev.pop_back();
        }
    }

public:
    vector<vector<int>> subsets(vector<int> &nums)
    {
        len = nums.size();

        vector<int> start;
        dfs(0, start, nums);

        return ret;
    }
};

int main()
{
    /*input*/
    vector<int> input = {1, 2, 3};
    /* test*/
    Solution test;
    vector<vector<int>> res = test.subsets(input);

    return 0;
}
```
