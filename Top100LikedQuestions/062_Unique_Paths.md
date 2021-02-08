# 062. Unique Paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

[LeetCode](https://leetcode.com/problems/unique-paths)  

### Example 1:
<img src="img/062_q.png" width = "400"/>
```
Input: m = 3, n = 7
Output: 28
```

### Example 2:
```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

### Example 3:
```
Input: m = 7, n = 3
Output: 28
```

#  不同路徑
一個機器人位於一個 m x n 網格的左上角 （起始點在下圖中標記為 “Start” ）。

機器人每次只能向下或者向右移動一步。機器人試圖達到網格的右下角（在下圖中標記為 “Finish” ）。

問總共有多少條不同的路徑？

## Solution
* Dynamic Programming

### C

```
int uniquePaths(int m, int n)
{
    /* m: number of rows, n: number of columns */
    int map[m][n];

    /*set bundary condition*/
    int i = 0;
    for (i = 0; i < n; ++i)
        map[0][i] = 1;

    for (i = 0; i < m; ++i)
        map[i][0] = 1;

    /* Dynamic Programming */
    for (i = 1; i < m; ++i)
    {
        for (int j = 1; j < n; ++j)
        {
            map[i][j] = map[i - 1][j] + map[i][j - 1];
        }
    }
    return map[m - 1][n - 1];
}

int main()
{
    int ans = uniquePaths(3, 7);

    return 0;
}
```
