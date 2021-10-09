# 面試金典 1622 蘭頓螞蟻

一只蚂蚁坐在由白色和黑色方格构成的无限网格上。开始时，网格全白，蚂蚁面向右侧。每行走一步，蚂蚁执行以下操作。

(1) 如果在白色方格上，则翻转方格的颜色，向右(顺时针)转 90 度，并向前移动一个单位。
(2) 如果在黑色方格上，则翻转方格的颜色，向左(逆时针方向)转 90 度，并向前移动一个单位。

编写程序来模拟蚂蚁执行的前 K 个动作，并返回最终的网格。

网格由数组表示，每个元素是一个字符串，代表网格中的一行，黑色方格由 'X' 表示，白色方格由 '_' 表示，蚂蚁所在的位置由 'L', 'U', 'R', 'D' 表示，分别表示蚂蚁 左、上、右、下 的朝向。只需要返回能够包含蚂蚁走过的所有方格的最小矩形。

[LeetCode](https://leetcode-cn.com/problems/langtons-ant-lcci)

### Example 1
```
Input: 0
Output: ["R"]
```

### Example 2
```
Input: 2
Output:
[
  "_X",
  "LX"
]
```

### C++ 


```
class Solution
{
private:
    enum ground
    {
        Black,
        White
    };
    int movement[4][2] = {{0, 1}, {-1, 0}, {0, -1}, {1, 0}};
    char direction[4] = {'R', 'D', 'L', 'U'};

public:
    vector<string> printKMoves(int K)
    {
        map<pair<int, int>, ground> mapColor;
        /* initial condition*/
        int xMax = 0;
        int xMin = 0;
        int yMax = 0;
        int yMin = 0;
        int currX = 0;
        int currY = 0;
        int action = 0;

        for (int i = 0; i < K; i++)
        {
            ground tempColor = White; // default all ground is white
            if (mapColor.find({currX, currY}) == mapColor.end())
                tempColor = White;
            else
                tempColor = mapColor[{currX, currY}];

            /* flip color of current positoin and add it to map*/
            action = action + (tempColor == White ? 1 : -1);
            action = ((action % 4) + 4) % 4;
            mapColor[{currX, currY}] = tempColor == Black ? White : Black;
            /* change direction*/
            currX = currX + movement[action][0];
            currY = currY + movement[action][1];
            xMax = max(xMax, currX);
            xMin = min(xMin, currX);
            yMax = max(yMax, currY);
            yMin = min(yMin, currY);
            printf("debug");
        }

        vector<string> ret;

        for (int row = xMax; row >= xMin; row--)
        {
            string tempRow = "";
            for (int col = yMin; col <= yMax; col++)
            {
                if (row == currX && col == currY)
                {
                    tempRow += direction[action];
                    continue;
                }

                if (mapColor.find({row, col}) == mapColor.end())
                    tempRow += '_';
                else if (mapColor[{row, col}] == White)
                    tempRow += '_';
                else
                    tempRow += 'X';
            }
            ret.emplace_back(tempRow);
        }

        return ret;
    }
};
```
