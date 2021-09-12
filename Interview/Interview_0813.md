# 面試金典 0810 堆箱子

堆箱子。給你一堆n個箱子，箱子寬 wi、深 di、高 hi。箱子不能翻轉，將箱子堆起來時，下面箱子的寬度、高度和深度必須大於上面的箱子。實現一種方法，搭出最高的一堆箱子。
箱堆的高度為每個箱子高度的總和。

輸入使用數組[wi, di, hi]表示每個箱子。


 
##  Pile Boxes
You have a stack of n boxes, with widths wi, depths di, and heights hi. The boxes cannot be rotated and can only be stacked on top of one another if each box in the stack is strictly larger than the box above it in width, height, and depth. Implement a method to compute the height of the tallest possible stack. The height of a stack is the sum of the heights of each box.

The input use [wi, di, hi] to represents each box.


[LeetCode](https://leetcode-cn.com/problems/pile-box-lcci)


### Example 1

```
輸入：box = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
輸出：6
```

### Example 2

```
輸入：box = [[1, 1, 1], [2, 3, 4], [2, 6, 7], [3, 4, 5]]
輸出：10
```

### C++ 

* 時間複雜度 O(n^2) 

* 空間複雜度 O(n)

```
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
public:
    int pileBox(vector<vector<int>> &box)
    {
        int len = box.size();
        if (len == 0)
            return 0;

        sort(box.begin(), box.end());
        int maxHeight = 0;
        /* dynamic programming*/
        vector<int> dpSpace(len, 0);

        for (int i = 0; i < len; ++i)
        {
            dpSpace[i] = box[i][2]; // only choose box[i] least height
            for (int j = 0; j < i; j++)
            {
                if (box[i][0] > box[j][0] && box[i][1] > box[j][1] && box[i][2] > box[j][2])
                {
                    dpSpace[i] = max(dpSpace[i], dpSpace[j] + box[i][2]);
                }
            }
            maxHeight = max(maxHeight, dpSpace[i]);
        }

        return maxHeight;
    }
};

int main()
{
    /* input */
    vector<vector<int>> input = {{3, 4, 5}, {1, 1, 1}, {2, 3, 4}, {2, 6, 7}};

    /* Algorithm */
    Solution test;
    int res = test.pileBox(input);

    return 0;
}
```
