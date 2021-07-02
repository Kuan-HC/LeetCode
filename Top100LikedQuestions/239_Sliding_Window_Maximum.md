# 239. Sliding Window Maximum
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

[LeetCode](https://leetcode.com/problems/sliding-window-maximum)

### Example 1:
```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

### Example 2:
```
Input: nums = [1], k = 1
Output: [1]
```

### Example 3:
```
Input: nums = [1,-1], k = 1
Output: [1,-1]
```

### Constraints:

* 1 <= nums.length <= 105
* -104 <= nums[i] <= 104
* 1 <= k <= nums.length

#  滑動窗口的最大值
給你一個整數數組 nums，有一個大小為 k 的滑動窗口從數組的最左側移動到數組的最右側。你只可以看到在滑動窗口內的 k 個數字。滑動窗口每次只向右移動一位。

返回滑動窗口中的最大值。

## Solution  


### C

* heap

```
#include <vector>
#include <queue>
#include <utility>

using namespace std;

class Solution
{
private:
    struct cmp
    {
        bool operator()(const pair<int, int> &lhs, const pair<int, int> &rhs)
        {
            return lhs.second < rhs.second;
        }
    };

public:
    vector<int> maxSlidingWindow(vector<int> &nums, int k)
    {
        int len = nums.size();
        if (len == 1)
            return nums;

        priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> heap;
        
        vector<int> ret;

        int idx = 0;
        for (idx = 0; idx < k; ++idx)
        {
            heap.emplace(make_pair(idx, nums[idx]));
        }
        ret.push_back(heap.top().second);

        for (int idx = k; idx < len; ++idx)
        {
            heap.emplace(make_pair(idx, nums[idx]));

            while (heap.top().first <= idx - k)
                heap.pop();
            
            ret.push_back(heap.top().second);
        }

        return ret;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {1, 3, -1, -3, 5, 3, 6, 7};

    /* unit test*/
    Solution test;
    vector<int> res = test.maxSlidingWindow(input, 3);

    return 0;
}
```

```
#include <vector>
#include <deque>

using namespace std;

class Solution
{

public:
    vector<int> maxSlidingWindow(vector<int> &nums, int k)
    {
        int len = nums.size();
        if (len == 1)
            return nums;

        deque<int> dq;

        int idx = 0;
        /* build first window*/
        for (idx = 0; idx < k; ++idx)
        {
            while ((dq.empty() != true) && (nums[dq.back()] < nums[idx]))
                dq.pop_back();
            dq.push_back(idx);
        }

        vector<int> ret;
        ret.push_back(nums[dq.front()]);

        for (idx = k; idx < len; ++idx)
        {
            while ((dq.empty() != true) && (nums[dq.back()] < nums[idx]))
                dq.pop_back();
            dq.push_back(idx);

            while (dq.front() <= idx - k)
                dq.pop_front();

            ret.push_back(nums[dq.front()]);            
        }

        return ret;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {1, 3, -1, -3, 5, 3, 6, 7};

    /* unit test*/
    Solution test;
    vector<int> res = test.maxSlidingWindow(input, 3);

    return 0;
}
```
