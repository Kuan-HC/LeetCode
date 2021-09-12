# 面試金典 0810 顏色填充

編寫函數，實現許多圖片編輯軟件都支持的「顏色填充」功能。

待填充的圖像用二維數組 image 表示，元素為初始顏色值。初始坐標點的行坐標為 sr 列坐標為 sc。需要填充的新顏色為 newColor 。

「周圍區域」是指顏色相同且在上、下、左、右四個方向上存在相連情況的若幹元素。

請用新顏色填充初始坐標點的周圍區域，並返回填充後的圖像。

 
##  Color Fill
Implement the "paint fill" function that one might see on many image editing programs. That is, given a screen (represented by a two-dimensional array of colors), a point, and a new color, fill in the surrounding area until the color changes from the original color.


[LeetCode](https://leetcode-cn.com/problems/color-fill-lcci)


### Example 1
```
輸入：
image = [[1,1,1],[1,1,0],[1,0,1]] 
sr = 1, sc = 1, newColor = 2
輸出：[[2,2,2],[2,2,0],[2,0,1]]
解釋: 
初始坐標點位於圖像的正中間，坐標 (sr,sc)=(1,1) 。
初始坐標點周圍區域上所有符合條件的像素點的顏色都被更改成 2 。
注意，右下角的像素沒有更改為 2 ，因為它不屬於初始坐標點的周圍區域。
```

### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
#include <queue>

using namespace std;

class Solution
{
private:
    vector<vector<int>> movement = {
        {0, 1},
        {1, 0},
        {0, -1},
        {-1, 0},
    }; // right, down, left, up

public:
    vector<vector<int>> floodFill(vector<vector<int>> &image, int sr, int sc, int newColor)
    {
        int oldColor = image[sr][sc];
        if(oldColor == newColor)
            return image;
            
        int rowNum = image.size();
        int colNum = image[0].size();

        /*Breadth first search*/
        image[sr][sc] = newColor;
        queue<pair<int, int>> front;
        front.push(make_pair(sr, sc));

        int nextRow = 0;
        int nextCol = 0;

        while (front.empty() != true)
        {
            pair<int, int> temp = front.front();
            front.pop();

            for (int i = 0; i < 4; ++i)
            {
                nextRow = temp.first + movement[i][0];
                nextCol = temp.second + movement[i][1];

                if(nextRow >= 0 && nextRow < rowNum && nextCol >= 0 && nextCol < colNum && image[nextRow][nextCol] == oldColor)
                {
                    image[nextRow][nextCol] = newColor;
                    front.push(make_pair(nextRow, nextCol));
                }
            }
        }

        return image;
    }
};

int main()
{
    /* input */
    vector<vector<int>> input = {{0,0,0}, {0,1,1}};

    /* Algorithm */
    Solution test;
    vector<vector<int>> res = test.floodFill(input, 1, 1, 1);

    return 0;
}
```
