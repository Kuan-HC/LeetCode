# 面試金典 1618 水域大小

你有一個用於表示一片土地的整數矩陣land，該矩陣中每個點的值代表對應地點的海拔高度。若值為0則表示水域。由垂直、水平或對角連接的水域為池塘。
池塘的大小是指相連接的水域的個數。編寫一個方法來計算矩陣中所有池塘的大小，返回值需要從小到大排序。

## Pond Size

You have an integer matrix representing a plot of land, where the value at that loca­tion represents the height above sea level.
A value of zero indicates water. A pond is a region of water connected vertically, horizontally, or diagonally. 
The size of the pond is the total number of connected water cells. Write a method to compute the sizes of all ponds in the matrix.

 
[LeetCode](https://leetcode-cn.com/problems/pond-sizes-lcci/)

### Example 1
```
Input: 
[
  [0,2,1,0],
  [0,1,0,1],
  [1,1,0,1],
  [0,1,0,1]
]
Output:  [1,2,4]
```


### C++ 

```
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

/*  Definition for a binary tree node. */
class Solution
{
    vector<vector<bool>> visted;
    vector<vector<int>> movement = {{-1,0},{1,0},{0,-1},{0,1}, {-1,1},{1,1},{-1,-1},{1,-1}};

public:
    vector<int> pondSizes(vector<vector<int>> &land)
    {
        int rowNum = land.size();
        int colNum = land[0].size();

        visted.resize(rowNum, vector<bool>(colNum, false));

        /* iterate matrix, if that spot is water and not visted yet, expand it*/

        vector<int> retSize;
        
        for(int row = 0; row < rowNum; ++row)
        {
            for(int col = 0; col < colNum; ++col)
            {
                if(land[row][col] == 0 && visted[row][col] != true)
                {
                    /* Breadth first search */
                    int pondSize = 1; 
                    /* set start point*/
                    queue<pair<int,int>> front;                    
                    front.push(make_pair(row,col));
                    visted[row][col] = true;
                    /* start bfs*/
                    while(front.empty() != true)
                    {
                        pair<int,int> temp = front.front();
                        front.pop();
                        for(const auto& move: movement)
                        {
                            int nextRow = temp.first + move[0];
                            int nextCol = temp.second + move[1];
                            if(    nextRow >= 0 && nextRow < rowNum 
                                && nextCol >= 0 && nextCol < colNum
                                && land[nextRow][nextCol] == 0 && visted[nextRow][nextCol] != true)
                            {
                                front.push(make_pair(nextRow, nextCol));
                                visted[nextRow][nextCol] = true;
                                pondSize++;
                            }
                        }
                    }
                    retSize.push_back(pondSize);                    
                }
            }
        }
        sort(retSize.begin(), retSize.end());
        return retSize;
    }
};

int main(void)
{
    /* input*/
    vector<vector<int>> input = {
        {0, 2, 1, 0},
        {0, 1, 0, 1},
        {1, 1, 0, 1},
        {0, 1, 0, 1}};
    /* test*/
    Solution test;
    vector<int> res = test.pondSizes(input);

    return 0;
}
```
