# 347. Top K Frequent Elements
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

[LeetCode](https://leetcode.com/problems/top-k-frequent-elements)

### Example 1:

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

### Example 2:

```
Input: nums = [1], k = 1
Output: [1]
```

#  前 K 个高频元素
給你一個整數數組 nums 和一個整數 k ，請你返回其中出現頻率前 k 高的元素。你可以按 任意順序 返回答案。


## Solution  
### Heap

### C++

```
#include <vector>
#include <unordered_map>
#include <queue>

using namespace std;

class Solution
{
private:
    struct FrequencyCmp
    {
        bool operator()(const pair<int, int> &lhs, const pair<int, int> &rhs) const
        {
            return lhs.second > rhs.second;
        }
    };

public:
    vector<int> topKFrequent(vector<int> &nums, int k)
    {
        /* count frequency of each value in unordered_map*/
        unordered_map<int, int> umap;
        for (const auto &i : nums)
            ++umap[i];

        priority_queue<pair<int, int>, vector<pair<int, int>>, FrequencyCmp> smallHeap;

        for (const auto &i : umap)
        {
            smallHeap.push(i);
            if (smallHeap.size() > k)
                smallHeap.pop();
        }

        vector<int> ret(k);
        for (auto &i : ret)
        {
            i = smallHeap.top().first;
            smallHeap.pop();
        }

        return ret;
    }
};

int main()
{

    vector<int> input = {1, 1, 1, 2, 2, 3};

    Solution test;
    vector<int> res = test.topKFrequent(input, 2);

    return 0;
}
```