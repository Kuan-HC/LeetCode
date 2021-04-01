# 200. Number of Islands
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

[LeetCode](https://leetcode.com/problems/number-of-islands)  

### Example 1:

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

### Example 2:

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```


# 島嶼數量

給你一個由 '1'（陸地）和 '0'（水）組成的的二維網格，請你計算網格中島嶼的數量。

島嶼總是被水包圍，並且每座島嶼只能由水平方向和/或豎直方向上相鄰的陸地連接形成。

此外，你可以假設該網格的四條邊均被水包圍。

## Solution

### C
* Breadth*First Search

```
#include <vector>
#include <deque>
using std::deque;
using std::vector;

class Solution
{
private:
  struct position
  {
    position() : x(0), y(0){};
    position(int _x, int _y) : x(_x), y(_y){};
    int x;
    int y;
  };

  int rowNum;
  int colNum;
  deque<position> open;
  vector<vector<int>> deltaList = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
  int inselValue{0};

  /** TODO: Breadth-First Algorithm*/
  void BFS(vector<vector<char>> &grid, vector<vector<bool>> &visted)
  {
    while (open.empty() != true)
    {
      auto expand = open.front();
      open.pop_front();

      position next;
      for (auto &move : deltaList)
      {
        next.x = expand.x + move[0];
        next.y = expand.y + move[1];

        if ((next.x < 0) || (next.x >= rowNum) || (next.y < 0) || (next.y >= colNum))
          continue;

        if ((visted[next.x][next.y] != true) && (grid[next.x][next.y] == '1'))
        {
          open.emplace_back(next);
          visted[next.x][next.y] = true;
        }
      }
    }
    ++inselValue;
  }

public:
  int numIslands(vector<vector<char>> &grid)
  {
    /** 
     * TODO: create a map record spots has been visted*
     */
    rowNum = grid.size();
    colNum = grid[0].size();
    vector<vector<bool>> visted(rowNum, vector<bool>(colNum, 0));

    for (int i = 0; i < rowNum; ++i)
    {
      for (int j = 0; j < colNum; ++j)
      {
        /**
         * TODO: Set the initial point for BFS algorithm
         * */
        if ((grid[i][j] == '1') && visted[i][j] != true)
        {
          visted[i][j] = true;
          open.emplace_back(position(i, j));
          /** TODO: Breadth-First Search*/
          BFS(grid, visted);
        }
      }
    }

    return inselValue;
  }
};

int main()
{
  vector<vector<char>> input = {{'1', '1', '0', '0', '0'},
                                {'1', '1', '0', '0', '0'},
                                {'0', '0', '1', '0', '0'},
                                {'0', '0', '0', '1', '1'}};

  Solution test;
  int ans = test.numIslands(input);

  return 0;
}
```