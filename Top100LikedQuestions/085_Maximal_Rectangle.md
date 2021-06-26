# 085. Maximal Rectangle

Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

[LeetCode](https://leetcode.com/problems/maximal-rectangle)  

### Example 1:

<img src="img/085_q1.jpg" width = "400"/>

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.
```

### Example 2:

```
Input: matrix = []
Output: 0
```

### Example 3:

```
Input: matrix = [["0"]]
Output: 0
```

### Constraints:

* rows == matrix.length
* cols == matrix[i].length
* 0 <= row, cols <= 200
* matrix[i][j] is '0' or '1'.



# 84. 最大矩形

給定一個僅包含 0 和 1 、大小為 rows x cols 的二維二進制矩陣，找出只包含 1 的最大矩形，並返回其面積。

## Solution

### C++
* Dynamic Programming 


```
#include <vector>
#include <cmath>

using namespace std;

class Solution
{
public:
    int maximalRectangle(vector<vector<char>> &matrix)
    {
        int row = matrix.size();
        if (row == 0)
            return 0;

        int col = matrix[0].size();

        /* allocate dynamic programming space*/
        vector<vector<int>> vertical(row, vector<int>(col, 0));
        vector<vector<int>> horizontal(row, vector<int>(col, 0));
        vector<vector<int>> final(row, vector<int>(col, 0));

        int i = 0;
        int j = 0;
        int maxSize = 0;
        /*vertical DP space initialization*/
        for (i = 0; i < col; ++i)
        {
            if (matrix[0][i] == '1')
            {
                vertical[0][i] = 1;
                maxSize = 1;
            }
        }
        /* vertical dynammic programming*/
        for (i = 1; i < row; ++i)
        {
            for (j = 0; j < col; ++j)
            {
                if (matrix[i][j] == '1')
                {
                    vertical[i][j] = vertical[i - 1][j] + 1;
                    maxSize = vertical[i][j] > maxSize ? vertical[i][j] : maxSize;
                }
            }
        }

        /*horizontal DP space initialization*/
        for (i = 0; i < row; ++i)
        {
            if (matrix[i][0] == '1')
            {
                horizontal[i][0] = 1;
                maxSize = horizontal[i][0] > maxSize ? horizontal[i][0] : maxSize;;
            }
        }
        /* horizontal dynammic programming*/
        for (i = 0; i < row; ++i)
        {
            for (j = 1; j < col; ++j)
            {
                if (matrix[i][j] == '1')
                {
                    horizontal[i][j] = horizontal[i][j - 1] + 1;
                    maxSize = horizontal[i][j] > maxSize ? horizontal[i][j] : maxSize;
                }
            }
        }

        /* Final DP space initialization*/
        final[0] = horizontal[0];
        for (i = 1; i < row; ++i)
            final[i][0] = vertical[i][0];

        /* Final dynammic programming*/
        for (i = 1; i < row; ++i)
        {
            for (j = 1; j < col; ++j)
            {
                if (matrix[i][j] == '0')
                    final[i][j] = 0;
                else if ((final[i - 1][j] == 0) || (final[i][j - 1] == 0))
                    final[i][j] = max(horizontal[i][j], vertical[i][j]);
                else if (final[i - 1][j - 1] == 0)
                    final[i][j] = max(final[i][j - 1], final[i - 1][j]) + 1;
                else if (final[i - 1][j - 1] != 0)
                {
                    int layer = vertical[i][j];
                    int length = horizontal[i][j];
                    int tmpMax = length;

                    for (int offset = 1; offset < layer; ++offset)
                    {
                        length = length > horizontal[i - offset][j] ? horizontal[i - offset][j] : length;
                        tmpMax = tmpMax >length * (offset+1)?tmpMax:length * (offset+1);
                    }

                    final[i][j] = tmpMax;
                }

                maxSize = final[i][j] > maxSize ? final[i][j] : maxSize;
            }
        }

        return maxSize;
    }
};

int main()
{
    /* Input*/
    vector<vector<char>> input = {{'0', '0', '0', '0', '0', '0', '1'}, {'0', '0', '0', '0', '1', '1', '1'}, {'1', '1', '1', '1', '1', '1', '1'}, {'0', '0', '0', '1', '1', '1', '1'}};
    
    /* unit test*/
    Solution test;
    int res = test.maximalRectangle(input);

    return 0;
}
```