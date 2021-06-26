# 084. Largest Rectangle in Histogram

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

[LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram)  

### Example 1:

<img src="img/084_q1.jpg" width = "600"/>

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

### Example 2:

<img src="img/084_q2.jpg" width = "400"/>

```
Input: heights = [2,4]
Output: 4
```

### Constraints:

* 1 <= heights.length <= 10^5
* 0 <= heights[i] <= 10^4


# 84. 柱狀圖中最大的矩形

給定 n 個非負整數，用來表示柱狀圖中各個柱子的高度。每個柱子彼此相鄰，且寬度為 1 。

求在該柱狀圖中，能夠勾勒出來的矩形的最大面積。

## Solution

### C++
* stack
```
#include <vector>
#include <stack>

using namespace std;

class Solution
{
private:
    stack<pair<int, int>> heightStack;
    int maxArea{0};
    int tmpArea{0};

    inline void stackProcess(const int &id)
    {
        pair<int, int> tmp = heightStack.top();
        heightStack.pop();

        if (heightStack.empty() != true)
            tmpArea = tmp.first * (id - heightStack.top().second - 1);
        else
            tmpArea = tmp.first * id;

        if( tmpArea > maxArea)
            maxArea = tmpArea;
        
    }

public:
    int largestRectangleArea(vector<int> &heights)
    {
        int len = heights.size();

        for (int i = 0; i < len; ++i)
        {
            while (heightStack.empty() != true && heights[i] < heightStack.top().first)
                stackProcess(i);

            heightStack.push(make_pair(heights[i], i));
        }

        while (heightStack.empty() != true)
            stackProcess(len);           
        
        return maxArea;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {5, 4, 1, 2};

    /* unit test*/
    Solution test;
    int res = test.largestRectangleArea(input);

    return 0;
}

```


* expand
```
#include <vector>
#include <queue>

using namespace std;

class Solution
{
private:
    struct cmp
    {
        bool operator()(const pair<int, int> &lhs, const pair<int, int> &rhs)
        {
            return lhs.first > rhs.first;
        }
    };

public:
    int
    largestRectangleArea(vector<int> &heights)
    {
        int len = heights.size();

        priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> smallHeap;

        for (int i = 0; i < len; ++i)
        {
            if (i >= 1 && heights[i] == heights[i - 1])
                continue;
            smallHeap.push(make_pair(heights[i], i));
        }

        int min = 0;
        int id = 0;
        int left = 0;

        int maxArea = 0;
        int tmpArea = 0;

        while (smallHeap.empty() != true)
        {
            min = smallHeap.top().first;
            id = smallHeap.top().second;
            smallHeap.pop();
            left = id;

            /* expand left boundary*/
            while (left - 1 >= 0 && heights[left - 1] >= min)
                --left;

            /* expand right boundary*/
            while (id + 1 < len && heights[id + 1] >= min)
                ++id;

            tmpArea = (id - left + 1) * min;
            if (tmpArea > maxArea)
                maxArea = tmpArea;
        }

        return maxArea;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {2,1,5,6,2,3};

    /* unit test*/
    Solution test;
    int res = test.largestRectangleArea(input);

    return 0;
}
```