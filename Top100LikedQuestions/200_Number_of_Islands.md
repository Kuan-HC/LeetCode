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

### C++

* Breadth*First Search

```
class Solution
{
private:
  vector<vector<int>> movement = {{0,1}, {1,0}, {0,-1},{-1,0}};  // right, down, left, up

public:
  int numIslands(vector<vector<char>> &grid)
  {
    /**
     *  Breadth Firsth Search
     *  Go through every position, if that one is explorable ( 1 && not visted),
     *  use BFS, when BFS finish, one island complete
     * */
    int rowNum = grid.size();
    int colNum = grid[0].size();
    int islandCount = 0;

    vector<vector<bool>> visted(rowNum, vector<bool>(colNum, false));

    for (int row = 0; row < rowNum; ++row)
    {
      for (int col = 0; col < colNum; ++col)
      {

        if (grid[row][col] == '1' && visted[row][col] == false)
        {
          /* find a possible place, start BFS*/
          queue<pair<int, int>> front;
          front.push(make_pair(row, col));

          while (front.empty() != true)
          {
            pair<int, int> tmpRowCol = front.front();
            front.pop();
            visted[tmpRowCol.first][tmpRowCol.second] = true;

            for(int move = 0; move < 4; ++move)
            {
              int nextRow = tmpRowCol.first + movement[move][0];
              int nextCol = tmpRowCol.second + movement[move][1];

              if(nextRow >= 0 && nextRow < rowNum && nextCol >= 0 && nextCol < colNum && visted[nextRow][nextCol] == false && grid[nextRow][nextCol] == '1')
              {
                front.push(make_pair(nextRow, nextCol));
              }
            }
          }
          islandCount++;
        }
      }
    }

    return islandCount;
  }
};

int main()
{
  /* input*/
  vector<vector<char>> input = {{'1', '1', '1', '1', '0'},
                                {'1', '1', '0', '1', '0'},
                                {'1', '1', '0', '0', '0'},
                                {'0', '0', '0', '0', '0'}};

  /* test*/
  Solution test;
  int ret = test.numIslands(input);

  return 0;
}
```